# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Fixed

- Keep the default `renovate/` branch prefix. The `deps/` prefix made `.github`'s `Validate branch name` check fail (it exempts only `renovate/` and `dependabot/`, and rejects dots such as `7.x`). `prHeader` already satisfies the PR template check.

- Renovate pull requests now pass each repository's gates: labelled `meta:no-changelog` (the changelog gate in `.github` and `tas-plugin`), and `prHeader` supplies the PR template's non-empty sections.
- Stop pinning npm devDependencies (`:pinDevDependencies` ignored): exact pins conflicted with `overrides` in `.github` (`EOVERRIDE`, failing every `npm ci`). Action and Docker digest pins stay.
- Ignore `**/archived/**` paths so archived workflows are not re-pinned.
- Disable updates to the Keep UI/API digests in `lightspeed-hosting-infra`: they are release-coupled and checked against `keep/versions.env`.
- Allow GHCR and Google Artifact Registry image updates without release timestamps while keeping the three-day cooldown for releases with timestamps.

- Semantic commit titles (`chore(deps):`), weekly schedule (before 07:00 Monday, Africa/Johannesburg), 3-day `minimumReleaseAge`, `prConcurrentLimit` 5, and one grouped pull request for non-major GitHub Actions updates.

### Changed

- Automerge only non-major updates: minor and patch (not 0.x) plus digest, pin and lock-file
  maintenance, through `packageRules` as the Renovate docs recommend. Major updates and 0.x versions
  stay open for a human. Replaces the top-level `automerge: true`.
- Stop excluding `lightspeed-hosting-infra` from automerge: it is now merged by Renovate once its
  status checks pass, like every other repository. Removes the `matchRepositories` exclusion rule.
- Clarify how repositories can override inherited automerge package rules.

### Added

- Organisation-wide inherited Renovate config: no onboarding PR, config file optional, and every
  update automerged by Renovate once status checks pass (`platformAutomerge` off).
