# Crates.io Build-Script Compromise

This data-only pack covers the August 20, 2026 crates.io compromise. The Rust Security Response Team reports three republished crates that pulled in a malicious build dependency; JFrog identifies the exact dropper versions and build-time payload behavior.

## Sources

- Rust Security Response Team: https://blog.rust-lang.org/2026/08/20/supply-chain-attack-on-arrayref/
- RustSec RUSTSEC-2026-0260: https://rustsec.org/advisories/RUSTSEC-2026-0260.html
- JFrog: https://research.jfrog.com/post/arrayref-proc-macro1-crates-io/

## Added Coverage

The package CSV contains only exact versions identified by the Rust Security Response Team and JFrog: `arrayref@0.3.10`, `internment@0.8.7`, `append-only-vec@0.1.9`, `proc-macro1@1.0.107`, and `proc-macro-en@1.0.10`. The last two crates carry the build-script download-and-execute behavior. The pack includes the reported staged payload filenames and a composite for the split Base64 C2 fragments plus detached process launch.

Spice already content-scans Cargo manifests/lockfiles and `build.rs`, and maps the `crates` ecosystem. No scanner code change is needed for these rules.

## Boundaries

Do not flag generic `build.rs` files or unrelated lookalikes such as `aovine`, `arone`, `aronenao`, and `tinymember` as equivalent malware. JFrog reports those lookalikes only write a test string or dummy build metadata; they are not the remote payload dropper covered here. The exposed publish windows were short, but RustSec reports 2,285 downloads of `arrayref@0.3.10`.
