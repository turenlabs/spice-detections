# PolinRider cross-ecosystem campaign - July 2026

Sources:

- Socket: PolinRider: North Korea-Linked Supply Chain Campaign Expands to npm, Packagist, Go Modules, and Chrome Extensions
  (https://socket.dev/blog/polinrider-north-korea-linked-supply-chain-campaign-expands)
- Socket tracker CSV:
  (https://socket.dev/supply-chain-attacks/polinrider)

Pack: `polinrider-2026-07`

## Summary

Socket reported PolinRider as an active, North Korea-linked campaign spanning npm, Packagist,
Go modules, and Chrome extensions. The 2026-07-01 tracker listed 162 artifacts. Spice covers the
supported package ecosystems from that tracker: npm, Composer/Packagist, and Go modules.

## Added coverage

- Exact npm, Composer, and Go module package/version rows from Socket's public CSV.
- Composer `dev-*` rows are included, so the app must preserve non-numeric exact versions from pack
  CSVs.
- Go module pseudo-versions are included, so the app must map `go.mod` to the `go` ecosystem.
- Composite IOC for the VS Code folder-open fake-font loader shape: `runOn: folderOpen`, Node
  execution, and a disguised `.woff2` payload.
- Composite IOC for obfuscated JavaScript that combines blockchain RPC targeting, developer secret
  collection, and loader/config injection context.

## Scan notes

Chrome extension artifacts from the Socket tracker are intentionally not encoded as package rows
because Spice does not currently index browser-extension manifests as a package ecosystem. The
Chrome extension names remain a future browser-extension scanning feature, not a detection-pack row.
