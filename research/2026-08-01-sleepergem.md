# SleeperGem RubyGems campaign — documented engine gap (no pack)

Disclosed July 19, 2026. No detection pack is shipped in this cycle; this note records
the evidence and the engine work required so a future change can pick it up.

## Source

- Aikido: https://www.aikido.dev/blog/sleepergem-rubygems-supply-chain-attack

## What happened

Two long-dormant RubyGems maintainer accounts were hijacked within hours of each other
to push the same malicious dependency into trusted gems — the first observed campaign
of this shape on RubyGems.

- `git_credential_manager` 2.8.0, 2.8.1, 2.8.2, 2.8.3: a dropper that downloads
  binaries from `https://git.disroot[.]org/git-ecosystem/` (a public Forgejo instance
  with an attacker-registered `git-ecosystem` username) with TLS verification disabled,
  executes them via `powershell -ExecutionPolicy bypass` or `/bin/sh`, and skips
  installation when ~30 CI environment variables are present. From 2.8.2 the installer
  is wired into the gem's load path, so a bare `require` triggers it.
- `dendreo`: two new versions adding `git_credential_manager` as a dependency. The
  primary source does not publish the exact version numbers.
- `fastlane-plugin-run_tests_firebase_testlab` (574,661 total downloads, unrelated
  maintainer): one new malicious version. The exact version number is not published.

No OSV records exist for these gems as of August 1, 2026.

## Why there is no pack

Spice's engine has no RubyGems support. Per `docs/DETECTIONS.md`, adding a new
ecosystem or file class requires an engine change (`manifestEcosystem`,
`normalizePackageEcosystem`, `textCandidate`, `isAlwaysScanBase`), plus `.gem` archive
handling for hash matching. That is scanner behavior, not pack data, and would require
an app release rather than a data-only refresh.

Exact versions are also unpublished for `dendreo` and
`fastlane-plugin-run_tests_firebase_testlab`; guessed package rows are not allowed.

## Candidate signals for a future engine change

- Exact rows: `git_credential_manager` = 2.8.0, 2.8.1, 2.8.2, 2.8.3 (rubygems).
- IOC: `(?i)git\.disroot\.org/git-ecosystem/` (campaign staging host).
- Composite: Forgejo `raw/branch/main` binary fetch + `OpenSSL::SSL::VERIFY_NONE` +
  `Process.spawn` shell/PowerShell execution + CI environment skip list.
