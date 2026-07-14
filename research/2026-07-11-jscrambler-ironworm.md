# IronWorm Jscrambler npm compromise - July 2026

Sources:

- Jscrambler security advisory
  (https://jscrambler.com/blog/security-advisory-malicious-npm-package)
- JFrog Security Research: IronWorm returns, rustier than ever
  (https://research.jfrog.com/post/ironworm-returns-rustier-than-ever/)
- Socket: Jscrambler supply-chain attack
  (https://socket.dev/blog/jscrambler-supply-chain-attack)

Pack: `ironworm-jscrambler-2026-07`

## Summary

Jscrambler disclosed malicious `jscrambler` releases in the IronWorm family. Versions `8.14.0`,
`8.16.0`, and `8.17.0` used a `preinstall` hook that ran `node dist/setup.js`. Versions `8.18.0`
and `8.20.0` moved execution into normal package import/CLI behavior and self-depended on
`jscrambler:^8.17.0`, so `npm --ignore-scripts` was not a sufficient control for the later releases.
The payload was stored in a custom CSI container whose magic bytes are `1B 43 53 49 01 03 00`.

The vendor also listed four dependent plugin releases as affected. They are encoded as exact
package/version exposure rows rather than described as independently injected packages.

## Added coverage

- Exact npm rows for five `jscrambler` releases plus
  `jscrambler-webpack-plugin@8.6.2`, `gulp-jscrambler@8.6.2`,
  `grunt-jscrambler@8.5.2`, and `jscrambler-metro-plugin@9.0.2`.
- Standalone detection of the campaign-specific CSI magic bytes and two published C2 IP addresses.
- Separate same-manifest composites for the preinstall generations and the later import-time
  generations. Each composite uses package identity, exact affected version, and the generation's
  execution/dependency marker so every required signal can co-occur in one `package.json`.

## Scan notes

- `setup.js`, `intro.js`, and `dist/` are common names and are deliberately not suspicious-filename
  atoms. Filename presence alone must not produce an archive finding.
- Published hashes for `dist/intro.js` and extracted platform payloads are internal-file hashes.
  They are recorded by the sources but not put in `knownSha256`, because Spice's current hash path
  must not misrepresent them as complete npm tarball hashes.
- Jscrambler's clean replacements are `jscrambler@8.22.0` and plugin versions `8.6.3`, `8.6.3`,
  `8.5.3`, and `9.0.3` respectively; those clean versions are not flagged.
