# Delta Xero Invoice Creation

![React](https://img.shields.io/badge/React-18-149ECA?logo=react&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-5-646CFF?logo=vite&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-Database-3FCF8E?logo=supabase&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-CSS-38B2AC?logo=tailwindcss&logoColor=white)
![License](https://img.shields.io/badge/license-Not%20specified-lightgrey)

A modern, responsive invoice management application built with React and Supabase. Create professional invoices, maintain customer and company details, preview documents, save drafts, and generate downloadable PDF invoices.

**Repository:** https://github.com/SagarChhetrii/Delta-Xero-Invoice-Creation

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Application Pages](#application-pages)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [Supabase Setup](#supabase-setup)
- [Available Scripts](#available-scripts)
- [Project Structure](#project-structure)
- [Deployment](#deployment)
- [Troubleshooting](#troubleshooting)
- [Security](#security)

## Features

- Secure sign-up, login, logout, and password-reset flows
- Create, edit, save, and delete invoices
- Invoice numbering and draft management
- Customer and company information forms
- Line-item and invoice-total calculations
- 10% demo tax calculation for draft and generated invoices
- Printable and downloadable invoice preview
- PDF generation with `@react-pdf/renderer`
- Invoice history with summary, filtering, pagination, and bulk actions
- Company profile, logo, preferences, account, and template settings
- Responsive desktop and mobile interfaces
- Real-time invoice change subscription
- Supabase authentication, database, storage, and row-level access

## Tech Stack

| Category | Technology |
| --- | --- |
| Frontend | React 18, Vite 5 |
| Routing | React Router 6 |
| Styling | Tailwind CSS, PostCSS |
| Backend | Supabase |
| Database | Supabase PostgreSQL |
| Authentication | Supabase Auth |
| PDF | React PDF Renderer |
| Forms | React Hook Form |
| Charts | Recharts, D3 |
| Animation | Framer Motion |
| Icons | Lucide React |

## Application Pages

| Route | Purpose |
| --- | --- |
| `/login` | Sign in to an existing account |
| `/signup` | Create a new account |
| `/invoice-creation-dashboard` | Create or edit an invoice |
| `/invoice-history-management` | Browse, filter, and manage saved invoices |
| `/invoice-preview-print-interface` | Preview, print, or export an invoice |
| `/company-settings-configuration` | Manage company, account, templates, and preferences |

## Getting Started

### Prerequisites

- Node.js 18 or newer
- npm
- A Supabase project

### Installation

```bash
git clone https://github.com/SagarChhetrii/Delta-Xero-Invoice-Creation.git
cd Delta-Xero-Invoice-Creation/frontend
npm install
```

### Run Locally

```bash
npm run dev
```

The development server is configured to run at:

```text
http://127.0.0.1:4028/
```

## Environment Variables

Copy the example file and add your Supabase project values:

```bash
cp .env.example .env
```

```env
VITE_SUPABASE_URL=https://your-project.supabase.co
VITE_SUPABASE_ANON_KEY=your-supabase-anonymous-key
```

The application requires both variables at startup. Do not use a Supabase service-role key in a browser environment.

Optional API and analytics variables can also be copied from `.env.example`:

```env
VITE_OPENAI_API_KEY=
VITE_GEMINI_API_KEY=
VITE_ANTHROPIC_API_KEY=
VITE_GOOGLE_ANALYTICS_ID=
VITE_ADSENSE_ID=
VITE_PERPLEXITY_API_KEY=
VITE_STRIPE_PUBLISHABLE_KEY=
```

## Supabase Setup

1. Create a project at [Supabase](https://supabase.com).
2. Open the SQL Editor in the Supabase dashboard.
3. Run the migration:

```text
frontend/supabase/migrations/20241216120000_invoice_app_with_auth.sql
```

4. Copy the project URL and anonymous key from **Project Settings > API**.
5. Add them to `frontend/.env`.
6. Ensure the `company-assets` storage bucket is created with appropriate public/private rules for company logos.
7. Confirm email authentication settings and redirect URLs match the environment where the app is running.

The migration is intended to set up the application's authentication-backed database tables and policies. Review it before applying it to an existing production database.

## Available Scripts

Run these commands from `frontend/`:

| Command | Description |
| --- | --- |
| `npm run dev` | Start the Vite development server |
| `npm run build` | Create a production build in `dist/` |
| `npm run preview` | Preview the production build locally |

## Project Structure

```text
frontend/
├── public/                 # Favicons and public assets
├── src/
│   ├── components/         # Shared UI and authentication components
│   ├── contexts/           # React context providers
│   ├── pages/              # Route-level application pages
│   ├── styles/             # Tailwind and global styles
│   ├── utils/              # Supabase and service helpers
│   ├── App.jsx
│   ├── Routes.jsx
│   └── index.jsx
├── supabase/
│   └── migrations/         # Database setup migration
├── .env.example
├── package.json
├── tailwind.config.js
├── vercel.json
└── vite.config.mjs
```

## Deployment

### Vercel

1. Import the GitHub repository in [Vercel](https://vercel.com).
2. Set the **Root Directory** to `frontend`.
3. Use these build settings:

```text
Framework preset: Vite
Build command: npm run build
Output directory: dist
Install command: npm install
```

4. Add `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` to Vercel environment variables.
5. Deploy the project.

The included `vercel.json` rewrites application routes to `index.html` for React Router.

### GitHub Pages

GitHub Pages can host this static build, but the app uses client-side routing and Supabase. Configure the Vite base path and Pages deployment workflow before publishing:

```js
// vite.config.mjs
export default defineConfig({
  base: "/Delta-Xero-Invoice-Creation/",
});
```

## Troubleshooting

### Missing Supabase variables

Make sure `frontend/.env` exists and contains both `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY`, then restart the Vite server.

### Port already in use

Start Vite on a custom port:

```bash
npm run dev -- --port 3000
```

### Build succeeds but routes return 404

Verify the hosting provider uses SPA fallback routing. The included Vercel configuration forwards all routes to `index.html`.

### Supabase authentication or database errors

- Confirm the Supabase project is active.
- Apply the included SQL migration.
- Check email confirmation and redirect settings.
- Verify the anonymous key and URL belong to the same project.
- Review table and storage policies for the signed-in user.

## Security

- Never commit `.env` or private credentials.
- The Supabase anonymous key is intended for browser use, but authorization must be enforced through Supabase RLS policies.
- Review and restrict storage and database policies before production use.
- Avoid placing OpenAI, Gemini, Anthropic, Stripe secret keys, or service-role credentials in Vite environment variables.

## Contributing

Contributions are welcome:

1. Fork the repository.
2. Create a feature branch.
3. Make your changes.
4. Run `npm run build`.
5. Open a pull request.
