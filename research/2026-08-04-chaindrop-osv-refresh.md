# ChainDrop and early-August 2026 malware refresh

This refresh adds high-confidence detection coverage disclosed after the detection
baseline at `2026-08-01T17:31:35Z`. The data-only packs use schema version 1 and
require no Spice scanner or release changes.

## Sources and scope

ChainDrop sources:

- StepSecurity: https://www.stepsecurity.io/blog/chaindrop-npm-worm
- Aikido: https://www.aikido.dev/blog/keyv-and-friends-compromised-in-npm-supply-chain-attack
- Socket: https://socket.dev/blog/popular-npm-packages-in-the-keyv-and-cacheable-namespaces-compromised-in-active-supply-chain
- Wiz affected-package source: https://raw.githubusercontent.com/wiz-sec-public/wiz-research-iocs/main/reports/keyv-packages.csv
- Wiz file metadata: https://github.com/wiz-sec-public/wiz-research-iocs/blob/main/reports/keyv-packages.csv

The Wiz snapshot used here contains 443 data rows. Its GitHub blob SHA is
`90d48f5b27a74ae3ae41bcf80159ab856f2c306d`. StepSecurity reports a different
feed snapshot of 444 packages and 2,212 versions. This refresh preserves the
443 exact Wiz rows and does not infer the larger count.

The Wiz source header is `Package,Malicious Versions`. The detection CSV adds
an explicit `Ecosystem` column with `npm` on every row so package matching stays
ecosystem-scoped in Spice.

## ChainDrop coverage

The full-carrier package rows in the source include:

- `keyv` 6.0.0
- `flat-cache` 6.1.24
- `file-entry-cache` 11.1.6
- `cacheable-request` 13.0.20
- `cacheable` 2.5.1
- `cache-manager` 7.2.10
- `@cacheable/memory` 2.2.1
- `@cacheable/net` 2.1.1
- `@cacheable/node-cache` 3.1.2
- `@cacheable/utils` 2.5.1
- `ecto` 5.0.1

The pack also preserves all other exact rows in the Wiz snapshot, including
the `@arv-bedrock`, `@hubsync`, `@thiennq`, `@onereach`, `@or-sdk`, `@ornikar`,
`@servicetitan`, `@qlik`, `@nebula.js`, `@umacloud`, and unscoped package rows.

Payload SHA-256 values:

- `54dc7ea54a1317cca0e890a2770630cf7fa6c97813e0cb9d2caa93012b350668` - npm `setup.mjs` loader
- `fd3ca4007b225fdf8de7af4345a19179d5efa8c4bb9205f88cda806e5684b1eb` - community `setup.mjs` loader
- `9fc2570b7cef51c1b8df116d144d11ff4096357be7d2c4c6367cfc2509cf1bcc` - `Math_Symbol.js` or `math_init.js`

The pack uses the exact `npm-cache.com:443/router` route, Ethereum resolver
contract `0xE1f2395ee43e45A1556EC6438a88c31B83493103`, and selector `0x53ed5143`.
`setup.mjs`, `Math_Symbol.js`, and `math_init.js` are suspicious filenames so
their exact published payload hashes are scanned inside package artifacts.
`setup.mjs` is present only to make the two exact setup payload hashes reachable;
it is not a standalone IOC. Generic Bun, cloud metadata, GitHub persistence, and
reused Shai-Hulud strings are only used inside a composite where they are anchored
by the ChainDrop route; they are not standalone ChainDrop IOCs.

## Exact OSV package coverage

### npm

