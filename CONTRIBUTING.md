# Contributing to VistaOps

Thanks for your interest in contributing to **VistaOps** 🚀  
This guide outlines the workflow and conventions we follow to keep the project consistent and maintainable.

---

## 📂 Branch Naming Conventions

To keep the repository organized and maintain a clear history, we use the following branch naming conventions:

- **`feature/<short-description>`**  
  For new features or enhancements.  
  _Example:_ `feature/laundry-status-tracking`

- **`bugfix/<short-description>`**  
  For fixing bugs that are not urgent production issues.  
  _Example:_ `bugfix/footer-hover-style`

- **`chore/<short-description>`**  
  For maintenance tasks, refactoring, dependency upgrades, or setup.  
  _Example:_ `chore/setup-ci-pipeline`

- **`hotfix/<short-description>`**  
  For urgent fixes that need to be patched into production immediately.  
  _Example:_ `hotfix/api-timeout-issue`

- **`release/<version>`**  
  For preparing production releases, tagging versions, or staging.  
  _Example:_ `release/v1.0.0`

- **`docs/<short-description>`**  
  For documentation updates or changes to project files.  
  _Example:_ `docs/update-readme`

---

## ✍️ Commit Message Guidelines

We follow a simple convention for commit messages to make history easy to scan:

- **Format:** `<type>(<scope>): <message>`
- **Types:** `feat`, `fix`, `chore`, `docs`, `refactor`, `style`, `test`

**Examples:**

- `feat(auth): add shared passcode flow for MVP`
- `fix(ui): correct footer hover underline`
- `docs(readme): update deploy section`
- `chore(deps): bump aws-sdk version`

---

## 🔀 Pull Request Process

When submitting a PR:

1. **Branch from `main`** (or `release/*` for hotfixes).
2. Use the PR template provided in [`.github/pull_request_template.md`](.github/pull_request_template.md).
3. Include:
   - **Context**: why this change is needed
   - **Changes**: what was done
   - **Testing**: how it was verified
   - **Risks & Rollback plan**
4. Keep PRs **focused**. Avoid mixing unrelated changes.
5. Update documentation (README, code comments) if needed.

---

## ✅ Code Style

- Use **clear, descriptive names** for variables, functions, and components.
- Keep functions small and focused — one responsibility per function.
- Follow the existing **CSS modular structure** (`/web/styles/`).
- For JS/TS: use **Prettier defaults** (2 spaces, semicolons, trailing commas).
- No secrets or keys in code. Use `.env` (gitignored) for configuration.

---

## 🔍 Testing & Verification

Before submitting a PR:

- Run the app locally and verify:
  - `open web/index.html` (or `npx http-server web`)
  - UI renders without console errors
  - Favicon + assets load correctly
  - Footer and links behave as expected
- For deploy-related changes:
  - Run `./deploy.sh --dry-run`
  - Confirm only expected files are uploaded/removed
  - Verify CloudFront invalidation runs if needed

---

## 👀 Code Review Guidelines

- Keep reviews respectful and constructive.
- Focus on **functionality, security, and clarity**.
- Approve when:
  - The branch follows naming conventions
  - Commit messages are clean
  - PR template is filled out
  - Tests/verification steps are documented
- Request changes if:
  - Secrets/keys are exposed
  - PHI compliance rules are violated (only first names allowed)
  - Documentation is missing or outdated

---

## 📜 License & Usage

This project is provided for **portfolio and demonstration purposes only**.  
All rights reserved © 2025 Sayeed Joseph.

---
