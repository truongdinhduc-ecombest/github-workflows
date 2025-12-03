# 📜 Contribution Guidelines & Release Workflow

This project leverages **GitHub Actions** to automate the creation of releases and changelogs. To ensure the generated release notes are accurate, professional, and useful, all team members **MUST** follow the guidelines below.

---

## 1. Branching Strategy

Always create a new branch from `main` (or `master`). Do not commit directly to the default branch.

**Naming Convention:** `type/short-description`

- **New Features:** `feat/user-auth`, `feat/dark-mode`
- **Bug Fixes:** `fix/ios-crash`, `fix/login-button`
- **Maintenance:** `chore/upgrade-deps`, `docs/update-readme`

---

## 2. Pull Request Rules (CRITICAL ⭐️)

The automation system reads the **Pull Request (PR) Title** and **Labels** to generate the changelog. The quality of your PR directly impacts the quality of our Release Notes.

### A. PR Title

The title will appear in the Changelog visible to stakeholders. It must follow the **Conventional Commits** format:

`type: description`

**Allowed Types:**

- `feat`: A new feature.
- `fix`: A bug fix.
- `chore`: Maintenance, config changes (no production code change).
- `refactor`: Code restructuring without behavioral changes.
- `docs`: Documentation only changes.
- `perf`: Performance improvements.

| ❌ DO NOT USE | ✅ DO USE                                      |
| :------------ | :--------------------------------------------- |
| `update code` | `feat: Add user dashboard layout`              |
| `fix bug`     | `fix: Resolve null pointer exception on login` |
| `refactor`    | `refactor: Optimize API response parsing`      |

### B. PR Labels (Mandatory)

You **MUST** assign at least one label to your PR using the right sidebar. This determines the category in the Changelog.

| Label                            | Description                   | Changelog Category     |
| :------------------------------- | :---------------------------- | :--------------------- |
| `breaking-change`                | Incompatible API changes      | 💥 Breaking Changes    |
| `feat`, `feature`, `enhancement` | New functionality             | ✨ New Features        |
| `fix`, `bug`                     | Bug fixes                     | 🐛 Bug Fixes           |
| `refactor`, `perf`               | Code/Performance improvements | ♻️ Code Refactoring... |
| `chore`, `docs`                  | Maintenance & Docs            | 🧰 Maintenance...      |
| `ignore-for-release`             | Exclude from changelog        | _(Hidden)_             |

> ⚠️ **Warning:** If no label is assigned, the PR will appear under **"Other Changes"**, which is untidy.

---

## 3. Merging Strategy

Reviewers should use **"Squash and merge"** when merging PRs.

- **Why:** This combines all intermediate commits (e.g., `wip`, `typo fix`) into a single, clean commit on the `main` branch.
- **Result:** The git history remains clean and aligns perfectly with the generated Changelog.

---

## 4. Release Process (For Maintainers)

Releases are fully automated. You do **not** need to manually draft releases on GitHub.

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

- GitHub Actions will trigger automatically.
- Within ~30 seconds, a new Release will be published under the **Releases** tab, complete with the auto-generated Changelog.

---

### ✅ Developer Checklist before creating a PR:

- [ ] Branch name follows convention (`feat/...`, `fix/...`).
- [ ] PR Title follows Conventional Commits (`feat: ...`).
- [ ] **Labels** are assigned. (Go back and add them if you forgot!)

---
