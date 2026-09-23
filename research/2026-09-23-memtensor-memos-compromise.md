# MemTensor MemOS npm and PyPI Compromise

This data-only pack covers the September 23, 2026 compromise of the MemTensor MemOS npm plugin and PyPI package reported by Socket.

## Source

- Socket Security Research: https://socket.dev/blog/memtensor-compromise

## Added Coverage

The package CSV contains the three compromised npm releases (`@memtensor/memos-cloud-openclaw-plugin@0.1.21`, `@memtensor/memos-cloud-openclaw-plugin@0.1.23`, and `@memtensor/memos-cloud-openclaw-plugin@0.1.25`) and `memoryos@2.0.34` from PyPI. The known SHA-256 map includes the PyPI wheel and source distribution hashes plus all reported cross-platform `sckit` binary hashes. The exact `sckit`/`sckit.exe` member names enable hash inspection within npm and PyPI package archives.

## Boundaries

The intervening npm releases `0.1.22` and `0.1.24` are omitted because Socket says their contents match the last known-good `0.1.20` apart from version strings. No generic credential names or parent-domain regexes are included; affected versions and artifact hashes are the primary detection signals. Socket performed static analysis and had not executed the binaries when the report was published.
