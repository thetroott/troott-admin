# Contributing to Troott Admin

How to contribute to this repository. For product overview, setup, and environment variables, see **[README.md](./README.md)**.

## Scope

This checkout is the **admin / ops** surface of the creator–admin web portal (`@troott/web`). Prefer ops-facing changes here; shared portal code may also exist in sibling checkouts (`troott-studio`, `troott-web`, `troott-internal`).

Do not add listener-only mobile features or marketing-site content here.

## Branch structure

| Branch | Purpose |
| --- | --- |
| `master` | Production-ready code. Always stable. Protected. |
| `staging` | QA / testing branch for integrating features before a release. |
| `release/vX.Y.Z` | Pre-production branch for final testing before going live. |
| `@username/feature-*` | Feature branches under a personal namespace. |
| `@username/fix-*` | Bug-fix branches under a personal namespace. |

### Branch naming

| Type | Pattern | Example |
| --- | --- | --- |
| Feature | `@username/feature-<short-desc>` | `@topeokuselu/feature-admin-user-table` |
| Bug fix | `@username/fix-<short-desc>` | `@damolaoladipo/fix-admin-cors` |
| Release | `release/v<semver>` | `release/v1.0.2` |

> Use lowercase and hyphens. Be concise and descriptive.

## Development workflow

### 1. Clone (if you haven’t)

```bash
git clone https://github.com/thetroott/troott-admin.git
cd troott-admin
```

Follow [README.md](./README.md) for `npm install`, `.env`, and `npm run dev`.

### 2. Create a feature branch

Open a feature branch from `staging`:

```bash
git checkout staging
git pull origin staging
git checkout -b @username/feature-your-task-name
```

### 3. Develop

Make your changes, test locally, and commit often with clear messages. Keep UI on `@troott/ui` where possible.

### 4. Sync with staging

```bash
git fetch origin
git rebase origin/staging
```

### 5. Push

```bash
git push origin @username/feature-your-task-name
```

### 6. Open a PR into staging

Your pull request should target **`staging`**, not `master`.  
Reference the issue in the description (e.g. `Closes #502`).

After approval, merge into `staging` (via GitHub or locally as your team prefers).

### 7. Create a release branch

When ready for deployment:

```bash
git checkout staging
git pull origin staging
git checkout -b release/v1.0.2
git push origin release/v1.0.2
```

Final QA and bug-fixing happen on `release/*` before production.

### 8. Merge release into master and staging

```bash
git checkout master
git merge release/v1.0.2
git push origin master

git checkout staging
git merge release/v1.0.2
git push origin staging
```

## Creating an issue

If you discover a bug or have a suggestion, open a GitHub Issue (if you have permission), or notify your team lead for triage and assignment.

## Useful commands

| Command | Description |
| --- | --- |
| `npm run dev` | Dev server on port **5053** |
| `npm run build` | Production build |
| `npm start` / `npm run preview` | Preview production build |
| `npm test` | Vitest |
| `npm run lint` | ESLint |

## Pull request notes

- PRs should target the **`staging`** branch.
- Reference issues with `Closes #issue-number`.
- Add context and screenshots/logs when helpful.
- Request reviewers before merging.
- Call out API or CORS changes that need `troott-api` updates.
