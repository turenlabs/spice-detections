# nodemon-sudo and tslint-conf npm backdoor - July 2026

Source:

- SafeDep: Malicious nodemon-sudo / tslint-conf npm backdoor
  (https://safedep.io/malicious-nodemon-sudo-tslint-conf-npm-backdoor/)

Pack: `nodemon-tslint-2026-07`

## Summary

SafeDep disclosed `nodemon-sudo@3.1.16` and its malicious dependency
`tslint-conf@7.2.1` on July 9. The carrier imitated a legitimate package while the transitive
dependency retrieved JavaScript through an IPFS gateway and dead-drop configuration, then executed
the response with access to Node's `require` capability.

Neither affected package used an npm install lifecycle hook for the malicious path. Merely requiring
or importing the fake logger was inert; the backdoor fired only after an application wired and
called that exported logger at runtime. Installing with `--ignore-scripts` therefore did not remove
the risk once the fake logger was invoked. Conversely, a lockfile match shows affected dependency
resolution, not proof that the runtime path executed.

## Added coverage

- Exact npm rows for `nodemon-sudo@3.1.16` and `tslint-conf@7.2.1`.
- Whole-package SHA-256 values published for those two npm artifacts.
- Exact Pinata hostname, IPFS CID, and two JSONKeeper dead-drop paths.
- A composite that requires multiple delivery and dynamic-execution signals, including the unusual
  `x-secret-key: _` request header.

## Scan notes

The source also publishes hashes for individual JavaScript files. Those hashes are not encoded as
whole-package hashes. The two `knownSha256` entries in the pack are the complete package artifacts
that Spice can match safely.
