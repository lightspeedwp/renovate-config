# renovate-config

Organisation-wide Renovate configuration for the `lightspeedwp` GitHub organisation, run by the
[Mend Renovate app](https://developer.mend.io/github/lightspeedwp) on the Community (free) plan.

## How it works

The Mend app applies [inherited config](https://docs.renovatebot.com/mend-hosted/hosted-apps-config/)
from `org-inherited-config.json` in this repository to every repository the app is installed on.
Mend switches inheritance on for the organisation only after it sees a commit to that file.

Merge order, lowest to highest: Mend global config, then this file, then a repository's own
`renovate.json`. Repository-level settings do not remove inherited package rules: those rules can
still match updates and override scalar settings such as `automerge`.

To disable automerge while keeping update PRs enabled, a repository can add a later matching package
rule in its `renovate.json`:

```json
{
  "packageRules": [
    {
      "matchPackageNames": ["*"],
      "automerge": false
    }
  ]
}
```

## Policy

| Update | Behaviour |
| --- | --- |
| Minor and patch (not 0.x) | Merged by Renovate once all status checks pass |
| Digest, pin and lock-file maintenance | Merged by Renovate once all status checks pass |
| Major updates and 0.x versions | Left open for a human to review and merge |

Repositories without a `renovate.json` are processed without an onboarding PR
(`onboarding: false`, `requireConfig: "optional"`).

## Requirements per repository

- The Mend Renovate app must be installed on the repository.
- `platformAutomerge` is off: Renovate merges a PR itself, on a later run, once every status check
  is green. GitHub's native auto-merge is not used, because on a repository without required checks
  it merges the moment the PR opens, before CI has run.
- Branch protection with required status checks. Renovate automerges only when checks pass, so a
  repository with no checks gets no protection from a broken update.
- If branch protection requires an approving review, install the
  [renovate-approve](https://github.com/apps/renovate-approve) app on the organisation, or
  Renovate cannot automerge.
- A `renovate.json` only where a repository needs different behaviour.

Renovate checks repositories daily before 04:00 in the configured timezone. The four-hour window
matches the Mend Community job queue's roughly four-hour polling interval, so an update whose
three-day cooldown has elapsed is re-evaluated promptly and can automerge instead of waiting for
the next Monday. `internalChecksFilter: "strict"` keeps updates with a pending
`renovate/stability-days` check out of branches entirely; the only exception is Docker digest
updates for unversioned tags, which have no release timestamp to age against.

## Validate a change

```sh
npx --yes --package renovate -- renovate-config-validator --strict org-inherited-config.json
```

The `validate` workflow runs the same check on every pull request.
