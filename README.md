# Installing Comfyui for Apple Mac Silicon
This is missing installation instruction for installing Comfyui on Apple Mac M1/M2, Metal Performance Shaders (MPS) backend for GPU

Requirements

1. **macOS 12.3** or (update to latest release)
  
2. download and Install **Python 3.10** (download from Python site: [macOS 64-bit universal2 installer](https://www.python.org/ftp/python/3.11.4/python-3.11.4-macos11.pkg)) once installed from the Application folder: double click and install the "Install Certificates.command" and "Update Shell Profile.command" both files will open in Terminal
  
3. Install **Xcode** command-line tools (Download [Xcode](https://apps.apple.com/us/app/xcode/id497799835?mt=12) from appstore) and install.
  
4. Install **Anaconda** for Apple silicon
  

```
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.sh
sh Miniconda3-latest-MacOSX-arm64.sh
```

## Check

check python version

```
python3 --version
```

Check pip version

```
python3 -m pip --version
```

## Install pytorch-nightly

```
conda install pytorch torchvision torchaudio -c pytorch-nightly
```

## pip

```
pip3 install --pre torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/nightly/cpu
```

## Clone the repositories Comfyui & ComfyUI-Manager

```
git clone https://github.com/comfyanonymous/ComfyUI
cd ComfyUI/custom_nodes
git clone https://github.com/ltdrdata/ComfyUI-Manager
cd ../
```

## Create and activate a virtual environment

Note: You should be in comfyui directory in terminal

```
python3 -m venv venv
source venv/bin/activate
```

## Install the required packages

```
python -m pip install -r requirements.txt
python -m pip install -r custom_nodes/ComfyUI-Manager/requirements.txt
```

## Install PyTorch with Mac M1 support (using Conda and pip3)

```
conda install pytorch torchvision torchaudio -c pytorch-nightly
pip3 install --pre torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/nightly/cpu
```

## Verify MPS device availability

(This is not part of the script; it's just a Python snippet to verify the MPS device)

```
python
```

```

>>> import torch
>>> if torch.backends.mps.is_available():
    mps_device = torch.device("mps")
    x = torch.ones(1, device=mps_device)
    print (x)
else:
    print ("MPS device not found.")
```

The output should show:

```
tensor([1.], device='mps:0')
```

Exit Python snippet

```
>>> exit()
```

## Lauch comfyui

```
PYTORCH_MPS_HIGH_WATERMARK_RATIO=0.0 python3 main.py --force-fp16
```
