# Agents

This document is **agent-specific** guidance for working in `clhbid/.github` — the org's shared
GitHub configuration: the issue forms in `.github/ISSUE_TEMPLATE/`, the pull request template, and
the org profile `README.md`. Every other repo inherits the issue forms from here, so this repo
never takes local templates of its own.

### Before Starting Work

1. Assign the issue to yourself — or to the person you are operating as — if that hasn't been
   done already, then set its `Status` to `In progress` on the CLHbid Delivery org project. See
   the `issue-tracker` skill for details.

### Before Finishing Work

1. If the change touches `.github/ISSUE_TEMPLATE/`, confirm it doesn't rename or remove the `bug`
   or `enhancement` categorization — GitHub silently drops a label an issue form applies if the
   repo filing against it doesn't have one by that exact name, and every repo without local
   templates files through these forms
1. Push the branch and open a pull request that references the issue it implements — see the
   `open-pr` skill
1. Request review from a human maintainer — see **How a run ends** below

### How a run ends

Passing checks is not finishing. Work is finished when a pull request exists and a human has been
asked to look at it, and every run ends in exactly one of these three states — see the `afk-loop`
skill for why, and how each gets reviewed:

| State        | Status             | What to do                                                                                                                                                                      |
| ------------ | ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Complete** | `Ready for Human`  | Open the pull request ready for review. Only claim this when checks pass, every acceptance criterion is addressed, and the agent brief is complete.                             |
| **Blocked**  | `Waiting on input` | Something you can't resolve would stop the pull request being merged. Leave it as a draft and comment with the specific question or action needed, and the steps to resolve it. |
| **Error**    | `Ready for Human`  | The run failed. Leave the pull request as a draft and comment with what failed, and if possible what action can be taken to resolve the issue.                                  |

## Devcontainer

No devcontainer here. A container exists to install the shared agent skills automatically; this
repo is templates and Markdown with no build, lint, or test step to run inside one, so a container
that existed solely to run an install script wouldn't pay for itself. Revisit if this repo grows
real tooling.

## Agent skills

The shared conventions are **installed, not committed**. They live in
[`clhbid/agent-context`](https://github.com/clhbid/agent-context). Without a devcontainer here,
nothing installs them automatically — run the install script from a
[`clhbid/clhbid.com`](https://github.com/clhbid/clhbid.com/blob/main/scripts/install-agent-skills.sh)
checkout instead:

```sh
./scripts/install-agent-skills.sh
```

It installs the skills globally for Claude Code. Pass an agent name to install them elsewhere, for
example `./scripts/install-agent-skills.sh copilot`, or `'*'` for every agent it detects.

| Skill           | What it covers                                                                                                                                                 |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `issue-tracker` | Issues via `gh`, the `Status` field and how to set it, the board query recipes, triage roles, cycles, labels, the commit convention, and how to decompose work |
| `afk-loop`      | Dispatching work to Copilot, reviewing what comes back, and handling a run that goes wrong                                                                     |
| `open-pr`       | Opening and updating a pull request                                                                                                                             |

**If you are reading this without those skills, you have everything you need.** A Copilot coding
agent runs in a container that has not installed them: the commands above, and **How a run ends**,
are the whole contract. Anything else is reference material for a person or a session with the
skills to hand — never a prerequisite for finishing an issue. If you find you needed something
that isn't here, say so on the pull request, so it can be added to this file rather than restored
as a copy of the docs.
