# Project Proposal: Unreal Engine 5 Asset Audit Tool (EUW)

## 1. Project Overview
The objective is to develop an Editor Utility Widget (EUW) within Unreal Engine 5 that automates the identification of project assets that exceed specific performance thresholds. The tool will specifically target textures with 4K resolutions and assets with excessive disk/memory footprints to ensure project stability and performance.

## 2. Intended Users
This tool is designed for integration into a professional collaborative pipeline, specifically targeting:
* **Technical Artists:** To establish and enforce technical budgets and performance benchmarks across the project.
* **Environment & Prop Artists:** To perform self-audits on individual assets before submitting work to source control, preventing "scope creep" in texture memory.
* **Optimization/QA Leads:** To identify "problem assets" that are causing VRAM bottlenecks or "Out of Video Memory" crashes during the testing phase.

## 3. Target Platform
* **Development Environment:** Windows / macOS (Unreal Engine 5 Editor).
* **Target Deployment:** While the tool runs in-editor, it is critical for optimizing builds for:
    * **Current-Gen Consoles (PS5/Xbox Series X):** Managing strict VRAM partitions.
    * **Mobile & VR (Quest 3):** Where texture memory is a primary bottleneck for frame rate stability.
    * **PC:** Ensuring scalability across various hardware tiers.

## 4. Key Data & File Formats
The tool will interface with the Asset Registry to analyze metadata without the overhead of loading every asset into memory.
* **Primary File Type:** `.uasset` (The standard Unreal Engine asset wrapper).
* **Class Focus:** `Texture2D`, `StaticMesh`.
* **Monitored Metadata:**
    * **Dimensions:** Flagging any texture with a resolution of 4096 x 4096 or higher.
    * **Resource Size:** Identifying assets exceeding a defined threshold in MB.
    * **LOD Bias / Compression:** Checking for uncompressed formats or missing LOD settings that contribute to unnecessary file bloat.

## 5. Production Value
The implementation of this tool provides three major benefits to a game production:

### A. Memory & Performance Management
A single 4K texture uses approximately 16x the memory of a 1K texture. By automating the detection of these assets, the tool prevents frame rate drops and crashes, ensuring the game stays within the target platform's hardware limitations.

### B. Build Size Optimization
Modern game installs are increasingly large. This tool identifies "bloated" assets early in the development cycle, allowing for better compression or downscaling. This results in smaller patch sizes and a reduced final installation footprint for the end-user.

### C. Workflow Efficiency (ROI)
Manually auditing thousands of project files is a high-cost, error-prone task. This widget automates the process, transforming a multi-hour manual search into a near-instantaneous report. This allows the creative team to focus on asset creation rather than technical troubleshooting.

## 6. Technical Implementation Note
The widget will utilize the Asset Registry Module in Blueprints/C++ to ensure high-speed scanning. By filtering by class and checking registry tags, the tool provides a non-destructive way to monitor project health without interrupting the creative workflow.