# Networking, Security & Compliance — UE5 Asset Scanner

**Tool selected:** `scan_assets.py` — a Python script that runs inside the Unreal Engine 5 editor via the Python scripting plugin. It scans a designated content folder (`/Game/DropOff`) for Static Meshes and Texture2D assets, flags those that breach configurable thresholds (triangle count, texture resolution, LOD count, file size on disk), and exports results to a `.csv` and a `.md` report.

---

## Identified Risks

### 1. Network Transmission
The tool currently operates **entirely locally**. It reads from the local UE5 asset registry and writes output files to the same directory as the script. No network calls are made, no data is sent anywhere. In its current form there is no network attack surface.

However, the output files (`scan_results.csv`, `scan_results.md`) may be committed to a shared repository (e.g. GitHub), at which point asset metadata — including internal content paths and file sizes — is transmitted and stored externally. This is a low-risk exposure but worth being intentional about.

### 2. Sensitive Project or Player Data Exposure
The tool does not touch player data or runtime game state. What it does expose is **internal project structure**:

- Asset names and content folder paths (e.g. `/Game/DropOff/SM_TreeHouse`)
- Triangle counts and texture resolutions, which could reveal the fidelity and scope of unreleased content
- File sizes, which could hint at the scale or complexity of in-development assets

If scan reports are committed to a public or insufficiently access-controlled repository, this metadata could be read by competitors or bad actors before a game ships.

### 3. Exploitation and Manipulation
Because the script runs with full editor privileges inside UE5, a **malicious or tampered version of the script** could cause significant harm. Potential vectors:

- **Script substitution:** If the script lives in a shared network drive or is distributed without integrity checking, an attacker with access could replace it with a version that calls `unreal.EditorAssetLibrary.delete_asset()` or similar destructive functions.
- **Path injection via asset names:** Asset names are embedded directly into output strings. If the output is later consumed by another tool (e.g. parsed by a CI pipeline), a crafted asset name containing characters like `;`, `|`, or newlines could cause injection in that downstream system.
- **Hardcoded scan path:** `SCAN_PATH = "/Game/DropOff"` is hardcoded in the script. If misconfigured or changed to `/Game`, the script would load every asset in the project, which could cause editor instability or be used to exfiltrate a full asset manifest.

### 4. What Happens if Compromised
A compromised version of this script could:
- Delete or corrupt assets silently during what appears to be a routine scan
- Exfiltrate the full asset manifest to an external endpoint
- Write false scan results that hide real issues or falsely flag clean assets

The blast radius is limited to the editor session and the local file system, but in a team context this could affect shared project state if content is on a network drive.

### 5. Internal Team Misuse
- A team member could modify thresholds (`MAX_TRIANGLES`, `MAX_TEXTURE_SIZE`, etc.) to suppress legitimate issues, effectively bypassing QA checks.
- The script could be run against unintended paths by changing `SCAN_PATH`.
- Results files could be manually edited before submission or review.

### 6. Misconfiguration
- Setting `MAX_ASSET_SIZE_MB = 1.0` is very conservative. If misconfigured to a very high value, large assets would pass silently.
- If `SCAN_PATH` is set to a path that doesn't exist, the script exits silently with zero flagged assets — which could be mistaken for a clean result.

### 7. Data Leakage
The CSV and Markdown outputs are written to the script's local directory with no access restrictions. Any process or user with read access to that directory can read the scan results.

---

## Mitigations

### Script Integrity
- Store the canonical version of the script in a version-controlled repository with **branch protection** on the main branch. No direct pushes; changes must go through a pull request and be reviewed.
- Optionally, generate and publish a checksum (e.g. SHA-256) of the script as part of the release process. Team members can verify the script has not been tampered with before running it.

### Output Access Control
- Scan result files (`scan_results.csv`, `scan_results.md`) should be added to `.gitignore` if the repository is public, or kept in a private, access-controlled repo.
- If results need to be shared across a team, store them in a location with role-based access (e.g. a private channel or internal dashboard) rather than a public commit.

