# September 2026 Shai-Hulud Reactivation

This data-only refresh adds the four npm packages published on September 7,
2026 with the byte-identical Shai-Hulud payload previously observed in the May
AntV wave. The current registry metadata now points each package at a
`0.0.1-security` holding release, but the malicious versions remain relevant
to lockfiles, npm caches, package archives, and incident review.

## Sources

OpenSSF OSV malicious-package records:

- https://api.osv.dev/v1/vulns/MAL-2026-16032 (`feishu-docx-mcp@0.3.2`)
- https://api.osv.dev/v1/vulns/MAL-2026-16025 (`bmc-i18n-extract-cli@1.1.1`)
- https://api.osv.dev/v1/vulns/MAL-2026-16024 (`blueai-cli@0.7.0`)
- https://api.osv.dev/v1/vulns/MAL-2026-16026 (`bmc-translate-utils@1.1.1`)

Primary campaign reporting:

- https://www.aikido.dev/blog/shai-hulud-npm-resurfaces
- https://corgea.com/research/shai-hulud-npm-resurfaced-four-packages-september-2026
- https://registry.npmjs.org/feishu-docx-mcp
- https://registry.npmjs.org/bmc-i18n-extract-cli
- https://registry.npmjs.org/blueai-cli
- https://registry.npmjs.org/bmc-translate-utils

## Added coverage

The package rows are exact version matches for the four OSV records. All four
records identify the same `index.js` SHA-256:

`e37e3ddeeaaa9e0c4fdbcb829b4895a6521031c80053fc436625b61e6ee5b1a6`

The pack also matches the shared install-time shape: a `bun run index.js`
preinstall hook, the Bun 1.3.13 dependency, and an obfuscated payload that
validates GitHub tokens, enumerates organizations, and inspects OAuth scopes.

## Boundaries

No generic `index.js` filename rule, generic lifecycle-hook rule, or hidden
endpoint inferred from the reports is included. The exact payload hash and
behavioral rules are retained as high-confidence evidence; the package rows
remain the primary detection path for manifests and lockfiles. This refresh
does not require a Spice scanner, application, or Homebrew release.
