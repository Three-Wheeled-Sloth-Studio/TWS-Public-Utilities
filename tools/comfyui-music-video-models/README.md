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

Do not run it from this repository folder unless this repository itself has been placed inside your ComfyUI root. The script intentionally uses relative paths and writes to:

```text
.\models\diffusion_models
.\models\text_encoders
.\models\vae
```

## How to run

From the intended ComfyUI root:

```bat
path\to\TWS-Public-Utilities\tools\comfyui-music-video-models\install-music-video-models.bat
```

The launcher preserves your current working directory and invokes the PowerShell script from the repository path.

To display help without downloading:

```bat
path\to\TWS-Public-Utilities\tools\comfyui-music-video-models\install-music-video-models.bat --help
```

## Prerequisites

- Windows
- PowerShell 5.1 or later
- `curl.exe`
- sufficient disk space
- internet access to Hugging Face

## Models installed

### Z-Image

`models/diffusion_models/`
- `z_image_turbo_bf16.safetensors`

`models/text_encoders/`
- `qwen_3_4b.safetensors`

`models/vae/`
- `ae.safetensors`

### LTX 2.5

`models/diffusion_models/`
- `ltx-2.5-22b-distilled-transformer-comfy-int8-convrot.safetensors`

`models/text_encoders/`
- `gemma4-12b-with-proj-ltx-2.5-comfy-int8-convrot.safetensors`

`models/vae/`
- `ltx-2.5-video-vae-bf16.safetensors`
- `ltx-2.5-audio-vae-bf16.safetensors`

## Workflow note

If the workflow still references filenames ending in `comfy-int8-control.safetensors`, select the installed `comfy-int8-convrot.safetensors` variants in those loader nodes after restarting ComfyUI.

The workflow's remaining issue may simply be the required audio input.

## Download behavior

- Existing files larger than 1 MB are skipped.
- `curl.exe --continue-at -` is used so interrupted downloads can resume.
- A failed download stops the script with an error.
