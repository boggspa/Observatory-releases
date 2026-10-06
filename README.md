# TaskWraith Observatory — releases

Signed and notarised macOS builds of **TaskWraith Observatory**, a local
dashboard for the Git repositories you work on and the AI models you use. This
repository holds release downloads and documentation only; the source is
private for now.

**[Download the latest release](https://github.com/boggspa/Observatory-releases/releases/latest)**

Requires macOS on Apple silicon (arm64). Builds are Developer ID–signed and
notarised by Apple, so they open without Gatekeeper warnings.

## What it shows

- **Repository tabs.** TaskWraith plus up to eight other local Git worktrees:
  commits, tracked lines, active days, branches, ahead/behind, working-tree
  change counts and self-expiring work-claim markers.
- **GitHub.** Stars, forks, watchers, issues, release download counters and
  star history. With a credential that has push access to the repository
  (a `gh auth login` session or a fine-grained token), also views, clones,
  top referrers and popular content.
- **Model usage.** If TaskWraith is installed, a year heatmap, 90-day
  heatmaps by 2-hour band, 90-day token charts and a per-model table, read
  from TaskWraith's local usage files.
- **Optional extras.** App Store Connect analytics reports and a loopback
  activity receiver, both off until configured.

## Privacy

Observatory runs locally. It has no account and sends no telemetry about you.

- Git facts are read locally and read-only. File contents and diff bodies are
  never read; only numeric totals and status counts are.
- Model usage is read from TaskWraith's files on this Mac. Workspace, chat and
  run identifiers are dropped before anything reaches the window, and nothing
  is uploaded.
- Network requests go only to `api.github.com` (repository metadata, releases,
  star dates, traffic), `api.appstoreconnect.apple.com` (only if you add
  credentials), and, for the window's sky backdrop, `ipapi.co` / `ipwho.is`
  (approximate location, rounded to about 11 km) and `api.open-meteo.com`
  (weather).
- Tokens and keys you enter are encrypted with the macOS keychain before they
  are written to disk.

## Verifying a download

Each release lists SHA-256 checksums and attaches `RELEASE-PROVENANCE.json`.

```bash
shasum -a 256 TaskWraith-Observatory-<version>-arm64.dmg   # compare with the release notes
hdiutil attach TaskWraith-Observatory-<version>-arm64.dmg
APP="/Volumes/TaskWraith Observatory <version>-arm64/TaskWraith Observatory.app"
codesign --verify --deep --strict "$APP"
spctl --assess --type execute -v "$APP"     # expect: accepted, source=Notarized Developer ID
xcrun stapler validate "$APP"
```

A Developer ID signature publicly identifies the signer's name and Apple Team
ID; that is inherent to macOS code signing.

## Feedback

Please open an [issue](https://github.com/boggspa/Observatory-releases/issues)
for bugs or requests.

## Licence

Apache License 2.0. See [LICENSE](LICENSE) and [NOTICE](NOTICE). Third-party
brand marks shown in the app are excluded from the licence grant.
