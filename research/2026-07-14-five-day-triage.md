# Five-day supply-chain detection triage - July 14 2026

Review window: July 9-14, with July 8 included where a disclosure or artifact boundary touched the
window.

## Added or corrected

- Miasma v3 AsyncAPI, Jscrambler IronWorm, nodemon-sudo/tslint-conf, and Braintree.Net incident
  packs.
- Exact PyPI and npm advisory packs for newly published records whose versions could be represented
  without broad range inference.
- IronWorm's June CSV was corrected against JFrog's primary table and explicit OSV deltas.

## Reviewed without a new pack

- **Injective Labs SDK:** already covered by `injective-2026-07`, including all 18 exact npm rows,
  tarball/chunk hashes, and the key-derivation exfiltration IOCs. A duplicate pack would only create
  duplicate findings.
- **Lucide Proxy:** JFrog's July 13 report
  (https://research.jfrog.com/post/lucide-proxy-npm-malware-campaign/) spans multiple generations.
  The July 8 wave was described as adware-only while earlier May variants carried DDoS/RCE
  behavior. The available campaign list does not provide a safe per-version capability mapping for
  Spice's critical affected-version finding, so encoding the full list would overstate the July
  artifacts. Coverage is deferred until those boundaries are exact.
- **Muck-and-Load:** Socket's July 8 report
  (https://socket.dev/blog/malicious-go-module-exposes-github-malware-lure-network) describes more
  than 1,200 versions and more than 700 malicious builds of
  `github.com/kaleidora/dnsub-scanning-tool`, but does not publish the exact malicious-version set.
  A guessed range or all-version row would violate the exact-version contract, so no package row was
  added.
- **IDE/editor recirculation:** the reviewed July 9-14 coverage repeated July 8 GhostApproval and
  Friendly Fire disclosures without a newly verified extension/artifact mapping. No new IDE pack
  was justified.
- **GitHub advisory feed noise:** broad `>= 0`, update-only, and batch-published records were not
  translated into all-version findings. Exact newly published rows that survived deduplication were
  retained in `npm-malware-2026-07`.

## Boundary notes

Advisory publication date, package upload date, incident date, and article date are different
signals. Feed packs in this review are explicitly labeled by record publication date. Incident
packs use the primary research to describe execution timing and do not infer execution merely from
a lockfile match.
