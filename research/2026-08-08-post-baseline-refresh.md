# Post-baseline August 2026 detection refresh

This data-only refresh extends the existing schema-v1 August npm and PyPI
packs. The prior manifest baseline was `2026-08-05T19:12:01Z`; this refresh was
prepared on `2026-08-08T13:42:44Z`.

No Spice scanner, application release, or Homebrew changes are required. The
scanner already loads exact package rows, package archive SHA-1/SHA-256 values,
regex IOCs, and multi-signal composites from the remote packs.

## Sources

OSV records used for the npm additions:

- https://api.osv.dev/v1/vulns/MAL-2026-13374
- https://api.osv.dev/v1/vulns/MAL-2026-13375
- https://api.osv.dev/v1/vulns/MAL-2026-13376
- https://api.osv.dev/v1/vulns/MAL-2026-13377
- https://api.osv.dev/v1/vulns/MAL-2026-13378
- https://api.osv.dev/v1/vulns/MAL-2026-13392
- https://api.osv.dev/v1/vulns/MAL-2026-13393
- https://api.osv.dev/v1/vulns/MAL-2026-13399
- https://api.osv.dev/v1/vulns/MAL-2026-13400
- https://api.osv.dev/v1/vulns/MAL-2026-13401
- https://api.osv.dev/v1/vulns/MAL-2026-13405
- https://api.osv.dev/v1/vulns/MAL-2026-13407
- https://api.osv.dev/v1/vulns/MAL-2026-13409
- https://api.osv.dev/v1/vulns/MAL-2026-13410
- https://api.osv.dev/v1/vulns/MAL-2026-13411
- https://api.osv.dev/v1/vulns/MAL-2026-13419
- https://api.osv.dev/v1/vulns/MAL-2026-13423
- https://api.osv.dev/v1/vulns/MAL-2026-13424
- https://api.osv.dev/v1/vulns/MAL-2026-13425
- https://api.osv.dev/v1/vulns/MAL-2026-13427
- https://api.osv.dev/v1/vulns/MAL-2026-13447
- https://api.osv.dev/v1/vulns/MAL-2026-13450
- https://api.osv.dev/v1/vulns/MAL-2026-13452
- https://api.osv.dev/v1/vulns/MAL-2026-13457
- https://api.osv.dev/v1/vulns/MAL-2026-13459
- https://api.osv.dev/v1/vulns/MAL-2026-13461
- https://api.osv.dev/v1/vulns/MAL-2026-13465
- https://api.osv.dev/v1/vulns/MAL-2026-13466
- https://api.osv.dev/v1/vulns/MAL-2026-13608
- https://api.osv.dev/v1/vulns/MAL-2026-13609
- https://api.osv.dev/v1/vulns/MAL-2026-13610
- https://api.osv.dev/v1/vulns/MAL-2026-13611
- https://api.osv.dev/v1/vulns/MAL-2026-13612
- https://api.osv.dev/v1/vulns/MAL-2026-13613
- https://api.osv.dev/v1/vulns/MAL-2026-13614
- https://api.osv.dev/v1/vulns/MAL-2026-13615
- https://api.osv.dev/v1/vulns/MAL-2026-13616
- https://api.osv.dev/v1/vulns/MAL-2026-13617
- https://api.osv.dev/v1/vulns/MAL-2026-13618
- https://api.osv.dev/v1/vulns/MAL-2026-13620
- https://api.osv.dev/v1/vulns/MAL-2026-13621
- https://api.osv.dev/v1/vulns/MAL-2026-13622
- https://api.osv.dev/v1/vulns/MAL-2026-13623
- https://api.osv.dev/v1/vulns/MAL-2026-13624
- https://api.osv.dev/v1/vulns/MAL-2026-13625
- https://api.osv.dev/v1/vulns/MAL-2026-13626
- https://api.osv.dev/v1/vulns/MAL-2026-13627
- https://api.osv.dev/v1/vulns/MAL-2026-13628
- https://api.osv.dev/v1/vulns/MAL-2026-13629
- https://api.osv.dev/v1/vulns/MAL-2026-13630
- https://api.osv.dev/v1/vulns/MAL-2026-13631
- https://api.osv.dev/v1/vulns/MAL-2026-13632
- https://api.osv.dev/v1/vulns/MAL-2026-13633
- https://api.osv.dev/v1/vulns/MAL-2026-13634 through https://api.osv.dev/v1/vulns/MAL-2026-13663
- https://api.osv.dev/v1/vulns/MAL-2026-13664

