# Braintree.Net NuGet payment-data skimmer - July 2026

Source:

- Socket: Braintree NuGet typosquat skims credit cards
  (https://socket.dev/blog/braintree-nuget-typosquat-skims-credit-cards)

Pack: `braintree-nuget-2026-07`

## Summary

Socket reported malicious NuGet releases under `Braintree.Net` that imitated the legitimate
Braintree .NET SDK and injected payment-card and account telemetry collection. The payload loaded
`DependencyInjector.Core`, decoded an obfuscated endpoint, and sent records to the unrelated
`api.348672-shakepay.com` host. Four `SipNet` releases declared the malicious dependency only for
.NET 8, 9, and 10 target frameworks; their assemblies were not themselves modified.

## Added coverage

- Exact NuGet rows for `Braintree.Net` versions `3.35.8` through `3.36.1`,
  and `DependencyInjector.Core` versions `1.0.0`, `1.3.0`, `1.4.0`, and `1.4.1`.
- Exact C2 hostname, API key, endpoint-obfuscation key and blob, and campaign-specific injected
  class names.
- Composites for the payment-data reporting channel and dependency-loader structure.

## Scan notes

- `SipNet@12.8.4` through `12.8.7` are not encoded as unconditional affected rows. Socket found the
  `SipNet` assemblies clean and the malicious `DependencyInjector.Core` dependency applies only to
  .NET 8, 9, and 10. The current pack schema cannot qualify a package row by target framework, so a
  direct row would mislabel classic .NET Framework and .NET Standard consumers. A resolved malicious
  `DependencyInjector.Core` version still matches in `packages.lock.json` or `project.assets.json`.
- `SipNet.OpenAI.Realtime@12.8.3` is also not encoded. Its own code is benign, and NuGet's default
  lowest-applicable resolution selects clean `SipNet@12.8.3`; exposure requires another constraint
  to float `SipNet` to a release that brings in the malicious dependency for a covered framework.
- Published DLL hashes are hashes of internal assemblies, not complete `.nupkg` archives. They are
  intentionally left out of `knownSha256` until Spice has an explicit archive-member hash contract.
- Generic DLL names and .NET loader/reflection terms are not suspicious filename atoms. Findings
  require an exact affected version, campaign-specific IOC, or multi-signal composite.
