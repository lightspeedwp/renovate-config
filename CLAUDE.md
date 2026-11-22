# CLAUDE.md

Organisation-wide Renovate config for `lightspeedwp`, applied by the Mend Renovate app as
inherited config. See README.md for the policy.

- `org-inherited-config.json` is the only config file. Its name and location are fixed by Mend.
- Any change reaches every repository on the next Renovate run, so keep changes small.
- Validate before committing:
  `npx --yes --package renovate -- renovate-config-validator --strict org-inherited-config.json`
- Record every change in CHANGELOG.md (Keep a Changelog).
- Branch names follow `{type}/{short-title}` from lightspeedwp/.github.
