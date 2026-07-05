# Miasma tracker refresh - July 2026

Source:

- Socket tracker: Miasma Mini Shai-Hulud Supply Chain Attack
  (https://socket.dev/supply-chain-attacks/miasma-mini-shai-hulud-supply-chain-attack)

Pack: `miasma-2026-06`

## Summary

Socket's Miasma tracker was refreshed through 2026-07-04 with 527 artifacts across npm, PyPI, and
Go module rows. The existing Spice Miasma pack already covered Red Hat npm, Hades PyPI, and
Leo/RStreams npm rows from earlier sources. This refresh preserves existing rows and unions in
Socket's current public tracker data.

## Added coverage

- New and updated npm package/version rows, including the late ImmobiliareLabs Backstage plugin wave.
- New PyPI rows from the current tracker CSV.
- Go module pseudo-version rows now that the app can match `go.mod` against the `go` ecosystem.

## Scan notes

The merged CSV is generated as exact package/version rows. Pack-side data alone is not enough for
Go modules; the app must treat `go.mod` as a text manifest and preserve leading-`v` pseudo-versions
from detection CSVs.
