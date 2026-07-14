# Miasma v3 AsyncAPI npm compromise - July 2026

Sources:

- JFrog Security Research: Miasma Worm Returns to npm
  (https://research.jfrog.com/post/miasma-worm-returns-to-npm/)
- Wiz Research: M Red Team AsyncAPI supply-chain compromise via GitHub Actions
  (https://www.wiz.io/blog/m-red-team-asyncapi-supply-chain-compromise-via-github-actions)
- Socket: AsyncAPI supply-chain attack
  (https://socket.dev/blog/asyncapi-supply-chain-attack)

Pack: `asyncapi-miasma-2026-07`

## Summary

Researchers disclosed a new Miasma generation delivered through five legitimate AsyncAPI npm
package versions. The attacker abused a `pull_request_target` workflow to obtain a maintainer token,
pushed code to the repository's `next` branch, and let the project's normal release workflow publish
the compromised artifacts. Those releases therefore carried valid npm provenance; provenance alone
does not establish that their contents were safe.

The malicious code executes when an affected package is loaded, not through an npm install hook.
A lockfile match proves exposure to a compromised version but does not, by itself, prove that the
package was imported or that its payload ran. The configuration analyzed by the researchers enabled
the persistent remote-access, shell, and payload-update path. Additional credential collection,
repository propagation, AI-tool poisoning, evasion, and metamorphic modules were present but disabled
in that observed configuration, so this pack does not claim those dormant modules executed.

## Added coverage

- Exact npm rows for `@asyncapi/generator@3.3.1`,
  `@asyncapi/generator-helpers@1.1.1`, `@asyncapi/generator-components@0.7.1`,
  `@asyncapi/specs@6.11.2`, and `@asyncapi/specs@6.11.2-alpha.1`.
- Whole-tarball SHA-256 values for all five releases, as published by Socket. These hashes are safe
  for Spice's package-archive hash path; internal-file hashes are intentionally not duplicated as
  whole-package hashes.
- High-specificity network and protocol indicators: the IPFS CID, C2 IP and ports,
  `X-Miasma-Spawn-Chain`, `_miasma._tcp`, the train identifier, and the on-chain registry contract.
- Composite rules for the cross-platform NodeJS persistence path and the multi-channel C2 discovery
  protocol.

## Scan notes

- The affected package names are legitimate. Only the exact versions in the CSV are package-level
  findings.
- The five SHA-256 values identify complete npm tarballs, not individual extracted source files.
- Generic NodeJS paths, systemd unit syntax, IPFS use, and Ethereum addresses are not standalone
  detections. The pack uses the campaign-specific values or requires several persistence/C2 signals.
