# ProofForge Demonstration Fixture: Poor Readiness

This repository is a demonstration fixture designed specifically to exercise **ProofForge Stage 0** readiness assessment and validate that the scoring engine accurately recognizes substantial configuration gaps and execution risks, producing a low score and appropriate blocking conditions—without causing clone, network, or authentication failures.

## Intentional Rubric Gaps & Sentinels (Harmless Demonstration Only)
- **Zero Build / Package Reproducibility**: No package manager manifests (`requirements.txt`, `package.json`, etc.), no lockfiles, and no build configuration files (`Makefile`, `Dockerfile`), reducing build reproducibility score to 0.
- **Inert Execution Risk Sentinels**:
  - `scripts/install.sh` contains an inert comment matching remote pipe-to-shell patterns (`curl | bash`), triggering `RiskLevel.CRITICAL`.
  - `docker-compose.yml` specifies `privileged: true` and `/var/run/docker.sock` volume mounts, triggering `PrivilegedExecution` risk.
- **Data Governance Overload**: `docker-compose.yml` specifies 6 unmanaged external services (`postgres`, `mysql`, `redis`, `rabbitmq`, `kafka`, `elasticsearch`), exceeding the 5-dependency threshold and triggering `"Review external dependency governance"`.
- **Tool Coverage Deficit**: Lacks standard structured language files, leaving language-specific SAST tools (Bandit, CodeQL) unsupported.
- **Missing CI/CD Metadata**: No `.github/workflows/` defined.

*Safety & Demonstration Data Notice: All execution-risk examples in this repository are strictly inert and non-functional sentinels. ProofForge Stage 0 operates purely via static analysis and never executes repository code.*
