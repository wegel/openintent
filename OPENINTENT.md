# OpenIntent project map

OpenIntent uses its own method. This map tells future humans and LLMs which repository sources control the project and which files merely realize or illustrate them.

## Sources and the choices they control

| Area | Human-owned source | Choices this source controls | Current realization or evidence |
| --- | --- | --- | --- |
| OpenIntent as a creative programming medium | `MANIFESTO.md` | The premise, vocabulary, tenets, and test that every OpenIntent feature must pass | All other project files and trials in real repositories |
| OpenIntent 0.1 | `README.md` | The current product surface: repository-native intent, two LLM roles, ordinary Git and CI, and human upstream approval | `skills/` and `templates/` |
| Adoption in varied projects | `README.md` and the applicable project's own intent | How OpenIntent enters a repository without forcing its sources into one schema | `templates/` and trials in adopting repositories |

`skills/` and `templates/` do not overrule the manifesto or the 0.1 choices in the README. They should change when real use exposes a better way to realize those sources.

Research, chat, issues, prototypes, and current tool behavior can inform a change. They control no lasting OpenIntent choice unless a human promotes that choice into `MANIFESTO.md`, `README.md`, or another source named here.

## How this repository changes

Use `$openintent-implement` for changes when that skill is available. Before review, reconcile the result with the final mapped sources. Then use `$openintent-review` from a separate context, run any relevant deterministic checks, and give a human the branch and evidence to judge.
