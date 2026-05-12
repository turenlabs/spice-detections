# 2026-05-12 Shai-Hulud Detection Refresh

This refresh adds cross-ecosystem indicators for Shai-Hulud, Sha1-Hulud 2.0, and Mini Shai-Hulud activity observed across npm, PyPI, Maven mirrors, and Packagist.

## Sources

- CISA: Widespread Supply Chain Compromise Impacting npm Ecosystem
- StepSecurity: Shai-Hulud Self-Replicating Worm Compromises 500+ NPM Packages
- Datadog Security Labs: The Shai-Hulud 2.0 npm worm
- Socket: Shai Hulud Strikes Again v2
- Snyk: TanStack npm Packages Hit by Mini Shai-Hulud
- Aikido: Mini Shai-Hulud Is Back
- Socket: Intercom npm package compromise
- Socket: Packagist Intercom PHP package compromise

## Added coverage

- Shai-Hulud v1 `bundle.js` SHA-256 and webhook/workflow strings.
- Sha1-Hulud 2.0 Maven mirror SHA-1 for `org.mvnpm:posthog-node`.
- Mini Shai-Hulud C2 and second-stage payload strings reported in the TanStack wave.
- Intercom npm/Packagist payload hashes, Composer plugin strings, and package/version rows.
- Campaign strings used in repo descriptions, commits, and generated artifacts.
