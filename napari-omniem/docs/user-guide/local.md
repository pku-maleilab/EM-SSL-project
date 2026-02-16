# Local Inference

Local (on-disk) inference is activated by clicking the 📁 button in the main **Napari-OmniEM** panel. In this mode, data are loaded from local files using `dask.array`, and intermediate results are currently stored as temporary **HDF5** files (this is the current implementation; more efficient backends are planned).

Compared with in-memory inference, local inference:

- Enables **multi-GPU parallel inference** when multiple GPUs are available

- Requires approximately **5–10× the original data size** to store temporary files

- Supports saving outputs in **multiple formats**, with optional visualization in napari

- Does **not** currently support the restoration→segmentation pipeline in a single run (restored images must be saved and reloaded for subsequent segmentation)

---

## Quick Start (Minimal Steps)

1. Open napari and launch **Plugins → OmniEM**.
2. Click 📁 to open the **Local Inference** panel.
3. Select input **Data**, **Task**, and **Solution**.
4. Click **Run**, confirm the settings, and start inference.
5. View results in napari or save them to disk.

For advanced configuration, see the detailed steps below.

---

## Step 0: Open Local Inference Panel

- Click the 📁 icon in the main **Napari-OmniEM** panel.
- This option is enabled only when a compatible GPU is available.

---

## Step 1: Select Data

- Click **Browse File** to select a local image or volume.
- Supported formats are those compatible with `dask.array`.
- Only **grayscale images** (no color channels) are accepted.
- If the data are 3D, specify the **z-dimension**:
    - By default, the axis with the **minimum side length** is selected.
    - Override this if your data use a different axis convention.

---

## Step 2: Select Task and Solution

- Task and solution selection is the same as in **in-memory inference**.
- Only solutions compatible with the selected data will be shown.

---

## Step 3: Advanced Settings (Sliding Window & Devices)

In addition to standard sliding window parameters, local inference provides two extra options:

- **Device selection**
    - GPU-only inference
    - Multiple GPUs can be selected
    - At least one GPU must be chosen

- **Temporary folder**
  - Specify the directory used to store temporary on-disk files during inference

For details on sliding window parameters, see the [Sliding Window Parameters](sw.md) page.

---

## Step 4: Run Inference

Before starting inference, the dialog displays:
    - **Estimated number of batches**

    - **Region of interest (ROI) size**

Steps:
    - Click **Run** to start inference.

    - When inference finishes, **Run** changes to **Redo**, allowing you to rerun with modified settings.

---

## Step 5: Save Output

Supported output options include:

1. **Open in napari**  

   - Both input data and results can be loaded  

   - Use with caution for very large datasets

2. **Standard file formats**

   - TIFF

   - PNG (2D results only)

   - NumPy (`.npy`)

3. **Chunked storage formats**

   - Zarr

   - NumPyStack

---

## Tips & Common Pitfalls

- Ensure sufficient disk space for **temporary files** (5–10× input size).
- For very large volumes, prefer smaller batch sizes to reduce peak memory usage.
- Clean up temporary folders before inference if disk space is limited.
- Temporary files are be removed automatically after inference.

---

## Related Pages

- [In-memory Inference](in-memory.md)
- [Sliding Window Parameters](sw.md)
- [Task and Solution Management](manage.md)
- [Model Zoo](../model-zoo/index.md)
