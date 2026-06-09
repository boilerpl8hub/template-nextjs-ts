# template-nextjs-ts

Next.js 16 + TypeScript + Tailwind CSS + shadcn/ui + Zustand + Axios boilerplate.

## What's included

- **Next.js 16** — App Router, RSC, SSR
- **TypeScript** — strict mode
- **Tailwind CSS v3** — with shadcn/ui color system, dark mode, glass utilities, animation classes
- **shadcn/ui** — configured via `components.json`, add components with `npx shadcn add`
- **Zustand** — `useUserStore` (token auth + hydration), `useUIStore` (theme/sidebar), persisted to localStorage
- **Axios client** — `src/services/services.ts`: Bearer token injection, 401 auto-redirect, typed helpers (`getData`, `postData`, `patchData`, `putData`, `deleteData`, `postFormData`, `putFormData`)
- **next-themes** — ThemeProvider wrapping the app
- **framer-motion** — installed, used in 404/error pages
- **lucide-react** — icon library
- **Docker** — `Dockerfile` + `docker-compose.yml`
- **CI/CD** — GitLab CI (`.gitlab-ci.yml`) + GitHub Actions (`.github/workflows/ci-cd.yml`)

---

## Prerequisites

- Node.js 20+
- npm
- Docker & Docker Compose (for containerized dev/deploy)
- `gh` CLI (optional, for bootstrapping from template)

---

## Quickstart

```bash
# From template
gh repo create my-app --template boilerpl8hub/template-nextjs-ts --public
git clone https://github.com/YOUR_ORG/my-app
cd my-app

# Install deps
npm install

# Set up env
cp .env.local.example .env.local
# Edit .env.local with your values

# Run dev server
npm run dev
```

---

## Setup checklist

When starting a new project from this template, complete every item:

### Project identity
- [ ] Rename `"name"` in `package.json` from `template-nextjs-ts` to your project name
- [ ] Update `metadata.title` and `metadata.description` in `src/app/layout.tsx`
- [ ] Update `<html lang="en">` in `src/app/layout.tsx` if using a different language (e.g. `lang="fa" dir="rtl"`)
- [ ] Update `viewport.themeColor` in `src/app/layout.tsx` to your brand color
- [ ] Replace `NEXT_PUBLIC_SITE_URL` in `.env.local`

### Font
- [ ] `src/app/layout.tsx` uses Inter from Google Fonts — swap to your font if needed
- [ ] If using a local font: add files to `public/fonts/`, update `src/utils/fonts.ts`, update `globals.css` `--font-sans`

### Colors & theme
- [ ] `src/app/globals.css` — update `--background`, `--primary`, `--accent`, etc. for your brand colors in both `:root` and `.dark`
- [ ] `tailwind.config.ts` — add brand-specific color tokens in the `// Add brand colors here` section

### Zustand stores
- [ ] `src/store/useUserStore.ts` — add user fields you need (e.g. `username`, `email`, `role`)
- [ ] `src/store/useUIStore.ts` — remove/add state relevant to your app
- [ ] Update `name:` in both stores' `persist()` to your app name (e.g. `"myapp-user"`)

### API client
- [ ] `src/services/services.ts` — update `localStorage.getItem("user-storage")` key if you renamed the store
- [ ] Update the 401 redirect path (`/signin`) to your auth page route

### next.config.ts
- [ ] Add your image hosting domains to `remotePatterns`

### Docker
- [ ] `docker-compose.yml` — update `FRONTEND_REGISTRY_IMAGE` default value

### CI/CD — GitLab
Set these CI/CD variables in your GitLab project (Settings → CI/CD → Variables):

| Variable | Description |
|----------|-------------|
| `REGISTRY` | Docker registry hostname (e.g. `registry.hamdocker.ir`) |
| `REGISTRY_USERNAME` | Registry login username |
| `REGISTRY_PASSWORD` | Registry login password |
| `FRONTEND_REGISTRY_IMAGE` | Full image name (e.g. `registry.hamdocker.ir/myorg/frontend`) |
| `FRONTEND_ENV_FILE` | Path to `.env.local` stored as a GitLab File variable |
| `SSH_PRIVATE_KEY` | Private key for server SSH access |
| `SERVER_HOST` | Deployment server IP/hostname |
| `SERVER_USER` | SSH user (e.g. `root`) |
| `PAT` | Registry personal access token for server-side pull |
| `TELEGRAM_BOT_TOKEN` | (Optional) Telegram bot token for notifications |
| `TELEGRAM_CHAT_ID` | (Optional) Telegram chat ID |
| `TELEGRAM_BUILD_THREAD_ID` | (Optional) Telegram thread ID |
| `BALE_BOT_TOKEN` | (Optional) Bale bot token for notifications |
| `BALE_CHAT_ID` | (Optional) Bale chat ID |

### CI/CD — GitHub Actions
Set these secrets in your GitHub repo (Settings → Secrets → Actions):

| Secret | Description |
|--------|-------------|
| `REGISTRY` | Docker registry hostname |
| `REGISTRY_USERNAME` | Registry username |
| `REGISTRY_PASSWORD` | Registry password |
| `FRONTEND_REGISTRY_IMAGE` | Full image name |
| `ENV_LOCAL` | Contents of `.env.local` |
| `SSH_PRIVATE_KEY` | Private key for SSH deploy |
| `SERVER_HOST` | Server IP/hostname |
| `SERVER_USER` | SSH user |

---

## Project structure

```
src/
├── app/
│   ├── globals.css         # Tailwind base + CSS variables + utility classes
│   ├── layout.tsx          # Root layout: font, ThemeProvider, metadata
│   ├── page.tsx            # Home page (replace with your content)
│   ├── not-found.tsx       # 404 page
│   └── error.tsx           # Global error boundary
├── components/
│   ├── ThemeProvider/      # next-themes wrapper
│   └── ui/                 # shadcn components (add via `npx shadcn add`)
├── hooks/
│   └── use-mobile.tsx      # useIsMobile() hook
├── lib/
│   └── utils.ts            # cn() — clsx + tailwind-merge
├── services/
│   └── services.ts         # Axios client + typed HTTP helpers
├── store/
│   ├── useUserStore.ts     # Auth tokens, persisted to localStorage
│   └── useUIStore.ts       # UI state (theme, sidebar)
├── types/
│   └── apiTypes.ts         # GetParams, PostParams, etc.
└── utils/
    └── fonts.ts            # Font configuration
public/
└── fonts/                  # Put local font files here
```

---

## Environment variables

| Variable | Description | Example |
|----------|-------------|---------|
| `NEXT_PUBLIC_BACKEND_URL` | Backend API base URL (no trailing slash) | `http://localhost:8080` |
| `NEXT_PUBLIC_SITE_URL` | Public site URL for OG/SEO | `https://myapp.com` |

---

## Development

```bash
npm run dev        # Start dev server at http://localhost:3000
npm run build      # Production build
npm run start      # Start production server
npm run lint       # ESLint
```

---

## Build & Deploy

```bash
# Build Docker image
docker compose build

# Run locally
docker compose up

# Deploy (CI/CD handles this automatically)
```

### Adding shadcn components

```bash
npx shadcn add button
npx shadcn add input dialog select
```
