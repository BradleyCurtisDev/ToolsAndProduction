---
marp: true
theme: default
paginate: true
backgroundColor: #d7d7d7ff
---
![bg right:50% 100%](https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExeXY0dGZqdXdxcmxvYzk2dno4dnN4dGpubzdzMGswd3B4bWJqZ2tlNiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/YA6dmVW0gfIw8/giphy.gif)

# UE5 Asset Auditor
### Tools and Production FGCT5017
**Bradley Curtis**


---

## 1. Overview
**The Problem:** We all know artists' favourite things are to make mistakes, and Unreal Engine 5 projects are notorious for running terribly. High-poly meshes and 4K textures makes Steam builds massive and slow down players' PCs.

![bg right:30% 100%](https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExbTViaDZ5NWJybXdrbnE0eHp3eHM4czYzYzJtM3NybnVkdmo1MjRzMCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/800iiDTaNNFOwytONV/giphy.gif)

**The Solution:** The **Asset Auditor** is an Editor Utility Widget that automatically scans your project for 3d models and textures that the artists thought they cooked on but actually didn't. It identifies unoptimized assets, ensuring our game hits performance targets and keeps the final Steam download size lean.


---

## 2. Key Features & Problem Solving

| Feature | Problem Solved |
| :--- | :--- |
| **Texture Resolution Scan** | Prevents VRAM crashes on lower-end GPUs. |
| **Nanite Integrity Check** | Catches high-poly meshes that are missing Nanite optimization. |
| **Unnecessary Vertices** | Catches models with unreasonably high poly counts. |
| **One-Click Quick Fix** | Allows the team to downscale textures instantly without leaving the tool. |

---

## 3. Functionality (Visuals)

![bg right:50% 80%](https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExNjY4cGZpZTI3M2M4MWFiNjdhc2t3c3E0eTh3dTlwODQ4eXdxeTh5ZSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/ACeIDlMpgc4yOf1Lyt/giphy.gif)

* **Step 1:** Open the Utility Widget.
* **Step 2:** Click "Run Audit."
* **Step 3:** Review the flagged assets list.
* **Step 4:** Use the "Fix" buttons to optimize.

---

## 4. Security & Data Compliance (GDPR)

![bg right:40% 80%](https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExNTdqeGx0OGo3czlsOGcwYnBzZGV0NnVvc2dna29hMWx4MGFxZWdydCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/Dps6uX4XPOKeA/giphy.gif)

People reallly dont like if their data is used for some reason so the tool doesnt take any personal information, only the assets in the project are scanned.

* **Minimal Data Footprint:** The tool only reads **metadata** (file size, resolution) of local assets. It does not access personal developer data.
* **Local Processing:** All auditing happens within the Unreal Editor environment. No project data is sent to external servers.


---

## 5. Moving Forward

1.  **Automated Build Hooks:** Automatically run the audit before a Steam Build is cooked.
2.  **Naming Convention Check:** Ensure all assets follow the `T_` (Texture) or `SM_` (Static Mesh) prefix rules.
3.  **Direct Integration:** Add a "Delete Unused Assets" feature to remove files that aren't actually used in any levels.

---

## Any Questions?

![bg right:60% 80%](https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExZ2lnNmd6cnpwNGZhdXd1cHlqdGQxYnE4cmo5d2p1bzh1d3dtcXpiNiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/cjttePPEs1shFLDfh2/giphy.gif)