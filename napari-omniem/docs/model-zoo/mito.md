# Mitochondria Segmentation

## Task Type
Segmentation

## Overview

The **Mitochondria Segmentation** model performs pixel-wise classification of mitochondria in electron microscopy (EM) images.  
It supports both 2D slice-wise model (trained on [CEM-Mitolab dataset](https://www.cell.com/cell-systems/fulltext/S2405-4712(22)00494-X)) and 3D volumetric-input model (trained on [MitoEM dataset](https://mitoem.grand-challenge.org/)).

This task outputs a labeled mask with the following classes:

- **Background**
- **Mitochondria**

---

## Available Solutions

### 1. ViT-L-2D

#### Configuration

```yaml
- name: "ViT-L-2D"
  note: "trained on CEM-MitoLab, no 3D fusion"
  datatypes:
    - 2
    - 3
  img_z: 1
  backbone_config: null
  weights: "weights/mito-seg/905953_model_199.pt"
```

#### Characteristics

* `img_z = 1` (2D model)
* Accepts:

  * 2D input
  * 3D input (processed slice-wise)
* No inter-slice fusion
* Suitable for fast inference and datasets without strong Z-continuity

#### Recommended Use Cases

* 2D EM slice segmentation
* Large-scale screening
* When Z-alignment consistency is uncertain

---

### 2. ViT-L-3D

#### Configuration

```yaml
- name: "ViT-L-3D"
  note: "trained on MitoEM, with 3D fusion, available when z_dim >= 16"
  datatypes:
    - 3
  img_z: 16
  backbone_config: null
  weights: "weights/mito-seg/909906_model_239.pt"
```

#### Characteristics

* `img_z = 16` (3D model)
* Accepts 3D input only
* Requires:
  * Z-dimension ≥ 16

---

## Output

The model produces a segmentation mask with:

| Label ID | Class Name   |
| -------- | ------------ |
| 0        | Background   |
| 1        | Mitochondria |

---

## Model Selection Guidance

| Scenario                            | Recommended Solution |
| ----------------------------------- | -------------------- |
| Single 2D slice analysis            | ViT-L-2D             |
| Thin Z-stack (< 16 slices)          | ViT-L-2D             |
| Thick volumetric dataset (≥ 16 Z)   | ViT-L-3D             |

Choose the 3D model when volumetric coherence is critical and sufficient Z-depth is available.
Use the 2D model for flexibility, speed, or limited Z-resolution datasets.

## Upcoming Updates

We are actively improving the mitochondria segmentation models. Planned updates include:

1. **Training on MitoEM 2.0 (3D Model)**  
   A new 3D segmentation model will be trained on the MitoEM 2.0 dataset to enhance volumetric accuracy, robustness, and generalization across diverse EM imaging conditions.

2. **Post-processing for Cross-Dimensional Consistency**  
   We will introduce post-processing techniques to improve consistency between:
   - Slice-wise 2D segmentation outputs  
   - Volumetric 3D segmentation outputs  

   These enhancements aim to reduce inter-slice discontinuities and improve structural coherence in reconstructed 3D volumes.

These updates will be released in future versions of Napari-OmniEM.
