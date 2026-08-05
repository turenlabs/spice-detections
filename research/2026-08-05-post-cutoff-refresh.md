# Post-cutoff August 2026 detection refresh

This refresh adds high-confidence package coverage disclosed after the detection
baseline at `2026-08-04T20:06:40Z`. It extends the existing schema-v1 August npm
and PyPI packs. No Spice scanner, release, or Homebrew changes are required.

The manifest update timestamp for this refresh is `2026-08-05T19:12:01Z`.
The research snapshot was `2026-08-05T18:34:27Z`.

## Sources

OSV records:

- https://osv.dev/vulnerability/MAL-2026-12080
- https://osv.dev/vulnerability/MAL-2026-12081
- https://osv.dev/vulnerability/MAL-2026-12082
- https://osv.dev/vulnerability/MAL-2026-12083
- https://osv.dev/vulnerability/MAL-2026-12502
- https://osv.dev/vulnerability/MAL-2026-12503
- https://osv.dev/vulnerability/MAL-2026-13355
- https://osv.dev/vulnerability/MAL-2026-13356
- https://osv.dev/vulnerability/MAL-2026-13357
- https://osv.dev/vulnerability/MAL-2026-13358
- https://osv.dev/vulnerability/MAL-2026-13359
- https://osv.dev/vulnerability/MAL-2026-13360
- https://osv.dev/vulnerability/MAL-2026-13361
- https://osv.dev/vulnerability/MAL-2026-13362

Additional campaign index:

- https://bad-packages.kam193.eu/pypi/package/bip39-py

## Exact npm coverage

The package rows are in `packs/npm-malware-2026-08-packages.csv` and the
origin hashes are in `packs/npm-malware-2026-08.json`.

| OSV | Package and exact version | Origin SHA-256 | Additional evidence |
|---|---|---|---|
| MAL-2026-13355 | `@astralcore/sl-aura@1.0.6` | `91ae2c72e5e03d23f3f5704859e8c92b9ce6c565c6d14d744d4382b980a0d233` | `config.env` SHA-256 `b2cd6d977cb86bab8e263e4b870be3070b40e8e55f4ee93beef65995d0140d8e`; MongoDB host `unity-free.pc6vkv.w.mongodb.net` |
| MAL-2026-13356 | `chai-foundry@7.0.2` | `94e40493af5310c6ee769911bff65e55538911ae3f286fba2a3474f9f8a38940` | `lib/config.js` SHA-256 `8397643af68793d57aec3637e79324e9183d6f1168009cd0676432515e88c515` |
| MAL-2026-13356 | `chai-foundry@7.0.3` | `47d799affc9421116994671c24da24cabadfb12a42d5b12ac54b2fce2aa1afe2` | Same obfuscated import-time loader campaign |
| MAL-2026-13357 | `app-hsu-layer@2.1.6` | `ccec10b777948fb3fcd849ce3741e0cd78bf46c23f037b8ab23ff6835acb6400` | C2 `95.216.118.146:3001/api/v1`, `/api/scan-patterns`, `/api/ssh-key` |
| MAL-2026-13357 | `app-hsu-layer@2.1.7` | `ad1ccd2bfbe4abd87e980067608328d6c0a6cb3d1145d8d8ff8d72a22667f00d` | Same SSH-key backdoor campaign |
| MAL-2026-13358 | `app-kst-engine@2.1.6` | `08cfc426d2f4b29bba2b81f2eb56eeee32ab114338a51fae5eeced2571e6b2d9` | `index.js` SHA-256 `d986a2e0a9eb3fc3781e166ff6b700e0d38249a6c9649982243c3754671f42d9`; C2 `170.205.31.203:3000/api/v1` |
| MAL-2026-13359 | `test-dev-config@0.1.0` | `44b80ff2bcf35e5c92c1c8a551b943d334f94793d693ce846707986613db8108` | `src/config.js` SHA-256 `1e355654c8db0fd5df4b9113585677568b5803765a132e17c7f974f19282f7b1`; endpoint `45.95.186.237:8000` |
| MAL-2026-13360 | `uzair-rajput-new@1.0.1` | `70070ac11c08aa4d23d214d9539b96f97c6bd6eaa56bb6561160d02bd6d52632` | `dist/index.cjs` SHA-256 `3f564f0df5a16009ca450256e3e5e0457dcd9202e10f79567b7b2aa354d888b2`; AES-256-CBC payload and dynamic `new Function` execution |

