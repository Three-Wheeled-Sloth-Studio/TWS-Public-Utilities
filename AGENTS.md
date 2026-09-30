# AGENTS.md

## Scope

This repository contains small public utilities. Keep each utility independent, documented, and easy to run.

## Operating rules

1. Work only on the files relevant to the requested utility.
2. Prefer small, atomic files over large multi-purpose scripts.
3. Use relative paths only. Never commit machine-specific absolute paths.
4. Every executable script intended for Windows must have a companion `.bat` launcher.
5. Every tool must have a README that states:
   - purpose
   - prerequisites
   - required working directory
   - exact run command
   - files/directories it reads or writes
6. Scripts must fail with clear messages when run from the wrong directory.
7. Avoid destructive operations unless explicitly requested and clearly confirmed.
8. Keep the source catalog current when files/functions are added or moved.
9. Update `refs/handoffs/currentHandoff.md` and `refs/handoffs/next-dev-prompt.md` when a meaningful slice is completed.
10. Run only the validation relevant to the files changed.

## Bounded re-entry

Before changing a utility, read:
- this file
- that utility's README
- the relevant entries in `refs/catalog/sourceCatalog.yaml`
- the current handoff if needed

Do not reread the whole repository.
