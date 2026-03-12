# Helix - Klipper Version and Firmware Repo Strategy

## Recommended Klipper Strategy for Manta M8P
Klipper does not publish classic semantic "stable releases" for most users. The practical production strategy is:

1. Start from upstream official Klipper repository `master`.
2. Validate on your exact hardware stack (Manta M8P V2.0 + CB1/CM4 + drivers).
3. Freeze a tested commit hash in this repo for reproducibility.

This gives you both compatibility and rollback safety.

## Official Repositories and Docs
- Klipper firmware/code: `https://github.com/Klipper3d/klipper`
- Klipper documentation: `https://www.klipper3d.org/`
- BTT Manta support material: `https://github.com/bigtreetech/Manta-M8P`

## Board-Specific Notes
- Use the board-specific config and pin mapping that matches Manta M8P V2.0 exactly.
- If a board option is missing in your local Klipper checkout, update to a newer upstream commit and retest.

## Windows 10/11 Clarification
- Klipper host service runs on Linux (typically CB1/CM4/Raspberry Pi OS class system).
- Windows 10/11 is fully valid for operator workstations (browser to Mainsail/Fluidd, remote tools, file management).

## Repo Linking Options
### Option A - Documented external dependency (simple)
Keep firmware external and record the validated commit hash in this repo.

### Option B - Git submodule (recommended for reproducibility)
Use a submodule under `firmware/klipper` pinned to a tested commit.

Example commands:
```bash
git submodule add https://github.com/Klipper3d/klipper firmware/klipper
git -C firmware/klipper checkout <TESTED_COMMIT>
git add .gitmodules firmware/klipper
git commit -m "Add Klipper firmware submodule pinned to tested commit"
```

## Initial Recommendation for Helix
- Use latest upstream Klipper at commissioning time.
- After machine acceptance tests, pin the exact passing commit hash.
- Record that hash in this file and in commissioning notes.
