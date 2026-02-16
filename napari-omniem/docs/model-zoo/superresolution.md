# Super-resolution

## Task Type
Image Restoration

## Description

The Super-resolution model enhances spatial resolution of EM images.  
It is trained for low-level structural restoration (from [EMDiffuse Dataset](https://www.nature.com/articles/s41467-024-49125-z)) without post-processing.

---

## Configuration

```yaml
name: "Super-resolution"
tasktype: 1
solution:
  - backbone_config: vitl.yaml
    datatypes:
      - 2
      - 3
    img_z: 1
    name: emdiffuse-l
    note: trained on EMDiffuse dataset, Low-level, no post-processing, alpha=0.25, beta=0.25
    weights: weights/superreso/981474_model_199.pt
```

## Model Characteristics

- 2D model (img_z = 1)

- Accepts both 2D and 3D input

- 3D input processed slice-wise

- No post-processing applied