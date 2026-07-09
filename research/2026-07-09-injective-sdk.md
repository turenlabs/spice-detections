# Injective Labs npm SDK compromise - July 2026

Sources:

- BleepingComputer: Injective SDK on npm infected with cryptocurrency wallet stealer
  (https://www.bleepingcomputer.com/news/security/injective-sdk-on-npm-infected-with-cryptocurrency-wallet-stealer/)
- Socket: Compromised Injective SDK npm package
  (https://socket.dev/blog/compromised-injective-sdk-npm-package)
- StepSecurity: Injective npm supply chain attack, 18 packages backdoored to steal crypto wallet keys
  (https://www.stepsecurity.io/blog/injective-npm-supply-chain-attack-18-packages-backdoored-to-steal-crypto-wallet-keys)
- OX Security: @injectivelabs npm package hijacked, impacting 87 dependent packages
  (https://www.ox.security/blog/injectivelabs-npm-package-hijacked-impacting-87-dependent-packages/)
- npm registry metadata and tarballs (independent verification, see below)

Pack: `injective-2026-07`

## Summary

An attacker compromised a legitimate contributor's GitHub account (`thomasRalee`) on the
injective-ts repository and published version `1.20.21` of `@injectivelabs/sdk-ts` plus 17
associated `@injectivelabs` packages (18 total). The payload hooks `PrivateKey.fromMnemonic()` and
`PrivateKey.fromHex()` via an injected `trackKeyDerivation()` function disguised as SDK telemetry.
Captured mnemonics and private keys are queued as `${method}:${value}:${Date.now()}`, base64-encoded,
and exfiltrated in the `X-Request-Id` header of an empty-body HTTP POST with
`Content-Type: application/grpc-web+proto` to `testnet.archival.chain.grpc-web.injective.network`,
a hostname styled after legitimate Injective gRPC-web infrastructure. The hostname is built at
runtime from a character-code array; it never appears as a literal string in the shipped files.

Timeline (verified against npm registry `time` metadata): malicious versions published
2026-07-08 20:59-21:00 UTC, clean `1.20.23` published 21:47-21:49 UTC the same day, all 18
malicious versions deprecated with "SECURITY: version 1.20.21 is compromised. Do not install."
Socket and BleepingComputer describe the incident as June 8; the registry timestamps confirm
July 8 (StepSecurity's UTC timeline). The malicious version was downloaded ~310 times.

## Independent verification

- Registry sweep of all 118 `@injectivelabs` scope packages found exactly 18 versions carrying
  the SECURITY deprecation, matching the vendor lists. Tarball SHA-1s in the pack come from
  registry `dist.shasum` for those 18 versions.
- Downloaded `sdk-ts` `1.20.21` and `1.20.23` tarballs. The two published SHA-256 hashes for
  `dist/cjs/accounts-Cy0p4lLW.cjs` and `dist/esm/accounts-jQ1GSgaW.js` reproduce exactly.
- The char-code-array IOC regex matches both malicious dist files and decodes to the exfil
  hostname. The clean `1.20.23` build contains none of: the hostname, `trackKeyDerivation`,
  `key-derivation-telemetry`, or the malicious chunk filenames (its chunk is
  `accounts-3rypojw1.js`).
- Composite IOC calibration: both malicious files match 6/6 signals; the worst clean-SDK file
  matches 1/6 (`fromMnemonic`/`fromHex`, expected in a wallet SDK). `minMatches: 4` leaves wide
  margin in both directions.

## Added coverage

- Exact npm package/version rows for all 18 packages at `= 1.20.21`.
- Known SHA-256 hashes for the two malicious dist chunks; known SHA-1 hashes for all 18 npm
  tarballs (matches raw tarballs and npm cache content blobs).
- String IOCs: literal exfil hostname, char-code-obfuscated hostname prefix
  ("testnet.archival"), `trackKeyDerivation`, `key-derivation-telemetry`, malicious hashed chunk
  filenames, and references to any of the 18 package names within 24 characters of `1.20.21`.
- Composite IOC for the exfil beacon shape: campaign marker, gRPC-web content-type disguise,
  `X-Request-Id` header channel, base64 encoding, wallet key-derivation context, and the queued
  payload format.

## Scan notes

- The exfil hostname sits under the legitimate `injective.network` domain. Bare
  `injective.network` or `grpc-web` references are NOT flagged; only the campaign-specific
  `testnet.archival.chain.grpc-web` host, which does not appear anywhere in the clean SDK.
- Package names in this campaign are legitimate packages; only version `1.20.21` is malicious.
  Name-based IOCs therefore always require the version string nearby, unlike packs for
  purely-malicious package names (for example TrapDoor).
- Git-side IOCs (attacker commits `01219285`, `fd105db9`, `5486f13e`, revert `7c4b1a09`,
  branch `test-backdoor-check`) are recorded here for triage but not encoded as pack rules;
  Spice does not scan git object databases.
- Remediation guidance: any mnemonic or private key that passed through version `1.20.21` of
  these packages should be treated as compromised; move funds to fresh wallets, rotate secrets,
  and upgrade to `1.20.23` or later.
