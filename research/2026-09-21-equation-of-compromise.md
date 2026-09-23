# Equation of Compromise npm Campaign

This data-only pack covers the malicious package versions that JFrog attributes to one multi-month npm campaign, including the runtime-triggered `indexed-btree` loader. It also includes the independent OSV-confirmed `indexed-btree@2.1.1` version.

## Sources

- JFrog Security Research, September 21, 2026: https://research.jfrog.com/post/equation-of-compromise/
- OSSF OSV MAL-2026-15888: https://github.com/ossf/malicious-packages/blob/main/osv/malicious/npm/indexed-btree/MAL-2026-15888.json
- Checkmarx indexed-btree analysis: https://checkmarx.com/zero-post/npm-btree-malware-campaign-affects-millions-of-downloads-no-need-for-install-script/

## Added Coverage

The CSV contains every exact version in JFrog's "Malicious packages, live at time of writing" table. `indexed-btree@2.1.2` is in that table; OSV independently identifies `indexed-btree@2.1.1` and supplies package archive SHA-256 values for both versions. The pack also detects the unusual LICENSE infection marker and uses a composite requiring at least two of the indexed-btree setter hook, its `sharedLoad.min.js` loader, and the campaign's exact Sepolia contract.

## Boundaries

JFrog could not recover the final encrypted task payloads; the pack does not claim those effects. Do not include the report's separate inflated/PuP list (`secure-library-loader`, `matrixhub`, `matrix-ops-core`), which is not established as weaponized. Avoid generic math-library, Slack, Telegram, RPC, and cloud-metadata indicators. Individual IOCs can appear in threat-intelligence text; exact package versions and the runtime-trigger composite are the primary signals.
