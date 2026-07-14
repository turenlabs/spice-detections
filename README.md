# Spice Detections

Community-maintained detection packs for Spice.

Spice fetches `manifest.json` before each scan and falls back to its locally cached detection bundle if this repository is unavailable.

## Layout

- `manifest.json` lists available packs.
- `packs/*.json` contains hashes, IOC regexes, and suspicious artifact atoms.
- `packs/*-packages.csv` contains affected package/version rows.

Current packs focus on exact compromised package versions and high-confidence indicators across npm,
PyPI, Composer, Go modules, crates.io, and NuGet. Recent coverage includes Miasma v3 in AsyncAPI,
IronWorm in Jscrambler, the nodemon-sudo/tslint-conf runtime backdoor, the Braintree.Net payment-data
skimmer, Injective Labs SDK, PolinRider, and exact advisory cohorts published during July 9-14 2026.
Earlier packs cover Miasma/Hades/Mini Shai-Hulud, TrapDoor, Laravel Lang, node-ipc, axios, Mastra,
Phantom Gyp, Solana FakeFix, and the corrected June IronWorm package set.
