# mediamate-dev/.github

Fælles GitHub Actions for MediaMates repos. Logikken ligger her, så en rettelse rammer
alle repos på én gang. Hvert repo har kun små workflows, der kalder herind.

| Workflow | Hvad den gør | Kopiér til repoet |
|---|---|---|
| [`opengrep.yml`](.github/workflows/opengrep.yml) | Statisk kodeanalyse (SAST) med [Opengrep](https://github.com/opengrep/opengrep) på pull requests og push | [`standard/opengrep.yml`](standard/opengrep.yml) → `.github/workflows/opengrep.yml` |
| [`zap-baseline.yml`](.github/workflows/zap-baseline.yml) | Passiv OWASP ZAP-scanning af et site. Kører kun, når repo-variablen `ZAP_TARGET` er sat | [`standard/zap.yml`](standard/zap.yml) → `.github/workflows/zap.yml` |
| [`ok-merge.yml`](.github/workflows/ok-merge.yml) | Merger en Dependabot-PR på en kommentar fra en godkender, når alle checks er grønne | [`standard/ok-merge.yml`](standard/ok-merge.yml) → `.github/workflows/ok-merge.yml` |
| – | Dependabot-opsætning | [`standard/dependabot.yml`](standard/dependabot.yml) → `.github/dependabot.yml` |

## Opsætning i et repo

- **Opengrep:** ingen opsætning. Reglerne ligger i [`opengrep/`](opengrep/).
- **ZAP:** sæt repo-variablen `ZAP_TARGET` til sitets adresse.
- **OK merge:** sæt repo-variablen `OK_MERGE_APPROVERS` til de GitHub-brugere, der må
  godkende, adskilt af mellemrum. Uden den afvises alle. Repoets deploy-workflow skal kunne
  startes med `workflow_dispatch`, fordi en merge lavet af en workflow ikke selv starter andre
  workflows.

Falske fund fra Opengrep undtages på linjen med en begrundelse:
`// nosemgrep: <regel-id> — <hvorfor det er sikkert>`.