| OSV record | Package and exact version | SHA-256 | Source |
|---|---|---|---|
| MAL-2026-11430 | `list-issue-predecessor-dependencies-block` 99.0.0 | `0f74d699bfc5fcf83c6f2864f93ecd41d3d9f8613f45f6bfb3b6dd5eeb7a880e` | https://api.osv.dev/v1/vulns/MAL-2026-11430 |
| MAL-2026-11484 | `simple-date-formatter-util-1` 1.0.0 | `8fbc767ae4319a00160dc56f05c82dc051f9fd8d66674de81372935f529ed241` | https://api.osv.dev/v1/vulns/MAL-2026-11484 |
| MAL-2026-11498 | `@custombots/custombot` 1.0.0 | `07c87d7c1e7e788959af6de895c76293fd0922dd1a422da325962de7f8d3d19a` | https://api.osv.dev/v1/vulns/MAL-2026-11498 |
| MAL-2026-11501 | `simple-date-formatter-util-5` 1.0.0 | `0eb3042c51ca3c377dd9f4e814a53f4901a805271896f9bfd1619891be4bff5c` | https://api.osv.dev/v1/vulns/MAL-2026-11501 |
| MAL-2026-11502 | `simple-date-formatter-new-1` 1.0.0 | `037638085662ef2cec04655349a528b60480aa642606d96eba158e62161b3a51` | https://api.osv.dev/v1/vulns/MAL-2026-11502 |
| MAL-2026-11515 | `@zzzgenesis00/bip39-generator` 3.1.2 | `5cd50fa982c125844b76d3527f878bd6a171b497e86fd7cbcccfc56d22000da4` | https://api.osv.dev/v1/vulns/MAL-2026-11515 |
| MAL-2026-11518 | `exnesss` 0.0.1 | `9547bba265ba397413387555d1bf269b1072ec4aba26409f22c72654c110cbf1` | https://api.osv.dev/v1/vulns/MAL-2026-11518 |

### PyPI

| OSV record | Package and exact version | SHA-256 | Source |
|---|---|---|---|
| MAL-2026-11428 | `wacve-utils` 1.0.7 | `24d4ada91d3bb23e5113caff835c4f285579f06da6ebe4153a456fb2627070f7` and `de96a68d25555c9ee1792a22b84307ba3bc68d1e012bd841454dc775986260cb` | https://api.osv.dev/v1/vulns/MAL-2026-11428; https://bad-packages.kam193.eu/pypi/package/wacve-utils |
| MAL-2026-11429 | `trongriden` 0.0.1 | `dfb2a16e0023940b622e66acf21c1597d4127d94fb730610f509960e49754c3f` | https://api.osv.dev/v1/vulns/MAL-2026-11429; https://bad-packages.kam193.eu/pypi/package/trongriden |
| MAL-2026-11503 | `instalogin1234` 0.0.1 | `f6ed64b38b3e872668e1d36a02c53136da1ab70ec9dacd2ac3b7d38c31794ebe` | https://api.osv.dev/v1/vulns/MAL-2026-11503; https://bad-packages.kam193.eu/pypi/package/instalogin1234 |
| MAL-2026-11516 | `coldcard-helpers` 1.4.2 | `127a096109f7b5b2bbedf7f6a9fc2e7baa706e93704ebd52615e744a9838fbc3` | https://api.osv.dev/v1/vulns/MAL-2026-11516; https://bad-packages.kam193.eu/pypi/package/coldcard-helpers |
| MAL-2026-11520 | `psbt-utils` 1.0.0 | `5424e50d87f8c14eb7d0d37d4c98e86a1c06fb3613a66fd9af2e9ab6fd611938` | https://api.osv.dev/v1/vulns/MAL-2026-11520; https://bad-packages.kam193.eu/pypi/package/psbt-utils |
| MAL-2026-11521 | `psbt-helpers` 1.0.0 | `394dea9d587ac1affba13c45ecfc28f5d005b2cb5f8b665dcf4591b60085a8ae` | https://api.osv.dev/v1/vulns/MAL-2026-11521; https://bad-packages.kam193.eu/pypi/package/psbt-helpers |

Exact PyPI IOCs are the wacve gist URL, the four trongriden domains, the
instalogin Discord channel URL, and the shared psbt firmware URL. The
`launchdarkly-ai-server-sdk` 1.0.1 and 1.9.9 candidate is deferred because OSV
classifies it as `PROBABLY_PENTEST` and provides no campaign-specific IOC.

## Exclusions

Records `MAL-2026-11506` through `MAL-2026-11514`, plus `MAL-2026-11483`,
`MAL-2026-11500`, `MAL-2026-11504`, `MAL-2026-11505`, and `MAL-2026-11517`,
have no concrete affected version and are not represented in package CSVs.
No generic package names, guessed versions, or broad behavior-only IOCs were added.