The npm pack uses exact infrastructure IOCs for the MongoDB host, the two
IP-and-path C2 endpoints, and the test-dev-config endpoint plus its encoded
address. The sl-aura file-management commands are composite-only with the
MongoDB host. The uzair-rajput-new AES/cipher/dynamic-execution signals are
composite-only. Chai-foundry has no stable published endpoint, so coverage is
the exact package rows and origin hashes.

## Exact PyPI coverage

The package rows are in `packs/pypi-malware-2026-08-packages.csv` and the
origin or archive hashes are in `packs/pypi-malware-2026-08.json`.

| OSV | Package and exact version | Origin SHA-256 | Artifact or evidence SHA-256 |
|---|---|---|---|
| MAL-2026-12080 | `bip39-py@1.0.6` | `c188f84ee0ad8238ed89a94673968e9f17c44d91d25dfe8012efd39e01705081` | Shared C2 `40f955f39128bd79-178-249-214-24.serveousercontent.com` |
| MAL-2026-12081 | `bitcoinlib-py@0.9.0` | `32582a69a108bf3ab34d8bd16122918dd29a56bff6f68a771b77c6c946bf9308` | Same crypto-stealer campaign |
| MAL-2026-12082 | `crypto-trading-toolkit@3.2.0` | `20c37efbefbfb1922a205d954cdb5666103fd3e343a67e89dc19694ad5b64ef0` | Same crypto-stealer campaign |
| MAL-2026-12083 | `crypto-wallet-sdk@1.8.3` | `d0bf047680c46c2f4c37c8a7b77e9d993acb05ef4925c660e0c5cccf95be581f` | Same crypto-stealer campaign |
| MAL-2026-13362 | `mnemonic-py@0.21` | `6599d6208d71e0e809661e86bf5641e6e7b871cd6f01a54abf22215b8a88ef11` | Same crypto-stealer campaign |
| MAL-2026-13361 | `defi-sdk-py@2.5.1` | `b292686db581afeaaa7d53e2281a90d7d470fc71ab9e7d6156c49e2e99a44a30` | Same crypto-stealer campaign |
| MAL-2026-12502 | `gcli-control@0.12.2` | `406ed2a02ad0507ec71fce2e2d287f628c7284a2476dce055727d963136d0a50` | Wheel `abb622dbc79151f0f7093234cd9babffb0403ee1825ff3b8fc8a56e9f5872cf4`; rendezvous `599ac3c39189fcc26e5a` |
| MAL-2026-12502 | `gcli-control@0.5.0` | `f94a308a9c8d68b87a9613385c1c818128ddfc01b29aa941047f209e601b4e46` | Same RAT campaign |
| MAL-2026-12502 | `gcli-control@0.12.4` | `b8bd4de0b73d7df676127ce8c632117fc7ea8d008bf941fb7d385f67a84f8d67` | Same RAT campaign |
| MAL-2026-12502 | `gcli-control@0.11.1` | `d99ccd85346f7a31a3eaffef748f106c1de645446ebd3e73a444fd340384ac3f` | Same RAT campaign |
| MAL-2026-12503 | `numpyp@0.7.7` | `971ce16c4710dfddc439c30ec2fc190001171f79fcd66f718ad358a43ecdf876` | Tarball `f00921577a6a04497c5a312090b5cf6b1899c8c2d61b64e5516bbd6d574fd7c6`; `numpyp/__init__.py` `abe7cee2214f53cea8c4103636bca26f85d96be57cf5eae095ce2e40947cb80b`; endpoint `fantasize-handcraft-pavement.ngrok-free.dev` |

The PyPI pack uses the exact crypto-stealer host, numpyp endpoint, and gcli
rendezvous identifier. `api.npoint.io`, `__BYPASS__`, and the gcli rendezvous
identifier are required together by the gcli composite; `BY:` is intentionally
not a standalone IOC.

## Hash and IOC boundaries

The six source/member evidence hashes are retained here but are not in
`knownSha256`: `config.env`, `lib/config.js`, `index.js`, `src/config.js`,
`dist/index.cjs`, and `numpyp/__init__.py` are not all hash candidates under
the current scanner. The two whole-archive artifact hashes for the gcli wheel
and numpyp source archive are active hash rules.

No generic browser paths, SSH paths, credential names, owner numbers, bare API
paths, port `8008`, `BY:`, or standalone AES/XOR/`new Function` indicators were
added. No package versions were inferred from versionless advisories. No
additional high-confidence rows were found for Crates.io, NuGet, Go, or
Composer.

ChainDrop and the earlier August npm/PyPI rows were already covered and were
not duplicated or changed.
