# Spice Detections

Community-maintained detection packs for Spice.

Spice fetches `manifest.json` before each scan and falls back to its locally cached detection bundle if this repository is unavailable.

## Layout

- `manifest.json` lists available packs.
- `packs/*.json` contains hashes, IOC regexes, and suspicious artifact atoms.
- `packs/*-packages.csv` contains affected package/version rows.

Current packs focus on concrete supply-chain incidents with published indicators, including Mastra/easy-day-js, Miasma Phantom Gyp, Miasma/Hades Mini Shai-Hulud (npm and PyPI), TrapDoor, Laravel Lang, Shai-Hulud/Mini Shai-Hulud, node-ipc, and axios.
