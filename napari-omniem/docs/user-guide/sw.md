# Sliding Window Parameters

Sliding window inference is used to process large 2D images or 3D volumes that cannot be forwarded through the model in a single pass. Napari-OmniEM applies window-based tiling with overlap and seamless merging to ensure both efficiency and output quality.

This page describes the key parameters that control sliding window inference and provides practical recommendations.

---

## Overview

During inference, the input image or volume is divided into overlapping tiles (windows). Each tile is processed independently by the model, and the results are merged to produce the final output.

Sliding window inference is used in:
- In-memory inference
- Local (out-of-core) inference

---

## Input XY Size

**Description**  
Defines the spatial size (in pixels) of each sliding window in the XY plane.

**Effect**
- Larger windows provide more spatial context and typically yield better prediction quality.
- Smaller windows reduce GPU memory usage but may degrade boundary consistency.

**Recommendation**
- Use the **largest size that fits in GPU memory**.

---

## Batch Size

**Description**  
Number of sliding windows processed simultaneously in a single forward pass.

**Effect**
- Larger batch sizes increase throughput.
- Smaller batch sizes reduce GPU memory usage.

**Recommendation**
- Set to **1** when GPU memory is limited.
- Increase gradually if memory allows.

---

## Overlap

**Description**  
Fractional overlap between adjacent sliding windows along each spatial dimension.

**Effect**
- Higher overlap improves boundary smoothness and reduces stitching artifacts.
- Lower overlap improves inference speed.

**Valid Range**
- `0.0` – `0.5`

**Recommendation**
- `0.1` is recommended for most inference tasks.
- Increase to `0.25` for boundary-sensitive tasks (e.g., segmentation).

---

## Practical Tips

- Prefer **larger XY sizes** over larger batch sizes for better prediction quality.
- Keep **overlap ≥ 0.1** to avoid visible stitching artifacts.
- If out-of-memory (OOM) errors occur:
    1. Reduce batch size
    2. Reduce XY size
    3. Reduce overlap (last resort)

---

## Modifying Default Sliding Window Settings

The default sliding window parameters can be modified from the main **Napari-OmniEM** panel.

- Click the ⚙️ **Settings** button in the panel.
- A new dialog window will appear.
- In the **Inference** tab, you can configure:

    - **Overlap**
  
    - **Batch size**

    - **Input XY size**

    - **Device** (single device selection for in-memory inference)

These settings define the default behavior for subsequent inference runs.

---

## Notes

> This page is under active development and will be updated with more information on memory usage under different parameter settings.

