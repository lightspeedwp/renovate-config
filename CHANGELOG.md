# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Changed

- Automerge every update type, majors and 0.x versions included, once status checks pass.
  `lightspeed-hosting-infra` stays excluded.
- Match 0.x versions independently of the package versioning scheme and clarify how repositories
  can override inherited automerge package rules.

### Added

- Organisation-wide inherited Renovate config: no onboarding PR, config file optional, automerge
  for minor, patch, pin and digest updates once checks pass, majors and 0.x left for review.
