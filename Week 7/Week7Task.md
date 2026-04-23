# Production Proposal — UE5 Asset Scanner

## What the Tool Does

The asset scanner is a two-part Python tool built for a UE5 project pipeline.

The first script (`scan_assets.py`) runs inside the UE5 editor using the Python scripting plugin. It scans a designated drop-off folder (`/Game/DropOff`) and checks every Static Mesh and Texture2D against a set of QA thresholds — triangle count, LOD count, texture resolution, and file size on disk. Anything that fails gets logged and exported to a CSV and a Markdown report.

The second script (`generate_report.py`) runs outside the editor. It reads the CSV, validates the data, generates matplotlib graphs, and rebuilds the Markdown report with the graphs embedded. It can be dropped into any repository and will search for `scan_results.csv` automatically.

The intention is that artists drop assets into the folder, a QA lead runs the scan, and the report gets committed to the shared repo for the team to review.

---

## Technical Stack

| Component | Technology |
|---|---|
| Editor scripting | Python 3.13 via UE5 Python Plugin |
| Game engine | Unreal Engine 5 |
| Report generation | Python 3.13, matplotlib |
| Version control | Git / GitHub |
| CI (optional) | GitHub Actions |

No backend server or database is needed. The tool is entirely file-based and runs locally on a developer machine.

---

## Hardware and Cloud Requirements

The tool runs on any machine capable of running UE5. There are no dedicated hosting requirements.

| Requirement | Detail |
|---|---|
| OS | Windows 10/11 (primary), macOS supported |
| RAM | 16 GB minimum (UE5 requirement) |
| Storage | Standard project storage — reports are text and a single PNG per scan |
| GPU | Required for UE5 editor, not for the scripts themselves |
| Network | Only needed if reports are pushed to a shared repository |

If the team wanted to automate scans on pull requests, a GitHub Actions runner or self-hosted CI agent would be needed. A self-hosted runner on an existing build machine would cover this at no extra cost.

---

## Cost Estimate

**Initial Setup**

| Item | Cost |
|---|---|
| UE5 licence | Free (royalty applies on shipped revenue over $1M) |
| Python + matplotlib | Free |
| GitHub repository | Free (private repos available on free tier) |
| Developer time to integrate into pipeline | ~1–2 days |

**Ongoing**

| Item | Estimated Cost |
|---|---|
| GitHub storage for reports | Negligible — text files and small PNGs |
| GitHub Actions CI minutes | Free tier (2,000 min/month) is sufficient for a scan that completes in under a minute |
| Maintenance | Occasional threshold updates as project standards evolve |

Total ongoing cost is effectively **£0/month** in the current local setup. If a hosted web dashboard were added in future (as discussed in the Week 3 networking evaluation), a small cloud instance would cost around **£5–10/month**.

---

## Target Platforms

The tool targets the **UE5 editor environment on Windows**, which is the primary development platform for the project. The report generator works on any platform with Python 3.x installed.

The scanned assets themselves are intended for a PC game build, so the thresholds (triangle limits, texture sizes) are set accordingly. If the project were to also target console or mobile, the thresholds would need adjusting and the scanner would need to be run per-platform configuration.

---

## System Diagram

```
+------------------+
|  Artist / QA     |
+--------+---------+
         |
         | Places assets in /Game/DropOff
         v
+------------------+        +--------------------+
|  UE5 Editor      |        |                    |
|  scan_assets.py  +------> |  scan_results.csv  |
|                  |        |  scan_results.md   |
+------------------+        +--------+-----------+
                                     |
                                     | generate_report.py reads CSV,
                                     | validates data, generates graphs,
                                     | rebuilds markdown
                                     v
                            +--------------------+
                            |  scan_results.md   |
                            |  (with graphs)     |
                            |  scan_results.png  |
                            +--------+-----------+
                                     |
                                     | Committed to shared Git repo
                                     v
                            +--------------------+
                            |  Team reviews      |
                            |  report on GitHub  |
                            +--------------------+
```

---

## Additional Notes

This tool does not involve multiplayer, connected systems, or a live backend, so those sections of the brief are not applicable. The tool is best kept local with version-controlled thresholds and an audit log if team size grows.

## Declared Assets

This document was modified and formatted with the use of:

- Claude Sonnet 4.6 (Claude, s.d.)

Claude (s.d.) At: https://claude.ai/login?from=logout (Accessed  29/03/2026).


- Google Gemini 3.1 Pro (Google Gemini, s.d.)

At: https://gemini.google.com (Accessed  29/03/2026).
