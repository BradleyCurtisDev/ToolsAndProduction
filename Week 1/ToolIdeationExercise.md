# Tool Proposal: Unreal Engine 5 Asset Audit Tool

## 1. Overview

I want to create a tool that can scan through the project files and find assets that are either too large or unoptimised. The tool will need to find textures that are too large, meshes with an excessive number of triangles.

## 2. Intended Users
The tool would be used by art leads and developers whos task is optimising the game. This could also be used by anyone who has access to the project but ideally it would output a report that could be sent to everyone involved with creating the assets for fast feedback.
* **Technical Artists:** To establish and enforce technical budgets and performance benchmarks across the project.
* **Environment & Prop Artists:** To check assets before using them in the scene to ensure they are up to standard.
* **Optimization/QA Leads:** To identify problem assets that are causing VRAM bottlenecks or "Out of Video Memory" crashes during the testing phase.

## 3. Target Platform
* **Development Environment:** Windows (Unreal Engine 5 Editor).
* **Target Deployment:** 
    * **PC:** Making sure the game runs on most hardware not just high end.

## 4. Key Data & File Formats
The tool will run through the Asset Registry to analyze metadata without the overhead of loading every asset into memory.
* **Primary File Type:** `.uasset`.
* **Class Focus:** `Texture2D`, `StaticMesh`.
* **Monitored Metadata:**
    * Finding any texture with a resolution of 4096 x 4096 or higher.
    *  Identifying assets exceeding a defined threshold in mb.
    * Checking for missing LOD settings.


## 5. Production Value

This asset scanner tool will help developers keep the game running smoothly and efficiently. It will also help them keep the game size down, which will make it easier for players to download and install the game. Art leads can use this tool to enforce technical budgets and performance benchmarks across the project. 

## Declared Assets

This document was modified and formatted with the use of:

- Claude Sonnet 4.6 (Claude, s.d.)

Claude (s.d.) At: https://claude.ai/login?from=logout (Accessed  22/04/2026).


- Google Gemini 3.1 Pro (Google Gemini, s.d.)

At: https://gemini.google.com (Accessed  22/04/2026).
