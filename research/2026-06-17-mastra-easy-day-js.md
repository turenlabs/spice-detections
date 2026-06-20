# Mastra / easy-day-js npm compromise - June 2026

Sources:

- https://socket.dev/blog/mastra-npm-packages-compromised
- https://www.aikido.dev/blog/over-140-popular-mastra-npm-packages-hit-by-supply-chain-attack
- https://research.jfrog.com/post/easy-day-js/
- https://security.snyk.io/mastra-supply-chain-compromise-june-2026

Pack: `mastra-2026-06`

## Summary

On 2026-06-17, compromised `@mastra/*` package versions were published with an injected transitive dependency on `easy-day-js`. The malicious behavior is in `easy-day-js@1.11.22`, which adds a `postinstall` hook that runs `node setup.cjs --no-warnings`.

The pack combines affected package/version rows from Aikido's published list with IOCs from Socket and JFrog:

- `easy-day-js@1.11.22`
- `setup.cjs` stage-1 loader hash and postinstall marker
- C2 endpoints `23.254.164.92:8000/update/49890878` and `23.254.164.123:443/49890878`
- loader markers `.pkg_history` and `.pkg_logs`
- persistence artifacts `protocal.cjs`, `NvmProtocal`, `com.nvm.protocal`, `nvmconf.service`, and `NodePackages`

## Scan notes

The affected package CSV catches lockfiles and manifests that record the compromised versions. The IOC rules catch the malicious `easy-day-js` payload in package caches, tarballs, install logs, and persistence locations. `setup.cjs` is intentionally not a suspicious filename atom by itself because benign packages commonly use setup loaders; it is gated by content IOCs and composites.
