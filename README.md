# SV3D: Novel Multi-view Synthesis and 3D Generation from a Single Image using Latent Video Diffusion

This repository is for environment setup and inference of the paper "SV3D: Novel Multi-view Synthesis and 3D Generation from a Single Image using Latent Video Diffusion."

## result

[https://github.com/Jaeae/sv3d/blob/main/outputs/simple_video_sample/sv3d_p/000000.mp4](https://github.com/user-attachments/assets/6934012c-2e0b-459a-b83c-46a7badc68c5)

[https://github.com/Jaeae/sv3d/blob/main/outputs/simple_video_sample/sv3d_p/000001.mp4](https://github.com/user-attachments/assets/c04a93e7-81f8-4f13-bdf0-0d5ea8c7ed5a)

## setup
Our default, provided install method is based on Conda package and environment management:

```bash
conda create -n sv3d python=3.10
conda activate sv3d
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118 # check CUDA version
pip3 install -r requirements/pt2.txt
pip3 install .
pip3 install -e git+https://github.com/Stability-AI/datapipelines.git@main#egg=sdata
```

## To run SV3D_u on a single image
### 1. download the model

```bash
pip install huggingface_hub
huggingface-cli login
huggingface-cli download stabilityai/sv3d sv3d_u.safetensors --local-dir checkpoints
```

### 2. Run the code
```
scripts/sampling/simple_video_sample.py --input_path <path/to/image.png> --version sv3d_u
```


## To run SV3D_p on a single image:
### 1. download the model
```bash
pip install huggingface_hub
huggingface-cli login
huggingface-cli download stabilityai/sv3d sv3d_p.safetensors --local-dir checkpoints
```
### 2. Run the code
Generate static orbit at a specified elevation eg. 10.0 
```bash
python scripts/sampling/simple_video_sample.py \
  --input_path <path/to/image.png> \
  --version sv3d_p \
  --elevations_deg 10.0
```

Generate dynamic orbit at a specified elevations and azimuths: 
specify sequences of 21 elevations (in degrees) to elevations_deg ([-90, 90]), and 21 azimuths (in degrees) to azimuths_deg [0, 360] in sorted order from 0 to 360. 
```bash
python scripts/sampling/simple_video_sample.py --input_path <path/to/image.png> --version sv3d_p --elevations_deg [<list of 21 elevations in degrees>] --azimuths_deg [<list of 21 azimuths in degrees>]
```

## BibTeX
```bibtex
@misc{voleti2024sv3dnovelmultiviewsynthesis,
  title        = {SV3D: Novel Multi-view Synthesis and 3D Generation from a Single Image using Latent Video Diffusion},
  author       = {Vikram Voleti and Chun-Han Yao and Mark Boss and Adam Letts and David Pankratz and Dmitry Tochilkin and Christian Laforte and Robin Rombach and Varun Jampani},
  year         = {2024},
  eprint       = {2403.12008},
  archivePrefix= {arXiv},
  primaryClass = {cs.CV},
  url          = {https://arxiv.org/abs/2403.12008}
}



