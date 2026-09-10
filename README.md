# Troott Admin

### Platform operations for Troott discipleship infrastructure

> **Troott** helps ministers and teachers publish, organise, and distribute sermons. Listeners discover and stream content without the clutter of unmanaged downloads. **Troott Admin** is the staff-facing surface for platform operators (`ADMIN` / `SUPER`) to manage users, content, and operational workflows.

This repository is the **admin checkout** of the creator/admin web portal SPA. Sibling folders (`troott-studio`, `troott-internal`, `troott-web`) currently share the same Vite/React codebase and package name `@troott/web` until product splits are fully separated.

## Introduction

Platform operators need a reliable place to:

- Inspect and manage users, roles, and minister-scoped content.
- Support creator studios without using listener mobile builds.
- Operate uploads, moderation, and account workflows against the Troott API.

**Troott Admin** answers:

- How do staff administer sermons, ministers, and accounts safely?
- How do we keep ops UI on the same design system as studio (`@troott/ui`)?
- How do we point local and prod builds at the correct API origin?

## Technologies

- **TypeScript**
- **React 19**
- **Vite 6**
- **React Router 7**
- **TanStack Query**
- **Tailwind CSS 4**
- **Zustand**
- **Axios**
- **`@troott/ui`**
- **Uppy** (S3-oriented uploads)
- **Sentry / PostHog** (when `VITE_APP_ENVIRONMENT=prod`)

## Getting Started

### Prerequisites

- **Node.js** 20+
- **npm** (this app uses `package-lock.json`)
- Running **Troott API** (see `troott-api`) and MongoDB
- Optional: Docker for containerised preview

### 1. Clone and enter the app

```bash
cd troott-admin
```

### 2. Install dependencies

```bash
npm install
```

### 3. Environment

```bash
cp .env.sample .env
```

| Variable | Purpose |
| --- | --- |
| `VITE_APP_API_URL` | API **origin only** (no `/api` path). Client appends `/api/v1`. Sample: `http://localhost:5025` |
| `VITE_APP_ENVIRONMENT` | `development` locally; `prod` enables Sentry/PostHog/Speed Insights |
| `VITE_APP_PUBLIC_SENTRY_DSN` | Optional Sentry DSN |
| `VITE_APP_PUBLIC_POSTHOG_KEY` / `VITE_APP_PUBLIC_POSTHOG_HOST` | Optional analytics |
| `VITE_USE_REAL_API_UPLOAD` | Upload pipeline toggle |
| `VITE_DEPLOYMENT_REGION` | Upload region hint (e.g. `us-east-1`) |
| `VITE_TROOTT_*` | Store / desktop download URLs for get-troott flows |

> **Port note:** Client samples use API **`5025`**. `troott-api` `.env.example` defaults to **`8080`**. Set `PORT=5025` on the API or point `VITE_APP_API_URL` at `8080`.

### 4. Run development

```bash
npm run dev
```

App: **http://localhost:5053**

> `troott-admin`, `troott-studio`, `troott-internal`, and `troott-web` all default to **5053**. Run only one at a time, or change the Vite port.

### 5. Build and preview

```bash
npm run build
npm start
# or
npm run preview
```

Preview also serves on **5053** (or `$PORT`).

### 6. Test and lint

```bash
npm test
npm run lint
```

## Project structure

```text
troott-admin/
├── src/
│   ├── app/           # Feature surfaces (admin, studio, auth, get-started, …)
│   ├── api/           # HTTP client config and API modules
│   ├── components/    # Shared UI
│   ├── routes/        # Route trees
│   ├── context/       # React context
│   └── services/      # Client services
├── public/
├── scripts/           # Build / get-troott helpers
├── docs/
├── Dockerfile
├── Caddyfile
├── .env.sample
└── package.json       # name: @troott/web
```

## Scripts

| Command | Description |
| --- | --- |
| `npm run dev` | Vite dev server on **5053** |
| `npm run build` | Production bundle |
| `npm start` | Preview bundle (`vite preview`, port `$PORT` or 5053) |
| `npm test` | Vitest |
| `npm run lint` | ESLint |

## Integrations

| Integration | Notes |
| --- | --- |
| Troott API | `VITE_APP_API_URL` → `{origin}/api/v1` |
| `@troott/ui` | Design system + tokens |
| Uppy / S3 | Sermon and asset upload flows |
| Sentry / PostHog | Enabled when environment is `prod` |

## Contributing

Branching, PR targets, release flow, and contribution guidelines live in **[CONTRIBUTING.md](./CONTRIBUTING.md)**. PRs should target `staging`.

## Related apps

| App | Role |
| --- | --- |
| `troott-studio` | Creator / minister studio portal |
| `troott-internal` | Internal staff umbrella checkout |
| `troott-web` | Combined portal checkout |
| `troott-api` | HTTP API |
| `troott-website` | Public marketing site (`troott.com`) |
| `troott-ui` | Shared React design system |

## License

MIT (see repository `LICENSE` if present).
