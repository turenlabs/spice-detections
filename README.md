# Spice Detections

Community-maintained detection packs for Spice.

Spice fetches `manifest.json` before each scan and falls back to its locally cached detection bundle if this repository is unavailable.

## Layout

- `manifest.json` lists available packs.
- `packs/*.json` contains hashes, IOC regexes, and suspicious artifact atoms.
- `packs/*-packages.csv` contains affected package/version rows.

Current packs focus on exact compromised package versions and high-confidence indicators across npm,
PyPI, Composer, Go modules, crates.io, and NuGet. The August 1 refresh adds exact late-July npm advisories and Joyfill 2773 npm,
late-July PyPI malware, Pepesoft NuGet tools, the Newtonsoftt.Json.Net NuGet typosquat, and an
Alibaba-targeted npm RAT cluster. Earlier July coverage includes Miasma v3 in AsyncAPI, IronWorm in
Jscrambler, the nodemon-sudo/tslint-conf runtime backdoor, the Braintree.Net payment-data skimmer,
Injective Labs SDK, and PolinRider. Earlier packs cover Miasma/Hades/Mini Shai-Hulud, TrapDoor,
Laravel Lang, node-ipc, axios, Mastra, Phantom Gyp, Solana FakeFix, and the corrected June IronWorm
package set. The September 16 refresh adds the four-package Shai-Hulud
reactivation wave published on September 7, including the shared payload hash
and exact affected versions. The September 23 refresh adds the August crates.io
build-script compromise, the Equation of Compromise npm campaign, and a
high-confidence Twilio-themed npm probe subset. These additions use exact
package versions and campaign-specific artifact indicators. A September 23
MemTensor refresh adds the compromised OpenClaw npm plugin and PyPI `MemoryOS`
releases with exact package versions and cross-platform payload hashes.
