Usage
=====

Running the Scanner
-------------------

The scanner runs inside the UE5 editor using the Python scripting plugin.

1. Place assets into ``/Game/DropOff`` in the Content Browser.
2. Open the UE5 Output Log and run the script via **File > Execute Python Script**.
3. Select ``scan_assets.py``.

The script will scan all Static Meshes and Texture2D assets found under
``SCAN_PATH`` and print a summary to the Output Log. Two output files are
written to the same directory as the script:

- ``scan_results.csv`` — raw flagged asset data
- ``scan_results.md`` — formatted Markdown report

Generating the Visual Report
-----------------------------

After the scan, run ``generate_report.py`` from outside the editor using
a standard Python installation:

.. code-block:: bash

   py generate_report.py

The script searches for ``scan_results.csv`` from the current working
directory. You can also pass the path explicitly:

.. code-block:: bash

   py generate_report.py "path/to/folder"

This validates the CSV data, generates a ``scan_results.png`` graph, and
rebuilds ``scan_results.md`` with the graph embedded.

Example Call Flow
-----------------

The following shows a typical end-to-end scan and report cycle:

.. code-block:: text

   [UE5 Editor]
   Execute scan_assets.py
        |
        +--> scan_results.csv  (raw flagged data)
        +--> scan_results.md   (basic report)

   [Terminal]
   py generate_report.py
        |
        +--> Validates CSV (unit tests)
        +--> Generates scan_results.png
        +--> Rebuilds scan_results.md with embedded graphs

Configuring Thresholds
-----------------------

Thresholds are defined as constants at the top of ``scan_assets.py``:

.. code-block:: python

   MAX_TRIANGLES    = 10000
   MAX_TEXTURE_SIZE = 2048
   MIN_LODS         = 2
   MAX_ASSET_SIZE_MB = 1.0
   SCAN_PATH        = "/Game/DropOff"

Adjust these values to match your project's requirements before running
the scan.
