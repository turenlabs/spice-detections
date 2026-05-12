# Mini Shai-Hulud Dead-Man's Switch Notes

Date: 2026-05-12

## Summary

The May 2026 Mini Shai-Hulud / TanStack wave includes a destructive persistence component commonly identified as `gh-token-monitor`. Public reporting describes it as a launchd or systemd user unit that monitors stolen GitHub token validity and runs `rm -rf ~/` if the token is revoked or starts returning a GitHub 4xx response.

## Detection Signals Added

- `gh-token-monitor` service or script name
- macOS LaunchAgent path: `~/Library/LaunchAgents/com.user.gh-token-monitor.plist`
- Linux systemd user service path: `~/.config/systemd/user/gh-token-monitor.service`
- Linux helper path reported by Snyk: `~/.local/bin/gh-token-monitor.sh`
- GitHub commit marker: `IfYouRevokeThisTokenItWillWipeTheComputerOfTheOwner`
- destructive handler command: `rm -rf ~/`
- GitHub polling behavior involving `api.github.com/user`, 60 second polling, or the commit-search marker
- optional 24 hour TTL indicator

## Sources

- Wiz, "Mini Shai-Hulud Strikes Again: TanStack + more npm Packages Compromised", 2026-05-12.
- Snyk, "TanStack npm Packages Hit by Mini Shai-Hulud", 2026-05-11/12.
- Cybersecurity Reach Foundation, "IfYouRevokeThisTokenItWillWipeTheComputerOfTheOwner: Inside the New Shai-Hulud npm Worm", 2026-05-11.
- TanStack, "Postmortem: TanStack npm supply-chain compromise", 2026-05-11.
