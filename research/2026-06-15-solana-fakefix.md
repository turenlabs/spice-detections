# Solana FakeFix npm and PyPI malware - June 2026

Source:

- JFrog Security Research: Solana Crypto Stealers, FakeFix Campaigns and Malicious npm Packages
  (https://research.jfrog.com/post/solana-fakefix/)

Pack: `solana-fakefix-2026-06`

## Summary

JFrog reported a cluster of malicious npm and PyPI packages targeting Solana developers, including
fake Solana/web3 packages, fake MEV tooling, and a CMS-themed FakeFix payload chain. The report
published package names and payload IOCs but did not publish a complete exact affected-version table,
so this pack uses IOC and composite rules instead of a package-version CSV.

## Added coverage

- Package-name reference IOC for the fake Solana/web3, blockchain utility, and CMS package names
  published by JFrog.
- Exact infrastructure and payload markers: `104.239.66.223:8899`, `77.90.185.225`,
  `PassWord1337/updates/main/install.js`, and the published Solana wallet address.
- Composite IOC for Telegram-based Solana key exfiltration.
- Composite IOC for the Windows/Deno FakeFix loader path.
- Composite IOC for the fake MEV private-key prompt and wallet-drain transfer path.

## Scan notes

The package-name IOC is intentionally scoped to unusual typosquat/fake-package names from the
writeup. Exact version rows should be added later if a primary source publishes affected versions.
