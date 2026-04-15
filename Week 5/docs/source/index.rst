UE5 Asset Scanner
=================

A Python QA tool for Unreal Engine 5. It scans a designated drop-off folder
and flags Static Meshes and Texture2D assets that exceed configurable thresholds
for triangle count, LOD count, texture resolution, and file size on disk.

Results are exported as a CSV and a Markdown report. A companion script
(``generate_report.py``) reads the CSV, validates the data, and rebuilds
the Markdown report with embedded matplotlib graphs.

.. toctree::
   :maxdepth: 2
   :caption: Contents

   usage
   api
