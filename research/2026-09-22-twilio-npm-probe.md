# Twilio-Themed npm Probe

This data-only pack covers only the per-version behavior established by ReversingLabs for `tw-pkgprobe-7731`. The source provides package SHA-1 values for all releases, but its narrative is internally inconsistent about `1.0.8` and does not detail `1.0.5` through `1.0.7`; those releases are intentionally omitted from critical rules.

## Sources

- ReversingLabs, September 22, 2026: https://www.reversinglabs.com/blog/malicious-npm-campaign-twilio

## Added Coverage

Exact package rows and SHA-1 archive hashes cover `tw-pkgprobe-7731@1.0.0` through `1.0.4`. Version `1.0.0` collects host/environment data and sends it to a webhook; `1.0.1` through `1.0.3` probe Twilio SID-named directories and inject an npm PoC; `1.0.4` explicitly exfiltrates `ACCOUNT_SID` and `AUTH_TOKEN` (SHA-1 `35b21553837b74e1fc5ac43efd839cdc28109fdf`). Package rows detect manifests/lockfiles; SHA-1 rules detect the exact package archives when scanned.

## Boundaries

Do not match Twilio environment-variable names, hostnames, webhooks, or cloud metadata alone; these are normal in Twilio development environments. Releases `1.0.5` through `1.1.1` are omitted pending clearer version-specific evidence. In particular, the report describes `1.1.0` and `1.1.1` as reconnaissance and contradicts itself about `1.0.8`.
