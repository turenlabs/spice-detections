# Spice Detections

Community-maintained detection packs for Spice.

Spice fetches `manifest.json` before each scan and falls back to its embedded detections if this repository is unavailable or malformed.

## Layout

- `manifest.json` lists available packs.
- `packs/*.json` contains hashes, IOC regexes, and suspicious artifact atoms.
- `packs/*-packages.csv` contains affected package/version rows.

Current packs focus on concrete supply-chain incidents with published indicators, including Shai-Hulud/Mini Shai-Hulud, node-ipc, and axios.
