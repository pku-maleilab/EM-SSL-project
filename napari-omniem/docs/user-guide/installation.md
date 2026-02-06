# Installation

This guide walks you through installing **Napari-OmniEM** from a downloaded archive and preparing the runtime environment.

---

## Step 1: Download Napari-OmniEM

Download the `napari-omniem.zip` archive from the given google driver folder  xz and extract it to a local directory:

```bash
unzip napari-omniem.zip
cd napari-omniem
```

## Step 2: Create a Conda Environment

We recommend using `conda` to manage dependencies.

```bash
conda create -n napari-omniem python=3.11 -y
conda activate napari-omniem
```

## Step 3: Install PyTorch with CUDA Support

Install PyTorch with the appropriate CUDA version for your system.

```bash
# Example: CUDA 11.8
pip install torch torchvision torchaudio \
  --index-url https://download.pytorch.org/whl/cu118
```

Visit [PyTorch](https://pytorch.org/) to find the correct installation command for your GPU and CUDA version.
If you do not have a GPU, install the CPU-only version instead.

## Step 4: Install Napari

Install napari and its GUI dependencies

```bash
pip install napari[all]
```

## Step 5: Install Napari-OmniEM

Install the plugin in editable (development) mode:

```bash
pip install -e .
```

This makes the plugin immediately available in napari.

## Step 6: Launch Napari

Start napari from the command line:

```bash
napari
```
Once napari is running, you should be able to find OmniEM in the plugin menu.

![Location of OmniEM in Plugins](imgs/plugins-omniem.png)
---

## Notes

- Ensure that your GPU drivers and CUDA runtime are properly installed before installing PyTorch with CUDA support.
- For large-volume inference, sufficient GPU memory and disk space are required.
- Multi-GPU inference is supported when multiple CUDA devices are available.
