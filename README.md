# 📜 Contribution Guidelines & Release Workflow

This project leverages **GitHub Actions** to automate the creation of releases and changelogs. To ensure the generated release notes are accurate, professional, and useful, all team members **MUST** follow the guidelines below.

---

## 1. Branching Strategy

Always create a new branch from `main` (or `master`). Do not commit directly to the default branch.

**Naming convention:** `type/short-description`

- **New features:** `feat/user-auth`, `feat/dark-mode`
- **Bug fixes:** `fix/ios-crash`, `fix/login-button`
- **Maintenance:** `chore/upgrade-deps`, `docs/update-readme`

**📖 Reference:** [Conventional Branch Naming](https://conventional-branch.github.io/)

---

## 2. Pull Request Rules (CRITICAL ⭐️)

The automation system reads the **Pull Request (PR) Title** and **Labels** to generate the changelog. The quality of your PR directly impacts the quality of our Release Notes.

### A. PR Title

The title will appear in the changelog visible to stakeholders. It must follow the **Conventional Commits** format:

`type: description`

**Allowed types:**

- `feat`: A new feature.
- `fix`: A bug fix.
- `chore`: Maintenance, config changes (no production code change).
- `refactor`: Code restructuring without behavioral changes.
- `docs`: Documentation only changes.
- `perf`: Performance improvements.

| ❌ Do not use | ✅ Do use                                      |
| :------------ | :--------------------------------------------- |
| `update code` | `feat: Add user dashboard layout`              |
| `fix bug`     | `fix: Resolve null pointer exception on login` |
| `refactor`    | `refactor: Optimize API response parsing`      |

**📖 Reference:** [Conventional Commits](https://www.conventionalcommits.org/)

### B. PR Labels (Mandatory)

You **MUST** assign at least one label to your PR using the right sidebar. This determines the category in the changelog.

| Label                                                  | Description                     | Changelog Category                |
| :----------------------------------------------------- | :------------------------------ | :-------------------------------- |
| `breaking-change`, `breaking`                          | Incompatible API changes        | 💥 Breaking Changes               |
| `feat`, `feature`, `enhancement`                       | New functionality               | ✨ New Features                   |
| `fix`, `bug`                                           | Bug fixes                       | 🐛 Bug Fixes                      |
| `refactor`, `perf`, `style`                            | Code improvements & refactoring | ♻️ Code Refactoring & Performance |
| `build`, `chore`, `ci`, `dependencies`, `docs`, `test` | Maintenance & Documentation     | 🧰 Maintenance & Documentation    |
| `ignore-for-release`                                   | Exclude from changelog          | _(Hidden)_                        |

> ⚠️ **Warning:** If no label is assigned, the PR will appear under **"Other Changes"**, which is untidy.
> 💡 **Note:** Bots like `dependabot` and `renovate-bot` are automatically excluded from changelog.

---

## 3. Merging Strategy

Reviewers should use **"Squash and merge"** when merging PRs.

- **Why:** This combines all intermediate commits (e.g., `wip`, `typo fix`) into a single, clean commit on the `main` branch.
- **Result:** The git history remains clean and aligns perfectly with the generated changelog.

---

## 4. Release Process (For Maintainers)

Releases are fully automated via GitHub Actions. You do **not** need to manually draft releases on GitHub.

**Workflow:**

1.  Ensure the `main` branch is stable.
2.  Determine the next version number (Semantic Versioning: `vMajor.Minor.Patch`).
3.  Create and push a tag:

```bash
# Example: Releasing version 1.0.0
git checkout main
git pull origin main

# 1. Create tag
git tag v1.0.0

# 2. Push tag to trigger automation
git push origin v1.0.0
```

🚀 **What happens next?**

- The `Auto release on tag` GitHub Actions workflow triggers automatically.
- Within ~30 seconds, a new release will be published under the **Releases** tab with:
  - Auto-generated changelog based on PR labels and titles
  - Release notes organized by category (Breaking Changes, Features, Bug Fixes, etc.)
  - Support for prerelease versions (tags containing `-` are marked as prerelease)

**📖 Reference:** [Semantic Versioning](https://semver.org/)

---

## 5. GitHub Actions Workflows

This repository includes automated workflows:

### **auto-release.yml**

- **Trigger:** When a tag matching `v*` is pushed
- **Action:** Automatically creates a GitHub release with auto-generated changelog
- **Permissions:** `contents: write` to create releases

### **sync-labels.yml**

- **Trigger:** When `.github/labels.yml` is modified on `main` branch (or manually via `workflow_dispatch`)
- **Action:** Syncs all defined labels to the repository
- **Permissions:** `issues: write` to manage labels

### **Label syncing**

All PR labels are defined in `.github/labels.yml` and automatically synced to your repository. These labels directly impact changelog categorization.

---

### ✅ Developer checklist before creating a PR:

- [ ] Branch name follows convention (`feat/...`, `fix/...`).
- [ ] PR Title follows Conventional Commits (`feat: ...`, `fix: ...`, etc.).
- [ ] **At least one label** is assigned from the available labels.
- [ ] If breaking changes, ensure `breaking-change` label is added.

---
