# Networking, Security & Compliance — UE5 Asset Scanner

## Identified Risks

### 1. Network Transmission
The tool currently operates **entirely locally**. It reads from the local UE5 asset registry and writes output files to the same directory as the script. No network calls are made, no data is sent anywhere. In its current form there is no network attack surface.

However, the output files (`scan_results.csv`, `scan_results.md`) may be committed to a shared repository (e.g. GitHub), at which point asset metadata, including internal content paths and file sizes can be transmitted and stored externally. This is a low-risk exposure but worth being intentional about.

### 2. Sensitive Project or Player Data Exposure
The tool does not touch player data or runtime game state. What it does expose is **internal project structure**:

- Asset names and content folder paths (e.g. `/Game/DropOff/SM_CoinStack`)
- Triangle counts and texture resolutions, which could reveal the fidelity and scope of unreleased content
- File sizes, which could hint at the scale or complexity of in-development assets

If scan reports are committed to a public or insufficiently access-controlled repository, this metadata could be read by competitors before the game releases.

### 3. Exploitation and Manipulation
Because the script runs with full editor privileges inside UE5, a **malicious or tampered version of the script** could cause significant harm. Potential vectors:

- **Script substitution:** If the script lives in a shared network drive or is distributed without integrity checking, an attacker with access could replace it with a version that calls `unreal.EditorAssetLibrary.delete_asset()` or similar destructive functions.
- **Path injection via asset names:** Asset names are embedded directly into output strings. If the output is later consumed by another tool (e.g. parsed by a CI pipeline), a crafted asset name containing characters like `;`, `|`, or newlines could cause injection in that downstream system.
- **Hardcoded scan path:** `SCAN_PATH = "/Game/DropOff"` is hardcoded in the script. If misconfigured or changed to `/Game`, the script would load every asset in the project, which could cause editor instability or be used to get the full asset list.

### 4. What Happens if Compromised
A compromised version of this script could:
- Delete or corrupt assets silently during what appears to be a routine scan
- Expose the full asset list to an external endpoint
- Write false scan results that hide real issues or falsely flag clean assets


### 5. Internal Team Misuse
- A team member could modify thresholds (`MAX_TRIANGLES`, `MAX_TEXTURE_SIZE`, etc.) to suppress legitimate issues, effectively bypassing QA checks.
- The script could be run against unintended paths by changing `SCAN_PATH`.
- Results files could be manually edited before submission or review.

---

## Mitigations

### Script Integrity
- Store the canonical version of the script in a version-controlled repository with **branch protection** on the main branch. No direct pushes; changes must go through a pull request and be reviewed.

### Output Access Control
- Scan result files (`scan_results.csv`, `scan_results.md`) should be added to `.gitignore` if the repository is public, or kept in a private, access-controlled repo.
- If results need to be shared across a team, store them in a location with role-based access (e.g. a private channel or internal dashboard) rather than a public commit.

### Data Minimisation (GDPR)
- The tool does not collect or process personal data, so GDPR obligations are minimal. However, if in future the tool is extended to log which team member created or last modified an asset, that constitutes personal data and would require a data retention policy, and the ability to delete records on request.


### Encryption
- No encryption is required for the tool in its current local-only form.

### Authentication
- If a networked version is built, authenticate using short-lived tokens (e.g. OAuth 2.0 / personal access tokens with expiry) rather than static API keys or passwords embedded in the script.

---

## Could Networking Improve This Tool?


### Where Networking Adds Value

**1. Centralised validation and shared dashboards**
In a team environment, individual developers running scans locally means results are siloed and inconsistent (different thresholds, different versions of the script). A central server could:
- Receive scan results via an authenticated HTTPS POST request
- Store them in a database and expose them via a read-only web dashboard
- Surface trends over time (e.g. asset bloat creeping up over a sprint)

**2. Version control integration**
The scan could be triggered automatically as part of a CI/CD pipeline (e.g. GitHub Actions calling a UE5 command-line build). Results could be posted as pull request comments. This removes the dependency on developers remembering to run the scan manually and makes QA enforcement automatic.

### Where Networking Adds Unnecessary Complexity

**For solo use or very small teams**, none of the above is worth the infrastructure overhead. A shared Git repository with protected thresholds in a config file and a manual review process achieves most of the benefits with none of the operational cost.

### Client–Server Model Assessment
A client–server model would improve **trust and consistency** in a team context: the server becomes the authoritative source for thresholds and for the official record of scan results, preventing local manipulation. However, it introduces new risks (the server itself must be secured, patched, and backed up) and is only worthwhile if the team has the time and skills to maintain it.

