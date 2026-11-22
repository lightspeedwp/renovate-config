# renovate-config

Organisation-wide Renovate configuration for the `lightspeedwp` GitHub organisation, run by the
[Mend Renovate app](https://developer.mend.io/github/lightspeedwp) on the Community (free) plan.

## How it works

The Mend app applies [inherited config](https://docs.renovatebot.com/mend-hosted/hosted-apps-config/)
from `org-inherited-config.json` in this repository to every repository the app is installed on.
Mend switches inheritance on for the organisation only after it sees a commit to that file.

Merge order, lowest to highest: Mend global config, then this file, then a repository's own
`renovate.json`. A repository's own config overrides anything set here.

## Policy

| Update | Behaviour |
| --- | --- |
| Minor, patch, pin, digest (version 1.0 or later) | Automerged once all status checks pass |
| Major, or any update to a 0.x version | Pull request for review |
| `lightspeed-hosting-infra` | Never automerged; merged through its own review gate |

Repositories without a `renovate.json` are processed without an onboarding PR
(`onboarding: false`, `requireConfig: "optional"`).

## Requirements per repository

- The Mend Renovate app must be installed on the repository.
- Branch protection with required status checks. Renovate automerges only when checks pass, so a
  repository with no checks gets no protection from a broken update.
- If branch protection requires an approving review, install the
  [renovate-approve](https://github.com/apps/renovate-approve) app on the organisation, or
  Renovate cannot automerge.
- A `renovate.json` only where a repository needs different behaviour.

## Validate a change

Validate it as repository config from a scratch directory:

```sh
cp org-inherited-config.json "$SCRATCH/renovate.json" && cd "$SCRATCH"
npx --yes --package renovate -- renovate-config-validator --strict
```

Expect exactly two errors, for `onboarding` and `requireConfig`. Both are global options that a
repository file may not set, but inherited config may. Any other error is real.
