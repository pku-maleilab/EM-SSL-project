# In-memory inference

In-memory inference is performed directly within the main **Napari-OmniEM** panel and operates on image data loaded as napari image layers. All computation is executed in memory, making this mode ideal for **interactive exploration, debugging, and small-to-medium EM datasets** that fit into GPU/CPU memory.

## Quick Start (Minimal Steps)

1. Open napari and load an EM image or volume.

2. Open **Plugins → OmniEM**.

3. Click **🔄 Refresh / Register** to detect loaded data.

4. Select **Data**, **Task**, and **Solution**.

5. Click **Run** → confirm → view results in napari.

For more control and advanced settings, see the detailed steps below.

## Step 1: Select data

- Load image data into napari via *File → Open File(s)*.

    - The data will appear as one or more **image layers**.

- Click the 🔄 **Refresh / Register** button in the *Napari-OmniEM* panel to register the currently loaded image layers.

- Select the target image from the **Data** dropdown list.

- If the selected data is a **3D volume**, specify the **z-dimension**:

    - By default, the axis with the **minimum side length** is automatically chosen.

    - You can override this if your data uses a different axis convention.

## Step 2: Select task and solution

- Choose a **Task** corresponding to the intended processing goal (e.g., segmentation, restoration).

- Select a compatible **Solution** from the **Solution** list.

    - Only solutions that are compatible with the selected data (dimensionality, modality, and task) will be shown.

    - For detailed descriptions of available tasks and solutions, refer to the [Model Zoo](../model-zoo/index.md).

> Terminology note
> - **Task**: defines *what* problem is being solved.
> - **Solution**: a concrete model + configuration that solves a task.

This terminology is consistent across **in-memory** and **local inference** modes.

## Step 3 advanced settings for sliding window inference

- In-memory inference uses the same sliding window mechanism as local inference.

- Adjust sliding window hyperparameters (e.g., input size, overlap, batch size) as needed.
- For detailed explanations and recommended values, see:
     - [Sliding Window Parameters](sw.md)

> If you are unsure, the default parameters are generally safe for first-time use.

## Step 4: Run inference

- Click the **Run** button to open the inference dialog.

- Review:

    - Estimated number of batches

    - Region-of-interest (ROI) size

- Click **Run** in the dialog to start inference.

- Once inference finishes, close the dialog to view results directly in napari as new layers.

## Tips & Common Pitfalls
### Memory usage

- In-memory inference loads data and intermediate results into memory.

- For large 3D volumes, GPU memory can be exhausted quickly.

- If you encounter out-of-memory errors:

    - Reduce batch size (even 1 is acceptable)

    - Reduce input window size

    - Consider using **Local Inference** instead

### Batch size

- Batch size primarily affects memory usage, not output quality.

- Small batch sizes are recommended for large EM data.

### Refresh/Register button

- Always click 🔄 Refresh / Register after:

    - Loading new data

    - Removing image layers

    - Renaming layers

- Failure to do so may result in missing or outdated data selections.

### When to use Local Inference instead

Use [Local Inference](local.md) if:

- The dataset is too large to fit into memory

- You want multi-GPU parallel inference

- You want to save results directly to disk (e.g., TIFF, Zarr, Dask)

## Related Pages

- [Local Inference](local.md)

- [Sliding Window Parameters](sw.md)

- [Task and Solution Manage](manage.md)

- [Model Zoo](../model-zoo/index.md)