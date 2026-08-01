# Late-July 2026 detection refresh

This refresh covers high-confidence package-registry incidents disclosed after the
2026-07-14 manifest update. Exact package rows are used only where the source identifies
the affected version. Hashes and content IOCs are retained for payloads recovered from
archives or source files.

## Joyfill npm 2773 prereleases

Primary source: https://socket.dev/blog/joyfill-npm-beta-releases-compromised

Affected npm prereleases:

- `@joyfill/layouts` 0.1.2-2773.beta.0, 0.1.2-2773.beta.1, 0.1.2-2773.beta.2
- `@joyfill/components` 4.0.0-rc24-2773-beta.4, 4.0.0-rc24-2773-beta.5, 4.0.0-rc24-2773-beta.6

The advisory-backed versions are beta.0 and beta.4; the expanded six-version set is from
StepSecurity's sandbox comparison of the shared 2773 build line. The pack detects the
published archive and bundle hashes, the `A9-0135-3` marker, the detached `/$/boot` path,
blockchain resolver infrastructure, and developer-tool persistence markers. The loader
runs on import rather than through an npm lifecycle hook.

## PyPI malware advisories

Primary records: OSV `MAL-2026-10754`, `MAL-2026-10757`, `MAL-2026-10917`,
`MAL-2026-10926`, `MAL-2026-11049`, `MAL-2026-11094`, and `MAL-2026-10780`.

- `airflow-provider-spirit` 0.0.1, 8.5.3, 8.5.4 and `dde-common` 0.0.1, 8.5.3, 8.5.4 use a fake telemetry PTH hook, rotating Cloudflare Workers, and DNS TXT payload delivery.
- `tinkoff-cloud-apis-internal` 0.0.1, 8.5.3, 8.5.4 is part of the same PTH/dropper campaign.
- `defi-kit` 2.1.1 imports a credential harvester that posts to two fixed IP endpoints.
- `mrmustard` 0.7.4 runs an import-time credential stealer and installs cron, shell, and PTH persistence.
- `govpkg` 0.1.0 and 0.2.0 downloads a binary and creates a disguised autostart entry.
- `cfgzen` 1.0.0 through 1.0.6 contains a native payload delivery chain.
- `data-parser-utils` 2.4.1 is a related tennacity campaign package with executable delivery and Poseidon infrastructure.

The pack does not treat generic `base64`, subprocess, HTTP, or environment access as standalone
malware indicators. Those behaviors are composite-only and require campaign infrastructure or
persistence markers.

## Pepesoft NuGet tools

Primary source: https://socket.dev/blog/11-malicious-nuget-tools-pose-as-game-cheats

The 11 malicious `DotnetTool` package IDs are `albion-x-x`, `amazing-x-x`, `calc-x-x`,
`grandrp-x-x`, `gta5rp-x-x`, `l2-x-x`, `majestic-x-x`, `rmrp-x-x`, `rusfish4-x-x`,
`throne-x-x`, and `trigger-x-x`. The public analysis gives an exact observed version for
`amazing-x-x` (7.7.8), so that row is included. Other package version mappings were not
published in the primary article and are not guessed. Downloader and payload hashes,
operator staging, the shared mutex and inherited key values, DNS-over-HTTPS resolution,
and `pepesoft.exe` execution are covered directly.

## Newtonsoftt.Json.Net NuGet typosquat

Primary source: https://jfrog.com/blog/nuget-typosquat-targets-betting-platform/

The seven exact malicious versions are 11.0.4, 11.0.5, 11.0.7, 11.0.8, 11.0.9,
11.0.10, and 11.0.11. The package is a trojanized Newtonsoft.Json fork targeting
Digitain's FG-Crash `GenerateGameResult` method and, in later generations, exfiltrating
results to `185.126.237.64:5341` using a Seq-shaped request.

## Alibaba-targeted npm cluster

Primary source: https://socket.dev/blog/npm-rat-targets-alibaba

The cluster includes `lib-mtop`, `aone-kit`, `aone-kit-cli`, `aone-sandbox`,
`local-config-parser`, `smart-config-manager`, `cloud-config-fetcher`,
`fast-transform-pipeline`, `aone-cloud-cli`, `colder-cli`, `def-open-client`,
`feedback-ai-sdk`, `flight-compare-analyzer`, `lwp-web-client`,
`lzd-unified-station-sdk`, `open-worker-cli`, `test-skill-zip`, and `uniapi-bridge`.
The primary report does not publish a complete exact-version mapping, so the pack uses
recovered payload hashes and composites for the package dependency chain, VM sandbox escape,
Alibaba Cloud staging, C2, and `__INJECT_MARKER__` persistence evidence instead of
all-version package rows.

## Release boundary

These are remote data packs. The Spice engine consumes them through the existing schema-v1
manifest loader; no scanner code change is required. Users of the next app release should run
`spice update` so the new bundle fingerprint invalidates cached results.

## Late-July npm advisory feed

Primary records: OSV `MAL-2026-10160`, `MAL-2026-11136`, `MAL-2026-11145`, `MAL-2026-11146`, and `MAL-2026-11137`.

The `npm-malware-2026-07-late` pack adds exact rows for `fluid-type-ui`, the rollup polyfill loader packages, `sigchain-js`, and `jobber-app-template-react`. Rules use package-specific loader behavior, companion payload stores, Ethereum resolver infrastructure, or the published exfiltration endpoint rather than generic JavaScript execution signals.
