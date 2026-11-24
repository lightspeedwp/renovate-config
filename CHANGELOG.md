# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

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
