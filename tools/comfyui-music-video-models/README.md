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

## Preferred one-command setup

From the ComfyUI root, run:

```bat
path\to\TWS-Public-Utilities\tools\comfyui-music-video-models\setup-music-video-workflow.bat
```

This command:

1. installs or verifies the required models,
2. fetches the current canonical `GeekatplayStudio/ComfyUI-Music-to-Video` flagship workflow,
3. preserves an untouched upstream copy,
4. creates a separate local copy,
5. applies known legacy `control` to `convrot` filename substitutions only when they are present, and
6. validates the seven required local model files.

Generated workflows are written relative to the ComfyUI root:

```text
.\user\default\workflows\tws-music-video\music_video_ALL_IN_ONE.upstream.json
.\user\default\workflows\tws-music-video\music_video_ALL_IN_ONE.local.json
```

The source copy is overwritten from upstream on each setup run. The local copy is regenerated from that source, so the operation is repeatable and never edits the upstream workflow in place.

## Restart ComfyUI after setup

After the setup completes, fully exit and restart ComfyUI Desktop, including its backend process, before loading the generated local workflow. ComfyUI builds its available-model lists when the backend starts, so models installed while ComfyUI is already running can continue to appear as missing until the backend restarts.

The utility intentionally does not force-close or restart ComfyUI because doing so could interrupt an active generation or other unsaved/in-progress work.

## Model-installer-only command


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
- Python 3 for automatic Hugging Face CLI bootstrap
- sufficient disk space
- internet access to Hugging Face

The installer checks for the Hugging Face CLI automatically, including user-level Windows Python Scripts directories that may not be on PATH. If `hf.exe` is already installed there, it is reused without running pip again. If it is genuinely missing, the installer installs `huggingface_hub` for the current Windows user using Python/pip and updates PATH for the current installer process.

LTX 2.5 is gated. If the CLI is not already authenticated, the installer starts `hf auth login` automatically. Complete the Hugging Face login using the account that has been granted LTX 2.5 access. Credentials remain in Hugging Face's local credential storage and are never written to this repository or installer.


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
- Existing LTX destination files larger than 1 MB are treated as installed and are not downloaded again.
- Missing gated LTX downloads use the authenticated Hugging Face CLI.
- LTX downloads are staged temporarily and then moved into the exact ComfyUI model directory.
- Authentication credentials are never written to this repository or the installer.
- Permanent HTTP/authentication failures fail fast.
