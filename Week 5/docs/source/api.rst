API Reference
=============

Constants
---------

These values are defined at the top of ``scan_assets.py`` and control
what the scanner flags.

.. list-table::
   :header-rows: 1
   :widths: 30 15 55

   * - Name
     - Default
     - Description
   * - ``MAX_TRIANGLES``
     - ``10000``
     - Maximum triangle count allowed for a Static Mesh
   * - ``MAX_TEXTURE_SIZE``
     - ``2048``
     - Maximum width or height in pixels allowed for a Texture2D
   * - ``MIN_LODS``
     - ``2``
     - Minimum number of LOD levels required on a Static Mesh
   * - ``MAX_ASSET_SIZE_MB``
     - ``1.0``
     - Maximum file size on disk in MB for any asset
   * - ``SCAN_PATH``
     - ``/Game/DropOff``
     - UE5 content path to scan recursively

----

scan_assets.py
--------------

scan_meshes()
~~~~~~~~~~~~~

Scans all Static Mesh assets found under ``SCAN_PATH`` and checks them
against the triangle count, LOD count, and file size thresholds.

**Parameters**

None. Uses the module-level constants.

**Returns**

``list[dict]`` — A list of flagged asset entries. Each dict contains:

.. list-table::
   :header-rows: 1
   :widths: 20 15 65

   * - Key
     - Type
     - Description
   * - ``type``
     - ``str``
     - ``"MESH"``, ``"LOD"``, or ``"SIZE"``
   * - ``name``
     - ``str``
     - The asset name as it appears in the Content Browser
   * - ``path``
     - ``str``
     - The UE5 content path of the asset (e.g. ``/Game/DropOff/3D``)
   * - ``issue``
     - ``str``
     - Human-readable description of the violation

**Errors**

- Returns an empty list if no Static Meshes are found at ``SCAN_PATH``.
- An asset is silently skipped if ``load_asset`` returns a non-mesh object.

----

scan_textures()
~~~~~~~~~~~~~~~

Scans all Texture2D assets found under ``SCAN_PATH`` and checks them
against the resolution and file size thresholds.

**Parameters**

None. Uses the module-level constants.

**Returns**

``list[dict]`` — A list of flagged asset entries. Each dict contains:

.. list-table::
   :header-rows: 1
   :widths: 20 15 65

   * - Key
     - Type
     - Description
   * - ``type``
     - ``str``
     - ``"TEXTURE"`` or ``"SIZE"``
   * - ``name``
     - ``str``
     - The asset name as it appears in the Content Browser
   * - ``path``
     - ``str``
     - The UE5 content path of the asset
   * - ``issue``
     - ``str``
     - Human-readable description of the violation

**Errors**

- Returns an empty list if no Texture2D assets are found at ``SCAN_PATH``.
- An asset is silently skipped if ``load_asset`` returns a non-texture object.

----

get_asset_size_mb(asset_data)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Returns the file size on disk of a UE5 asset by resolving its ``.uasset``
path from the project content directory.

**Parameters**

.. list-table::
   :header-rows: 1
   :widths: 20 20 60

   * - Name
     - Type
     - Description
   * - ``asset_data``
     - ``unreal.AssetData``
     - The asset data object returned by the asset registry

**Returns**

``float | None`` — File size in MB rounded to 2 decimal places, or
``None`` if the ``.uasset`` file could not be found on disk.

----

generate_markdown(flagged_assets, script_dir)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Generates a Markdown report from the list of flagged assets and writes
it to ``scan_results.md`` in the script directory.

**Parameters**

.. list-table::
   :header-rows: 1
   :widths: 20 20 60

   * - Name
     - Type
     - Description
   * - ``flagged_assets``
     - ``list[dict]``
     - The combined output of ``scan_meshes()`` and ``scan_textures()``
   * - ``script_dir``
     - ``str``
     - Absolute path to the directory where the report will be written

**Returns**

``str`` — The absolute path to the written ``.md`` file.

**Errors**

- Raises ``OSError`` if the script directory is not writable.

----

print_and_export(flagged_assets)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Prints a summary of all flagged assets to the UE5 Output Log, exports
the results to ``scan_results.csv``, and calls ``generate_markdown()``
to write the Markdown report.

**Parameters**

.. list-table::
   :header-rows: 1
   :widths: 20 20 60

   * - Name
     - Type
     - Description
   * - ``flagged_assets``
     - ``list[dict]``
     - The combined output of ``scan_meshes()`` and ``scan_textures()``

**Returns**

Nothing. Side effects: writes ``scan_results.csv`` and ``scan_results.md``
to the script directory and prints results to the Output Log.

**Errors**

- Raises ``OSError`` if the script directory is not writable.

----

generate_report.py
------------------

resolve_scan_dir(user_path)
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Locates the directory containing ``scan_results.csv``. If no path is
provided, searches recursively from the current working directory.

**Parameters**

.. list-table::
   :header-rows: 1
   :widths: 20 20 60

   * - Name
     - Type
     - Description
   * - ``user_path``
     - ``str | None``
     - Path to a folder or CSV file, or ``None`` to trigger auto-search

**Returns**

``str`` — Absolute path to the directory containing ``scan_results.csv``.

**Errors**

- Exits with an error message if the path does not exist.
- Exits with an error message if no ``scan_results.csv`` is found.
- Exits and lists all matches if multiple ``scan_results.csv`` files are found.

----

run_unit_tests(rows)
~~~~~~~~~~~~~~~~~~~~

Validates the loaded CSV data against a set of structural assertions.
Checks that the data is well-formed and that every flagged value genuinely
violates its threshold.

**Parameters**

.. list-table::
   :header-rows: 1
   :widths: 20 20 60

   * - Name
     - Type
     - Description
   * - ``rows``
     - ``list[dict]``
     - Rows loaded from ``scan_results.csv``

**Returns**

``bool`` — ``True`` if all assertions pass, ``False`` if any fail.

----

generate_graph(rows, output_path)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Generates a three-chart matplotlib figure from the scan data and saves
it as a PNG.

Charts produced:

- **Issues by Type** — horizontal bar chart
- **Issues by Type and Folder** — grouped bar chart split by content path
- **File Size Violations** — ranked bar chart of all assets over the size limit

**Parameters**

.. list-table::
   :header-rows: 1
   :widths: 20 20 60

   * - Name
     - Type
     - Description
   * - ``rows``
     - ``list[dict]``
     - Rows loaded from ``scan_results.csv``
   * - ``output_path``
     - ``str``
     - Absolute path where the PNG will be saved

**Returns**

Nothing. Writes a PNG file to ``output_path``.

----

rebuild_markdown(rows, header_block, png_filename)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Reconstructs ``scan_results.md`` from scratch using the scan data and
the original header block preserved from the previous scan.

**Parameters**

.. list-table::
   :header-rows: 1
   :widths: 20 20 60

   * - Name
     - Type
     - Description
   * - ``rows``
     - ``list[dict]``
     - Rows loaded from ``scan_results.csv``
   * - ``header_block``
     - ``str``
     - The header section extracted from the existing ``scan_results.md``
   * - ``png_filename``
     - ``str``
     - Filename of the graph PNG (used as a relative image reference)

**Returns**

``str`` — The full Markdown content as a string. The caller is responsible
for writing it to disk.
