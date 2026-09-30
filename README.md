# TWS Public Utilities

Small public utilities and scripts from Three-Wheeled Sloth Studio.

## Repository conventions

- Each utility lives in its own folder under `tools/`.
- Every tool must use relative paths only. Do not hard-code local machine paths.
- Every PowerShell, Python, or similar script intended for Windows use must include a companion `.bat` launcher.
- Each tool folder must include a README that states the directory from which the launcher/script must be run.
- Utilities should fail clearly and avoid destructive behavior by default.

## Agent workflow

This repository uses an Agent Academy-compatible lightweight structure:

- `AGENTS.md` - agent operating rules
- `refs/handoffs/currentHandoff.md` - current state
- `refs/handoffs/next-dev-prompt.md` - bounded next-step prompt
- `refs/planning/roadmap.md` - simple roadmap
- `refs/testing/validationCommands.yaml` - validation commands
- `refs/catalog/sourceCatalog.yaml` - compact source/function catalog

Agents should read only the files needed for the immediate task.

## Current tools

- `tools/comfyui-music-video-models/` - installs the model set required by the referenced ComfyUI music-video workflow.