OSV records used for the PyPI additions:

- https://api.osv.dev/v1/vulns/MAL-2026-13380
- https://api.osv.dev/v1/vulns/MAL-2026-13486
- https://api.osv.dev/v1/vulns/MAL-2026-13487
- https://api.osv.dev/v1/vulns/MAL-2026-13488
- https://api.osv.dev/v1/vulns/MAL-2026-13489
- https://api.osv.dev/v1/vulns/MAL-2026-13490
- https://api.osv.dev/v1/vulns/MAL-2026-13606
- https://api.osv.dev/v1/vulns/MAL-2026-13607
- https://bad-packages.kam193.eu/pypi/package/fastapii
- https://bad-packages.kam193.eu/pypi/package/flasq
- https://bad-packages.kam193.eu/pypi/package/idnna
- https://bad-packages.kam193.eu/pypi/package/pydanticc
- https://bad-packages.kam193.eu/pypi/package/fast-hashes
- https://bad-packages.kam193.eu/pypi/package/speed-hashes

## Added coverage

`npm-malware-2026-08` now includes exact package rows and package archive
SHA-1 values for the 13374-13378 loader/backdoor cluster, golaaa,
wallet-monitor-snap, agenthub-multiagent-mcp, agenttunnels, helmet-pro,
vitest-preview-pro-all, @0l00000l/auth, the three @addai packages,
@holocronlab/botruntime-runtime, fetchrtds, tailwindcss-hide-scrollbar,
typst-resume-cli, @leejungkiin/awkit, the gpt-terminal/wormgpt RATs,
move-bcs-codec, opencode-optimised-toolings, shadowx-fca, vite-vue-path-map,
the RedShell streak package family, Prisma/Hardhat packages, the Catbox
dropper pair, localization-fixer, modern-localization, titan-exchange-
shared-permissions, the verified 13610-13627 package wave, and all 30
sme-rko-finance-front-operations packages at version 35.8.1.

The npm pack adds exact infrastructure indicators for those campaigns,
including the app-api-sdk collector, Claude/agent relays, JSONBin bins,
BotRuntime, Flasq-adjacent npm infrastructure, Catbox, RedShell, Prisma,
gpt-terminal/wormgpt, and the sme-rko worker and DNS fallback hosts. Generic
install hooks, filenames, credential names, and standalone `new Function`,
AES, XOR, or local-port indicators are not added. RedShell, JSONBin, Catbox,
sme-rko, and Ethereum RPC behavior use composites where a single string could
be too broad.

`pypi-malware-2026-08` now includes exact artifact hashes and rows for:

- `uncrypt==0.1.1`
- `fastapii==0.1.1`
- `flasq==0.1.2`
- `idnna==0.1.1`
- `pydanticc==0.3.0`
- `fast-hashes==0.1.0`
- `speed-hashes==0.1.0`
- `cdktn-provider-azurerm==17.0.0`

The Flasq-family rules use only the verified GitHub release URL and IP
`193.70.34.101`, with an install-time dropper composite. The OSV record lists
additional fastapii affected versions, but the verified archive hash belongs
to `fastapii-0.1.1.tar.gz`; no other fastapii version was added.

## Explicit exclusions

ChainDrop and the earlier August npm/PyPI rows already covered by the current
packs were not duplicated. Records published before the prior manifest
timestamp but imported or modified later were not treated as new coverage.
Generic/no-behavior records, `PROBABLY_PENTEST` records, advertised remote
shell products, unverified package versions, and source-record/blob hashes were
excluded. No additional scanner, release, Formula, or Cask changes are part of
this refresh.
