# ComfyUI Music Video Model Installer

Downloads the model set used by the ComfyUI music-video workflow discussed for Z-Image plus LTX 2.5.

## Required working directory

Run this tool from the ComfyUI root directory that contains the `models` folder.

Example shape:

```text
ComfyUI/
  models/
    diffusion_models/
    text_encoders/
    vae/
```

The script uses the current ComfyUI root and writes model files under `.\models\`.

## How to run

From the intended ComfyUI root:

```bat
path\to\TWS-Public-Utilities\tools\comfyui-music-video-models\install-music-video-models.bat
```

To display help without downloading:

```bat
path\to\TWS-Public-Utilities\tools\comfyui-music-video-models\install-music-video-models.bat --help
```

## Prerequisites

- Windows
- PowerShell 5.1 or later
- `curl.exe`
- Hugging Face CLI command `hf` for gated LTX 2.5 models
- sufficient disk space
- internet access to Hugging Face

Install the Hugging Face CLI if needed:

```powershell
pip install -U huggingface_hub
```

LTX 2.5 is gated. After your Hugging Face account has been granted model access, authenticate this machine once:

```powershell
hf auth login
```

Current Hugging Face CLI versions support browser/device login. The credential is stored by Hugging Face locally; this repository and installer do not store your token.

You can verify the active account with:

```powershell
hf auth whoami
```

## Models installed

Z-Image:
- `models/diffusion_models/z_image_turbo_bf16.safetensors`
- `models/text_encoders/qwen_3_4b.safetensors`
- `models/vae/ae.safetensors`

LTX 2.5:
- `models/diffusion_models/ltx-2.5-22b-distilled-transformer-comfy-int8-convrot.safetensors`
- `models/text_encoders/gemma4-12b-with-proj-ltx-2.5-comfy-int8-convrot.safetensors`
- `models/vae/ltx-2.5-video-vae-bf16.safetensors`
- `models/vae/ltx-2.5-audio-vae-bf16.safetensors`

## Download behavior

- Public Z-Image downloads use curl with resume and transient-network retry support.
- Existing public files are remotely checked so partial files can resume.
- Gated LTX downloads use the authenticated Hugging Face CLI.
- LTX downloads are staged temporarily and then moved into the exact ComfyUI model directory.
- Authentication credentials are never written to this repository or the installer.
- Permanent HTTP/authentication failures fail fast.
