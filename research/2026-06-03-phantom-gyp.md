# Miasma Phantom Gyp npm compromise - June 2026

Sources:

- https://www.stepsecurity.io/blog/binding-gyp-npm-supply-chain-attack-spreads-like-worm
- https://snyk.io/blog/node-gyp-supply-chain-compromise-self-propagating-npm-worm-binding-gyp/
- https://security.snyk.io/node-gyp-supply-chain-compromise-june-2026
- https://www.chainguard.dev/unchained/chainguard-artifacts-safe-from-miasma-phantom-gyp-npm-attack

Pack: `phantom-gyp-2026-06`

## Summary

On 2026-06-03, Miasma spread across npm packages with an install-time technique StepSecurity named Phantom Gyp. Instead of adding `preinstall` or `postinstall` scripts to `package.json`, the malicious tarballs added a `binding.gyp` file that made npm run `node-gyp rebuild`. The Gyp command substitution then executed `node index.js` and returned `stub.c` so the native-build path completed quietly.

The pack encodes StepSecurity's affected package table and adds content IOCs for:

- `<!(node index.js > /dev/null 2>&1 && echo stub.c)` inside `binding.gyp`
- Miasma dead-drop markers
- Bun runtime download and payload handoff
- GitHub Actions memory/token theft signals
- GitHub API exfiltration and results artifacts

## Scan notes

`binding.gyp` is common in legitimate native npm packages, so it is not a suspicious filename atom by itself. Spice must content-scan `binding.gyp` only in package-cache and archive contexts, then let the composite IOC require the Phantom Gyp command-substitution shape.
