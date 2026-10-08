# Repository Guardrails & Setup Checklist

A comprehensive setup checklist designed to establish strict, automated guardrails for both human and AI contributors when initializing a new repository.

---

## License

This project is released under the MIT License. See [LICENSE](LICENSE) for full terms.

## Contributing

Contributions are welcome, but all pull requests must be reviewed and approved by @glennfaison or another code owner listed in [CODEOWNERS](CODEOWNERS) before merge.

## 1. Branching Strategy & Naming Conventions

- [ ] **Define branching rules:** Select and document the team's branching strategy (e.g., standard Gitflow or Trunk-Based Development).
- [ ] **Branch name validation script:** Create a script (e.g., `scripts/verify-branch-name.sh` or Node.js equivalent) that checks branch names against standard naming patterns (e.g., `feature/*`, `bugfix/*`, `hotfix/*`, `release/*`).
- [ ] **Prevent local non-compliant branch creation:** Configure local tooling or aliases/wrapper scripts that fail early when attempting to checkout or create non-compliant branch names.
- [ ] **Pre-push branch validation hook:** Configure a Git pre-push hook (via Husky or native `.git/hooks`) that runs the branch verification script and aborts pushes for non-compliant branch names.

---

## 2. Local Hooks & Verification

- [ ] **Pre-push build check:** Add a local `pre-push` script/hook to verify that the debug build compiles cleanly without errors before sending code to the remote repository.
- [ ] **Pre-push smoke test suite:** Configure a fast-running smoke test suite execution in the `pre-push` hook to catch regressions locally before pushing.

---

## 3. Remote Governance & GitHub Rulesets

- [ ] **Branch protection / Rulesets:** Configure GitHub Repository Rulesets or Branch Protection Rules on primary branches (`main`, `develop`):
  - [ ] Require Pull Requests before merging.
  - [ ] Block direct pushes to protected branches.
  - [ ] Require linear history or specific merge strategies (e.g., squash merging).
  - [ ] Enforce status checks to pass prior to merging.
- [ ] **Custom branch pattern enforcement:** Add GitHub targeting rulesets for custom branch patterns if extended beyond standard defaults.

---

## 4. Continuous Integration & Workflows

- [ ] **CI build & test workflows:** Set up GitHub Actions workflows triggered on PRs and pushes:
  - [ ] Execute full unit, integration, and end-to-end test suites.
  - [ ] Validate release/debug build configurations across targeted environments.
- [ ] **Static code analysis & linting:**
  - [ ] Configure code formatters (e.g., Prettier) and strict linters (e.g., ESLint / Biome).
  - [ ] Enforce module boundary rules (e.g., via `eslint-plugin-boundaries`, Nx module boundary rules, or language-native access controls) to prevent invalid cross-module imports and exposure of private internal code.
  - [ ] Enforce strict compiler and type checks (e.g., TypeScript `strict: true`, no implicit `any`).
