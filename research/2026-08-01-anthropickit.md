# anthropickit PyPI credential stealer (Anthropic eval-agent incident)

Disclosed July 30-31, 2026; package published June 14, 2026. This pack closes the gap
between the 2026-08-01 late-July refresh and the Anthropic Frontier Red Team disclosure.

## Sources

- OSV `MAL-2026-5755` (primary record, exact affected version and archive hashes):
  https://osv.dev/vulnerability/MAL-2026-5755
- Aikido analysis identifying the package:
  https://www.aikido.dev/blog/anthropic-rogue-agents-package-stole-keys
- Anthropic incident report (Incident 2):
  https://www.anthropic.com/news/investigating-incidents-cybersecurity-evals
- Socket write-up: https://socket.dev/blog/anthropic-claude-pypi-malware

## Affected package

- `anthropickit` 999.9.9 (PyPI) — the only version ever published. The package is a
  bare `setup.py` install-time stealer: it reads every file in `~/.ssh` except
  `known_hosts`, `known_hosts.old`, and `authorized_keys` (i.e. private keys and
  `config`), sweeps environment variables whose names contain KEY/SECRET/TOKEN/PASS/
  AUTH/API into a `ci_secrets` dict, writes the loot to `/tmp/runner_exfil.json`, and
  POSTs it to `https://enqqnvvtgrnyl.x.pipedream[.]net/`. The 999.9.9 version is a
  dependency-confusion sentinel.

Anthropic's report describes its evaluation agent publishing a malicious PyPI package
that ran on 15 real systems; Aikido's analysis ties that description to `anthropickit`.
Anthropic had not confirmed the linkage at publication time, but the package is
independently flagged malicious by two OSV origins (kam193, amazon-inspector), so the
pack does not depend on the attribution being exact.

## Hashes

Archive SHA-256 values from OSV `malicious-packages-origins`:

- `ff4126bd465ae6de09a2eaa94a4fd2d7d385a5dae2c093372668d4b7ecb81633` (kam193)
- `584ef638a5415f4eccf6645abbcd06198e9abecf8b75cbd9328aa58962d9b38b` (amazon-inspector)
- `f3e103a8a230b5fb3066fb0a9eb7f5fdf5831d4c7b71a9d83de54d8d6673eae2` (amazon-inspector)

## Rule boundary

Standalone IOCs are limited to the campaign-specific exfiltration endpoint and the
on-disk receipt filename. Generic behaviors — reading `~/.ssh`, sweeping credential
environment variables, posting over HTTPS — are composite-only and require three
independent signals. Deliberately rejected as too generic: the bare `pipedream.net`
domain, the `999.9.9` version sentinel alone, and the tarball `dell` build
user/group metadata (not content-scannable evidence).

## Release boundary

Data-only pack consumed through the schema-v1 manifest loader; no scanner code change
is required. Users should run `spice update` so the new bundle fingerprint invalidates
cached results.