### Input Sanitisation (for downstream use)
- If scan output is ever consumed programmatically (e.g. by a CI parser), sanitise asset name and path strings before processing. Strip or escape characters like `;`, `|`, `\n`, and `"`.
- Validate that `SCAN_PATH` resolves to a real content path before beginning the scan, and surface an explicit warning rather than silently returning zero results.

### Threshold Configuration
- Move thresholds (`MAX_TRIANGLES`, `MAX_TEXTURE_SIZE`, `MIN_LODS`, `MAX_ASSET_SIZE_MB`) out of the script and into a separate config file (e.g. `scan_config.json`). Version-control the config separately with the same branch protections as the script, so threshold changes are auditable.

### Logging and Auditing
- The script currently prints results to the UE5 Output Log. Add a log entry that records **who ran the scan** (OS username via `os.getenv("USERNAME")`) and **when**, alongside the results. Append this to a persistent audit log rather than overwriting it each run.
- This makes it possible to detect if results were suppressed or if the script was run by an unexpected user.

### Data Minimisation (GDPR principle)
- The tool does not collect or process personal data, so GDPR obligations are minimal. However, if in future the tool is extended to log which team member created or last modified an asset, that constitutes personal data and would require: a lawful basis, a data retention policy, and the ability to delete records on request.
- For now: log only what is necessary for QA (asset paths, metrics, timestamps). Do not add attribution data unless there is a specific need.

### Encryption
- No encryption is required for the tool in its current local-only form.
- If results are transmitted in the future (see below), HTTPS is the minimum requirement for any REST endpoint; TLS 1.2+ only.

### Authentication
- Not applicable locally. If a networked version is built, authenticate using short-lived tokens (e.g. OAuth 2.0 / personal access tokens with expiry) rather than static API keys or passwords embedded in the script.

---

## Could Networking Improve This Tool?

The tool currently operates fully locally, which is simple, fast, and secure by default. Below is an honest evaluation of where networking could add value and where it would not.

### Where Networking Adds Value

**1. Centralised validation and shared dashboards**
In a team environment, individual developers running scans locally means results are siloed and inconsistent (different thresholds, different versions of the script). A central server could:
- Receive scan results via an authenticated HTTPS POST request
- Store them in a database and expose them via a read-only web dashboard
- Surface trends over time (e.g. asset bloat creeping up over a sprint)

This would require: a lightweight REST API (e.g. FastAPI), a database, and authentication — a meaningful but justified investment for a team of 5+ with regular asset reviews.

**2. Version control integration**
The scan could be triggered automatically as part of a CI/CD pipeline (e.g. GitHub Actions calling a UE5 command-line build). Results could be posted as pull request comments, blocking merges if thresholds are exceeded. This removes the dependency on developers remembering to run the scan manually and makes QA enforcement automatic.

**3. Centralised threshold management**
Rather than each developer having a local copy of `scan_config.json`, thresholds could be fetched from a config endpoint at scan start. This ensures all team members always run with the agreed standards, and changes take effect immediately without redistributing a file.

### Where Networking Adds Unnecessary Complexity

**For solo use or very small teams**, none of the above is worth the infrastructure overhead. A shared Git repository with protected thresholds in a config file and a manual review process achieves 80% of the benefit with none of the operational cost.

### Client–Server Model Assessment
A client–server model would improve **trust and consistency** in a team context: the server becomes the authoritative source for thresholds and for the canonical record of scan results, preventing local manipulation. However, it introduces new risks (the server itself must be secured, patched, and backed up) and is only worthwhile if the team has the capacity to maintain it.

**Recommendation:** Keep the tool local for now. Add a `scan_config.json` for threshold management and an audit log for traceability. If the team grows or asset reviews become a bottleneck, revisit a centralised dashboard as the next step. The tool does not need networking to be effective — and avoiding it keeps the attack surface small.
