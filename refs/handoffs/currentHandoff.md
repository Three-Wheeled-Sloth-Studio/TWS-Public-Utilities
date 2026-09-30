# Current Handoff

## Current state

Repository seeded with the baseline public-utility structure.

Initial utility:
- ComfyUI Music Video Model Installer

## Conventions established

- tools live under `tools/`
- relative paths only
- Windows launchers use `.bat`
- each tool has a local README with working-directory instructions
- bounded agent context via `AGENTS.md`, catalog, and handoffs

## Validation

For the initial utility, syntax/behavior should be validated on Windows PowerShell 5.1+ with `curl.exe` available.

## Open items

- Confirm exact upstream LTX 2.5 filenames if the referenced workflow changes.
- Add new utilities as needed without coupling them to this tool.
