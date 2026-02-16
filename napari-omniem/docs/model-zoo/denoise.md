
# Denoise

## Task Type
Image Restoration

## Description

The Denoise model reduces noise in EM images while preserving ultrastructural details.  
It is trained for low-level noisy restoration (from [EMDiffuse Dataset](https://www.nature.com/articles/s41467-024-49125-z)) without post-processing.

---

## Configuration

```yaml
name: Denoise
tasktype: 1
solution:
  - backbone_config: vitl.yaml
    datatypes:
      - 2
      - 3
    img_z: 1
    name: emdiffuse-l
    note: trained on EMDiffuse dataset, Low-level, no post-processing, alpha=0.25, beta=0.25
    weights: weights/denoise/981553_model_199.pt
```


## Model Characteristics

- 2D model (img_z = 1)

- Accepts both 2D and 3D input

- 3D input processed slice-wise

- No post-processing applied