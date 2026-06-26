# 2026-06-25 Leo/RStreams Shai-Hulud / Hades npm wave

Source:

- JFrog Security Research: Shai-Hulud Continues: Hades Payload Hits Leo/RStreams npm Packages
  (https://research.jfrog.com/post/shai-hulud-miasma-alright-lets-see-if-this-works/)

Pack: `miasma-2026-06`

## Summary

JFrog reported a new Shai-Hulud/Hades npm wave affecting 20 Leo/RStreams ecosystem packages. The
payload reused the broader Hades/Miasma behavior family: credential collection, GitHub dead-drop
exfiltration, package-registry and CI/CD propagation logic, AI-tool persistence hooks, and
`gh-token-monitor` dead-man switch behavior. Delivery still uses the `binding.gyp` install-time
execution path, where npm can invoke `node-gyp rebuild` and expand `<!(...)` shell substitutions.

## Added coverage

- 20 exact npm package/version rows from JFrog's IOC table.
- New campaign and token relay markers: `Alright Lets See If This Works` and `RevokeAndItGoesKaboom`.
- Additional decoded strings and exact payload key/search markers: `TheBeautifulSandsOfTime`,
  `thebeautifulmarchoftime`, the two published RSA public-key prefixes, and the GitHub commit-search
  marker for `firedalazer`.
- Expanded Hades GitHub dead-drop and JavaScript-stealer composites so the Leo marker set is covered
  alongside the older Hades marker set.
- A gated `SEED_PAT` bootstrap composite requiring `GITHUB_REPOSITORY`, `Seeder`, and `SEED_PAT`
  together instead of treating `SEED_PAT` as a standalone IOC.
- An AI-tool persistence/workflow composite for strings JFrog published in the repository and workflow
  IOC section, including `.windsurfrules`, `.github/copilot-instructions.md`, `mcp.json`, and
  `.aider.conf.yml`.

## App scan-boundary note

The app must content-scan the added AI/editor config paths in default project scans; otherwise pack
regexes only fire in deep scans or package archives. This update pairs the pack changes with an
engine `scanEngineVersion` bump and new repo-open scan gates for `.windsurfrules`,
`.github/copilot-instructions.md`, `mcp.json`, and `.aider.conf.yml`.
