# PakBooks

Accounting and business operations for small and medium businesses, built with
Pakistan in mind. Sales, purchases, inventory, tax, banking, payroll and
approvals in one double-entry application that you can run on your own computer,
on a Chromebook, or on your own cloud server.

## Download

Get the latest package from the
[releases page](https://github.com/riyanimran12-lab/pakbooks/releases/latest):

- **PakBooks.zip** — everything: the Windows program, the Chromebook edition, the
  cloud edition and a six-page guide
- **PakBooks-Editions-Guide.pdf** — the same steps as a printable document

## Editions

The same program ships in three forms:

| Edition | Runs on | How it is delivered |
| --- | --- | --- |
| Windows | A normal Windows PC | Portable folder with `PakBooks.exe` — no installer, no server |
| ChromeOS | A Chromebook | Source plus `deploy/chromebook/setup.sh`, built once inside the Linux environment |
| Cloud | An Ubuntu server (e.g. Oracle free tier) | Source plus `deploy/oracle/setup.sh`; serves an https website |

Each edition keeps its own data. Move books between them with a backup file.

## Features

- **Sales and purchases** — quotations through invoices and bills, with tax and
  other charges per line, returns and credit/debit notes.
- **Inventory** — units of measure, weighted-average costing, stock movements,
  valuation and reorder insight.
- **Tax** — sales tax and withholding configured as effective-dated rates, never
  hard-coded; tax periods, annexure exports, filing reminders and carry-forward.
  The e-invoice module is an integration point, not a certification.
- **Banking and cash** — bank accounts with consolidation, statement import,
  cashbook close, POS shifts and held sales.
- **Payroll** — employees, salary structures, overtime, employer contributions,
  payslips, and posting to the ledger.
- **Approvals** — maker-checker on sensitive actions, multi-level chains,
  delegations, and notifications.
- **Multi-currency** — configurable currencies, effective-dated FX rates, foreign
  settlement with realised gain/loss, unrealised exposure.
- **Reporting** — trial balance, P&L, balance sheet, ledgers with drill-down,
  ageing, dashboards, Excel import and export, printable documents.
- **Workspace** — companies, roles and permissions, two-factor authentication,
  password reset, audit trail, live FX widget, AI-assisted draft preparation.
- **Backups** — full database backup download and upload/restore from the app,
  plus command-line scripts for each edition.

## Accounting rules the code enforces

- Posted records are never edited or deleted. Corrections are reversals or
  credit/debit notes.
- AI never posts. It only prepares drafts for a human to review and post.
- Money is calculated with decimal arithmetic, never floating point.
- Tax rates and FX rates are effective-dated configuration, not code.
- Every query is scoped to the signed-in company; workspaces are isolated.
- Every posting posts to the general ledger or it does not post at all.

## Technology

- **API** — Fastify 5, TypeScript, Drizzle ORM, PostgreSQL-compatible embedded
  PGlite by default (no database server needed), Zod validation, Vitest.
- **Web** — Next.js 16 App Router, React 19, standalone build, server actions.
- **Shared** — a typed package of DTOs and contracts used by both apps.
- **Monorepo** — npm workspaces (`apps/api`, `apps/web`, `packages/shared`).

## Run from source

Requires Node.js 20.9 or newer.

```bash
npm install
npm run dev
```

Web on <http://127.0.0.1:3000>, API on <http://127.0.0.1:4000>. The database is
created on first start under `apps/api/.data`. Create your own account on the
sign-in page — there is no demo login and no sample company.

Production build:

```bash
npm run build
npm start
```

Other useful commands:

```bash
npm test          # shared + API test suites
npm run typecheck
npm run lint
npm run db:seed   # seed a fresh database
```

## Deploy scripts

- `deploy/windows/` — `Backup-PakBooks.cmd` and `Restore-PakBooks.cmd`
- `deploy/chromebook/` — `setup.sh`, `start.sh`, `stop.sh`, `backup.sh`, `restore.sh`
- `deploy/oracle/` — `setup.sh`, `status.sh`, `update.sh`, `backup.sh`, `restore.sh`

## Status

Phases 0 through 5 are implemented and covered by an automated test suite.
Production hardening work is ongoing.

## Disclaimer

PakBooks helps you keep books and prepare documents. It does not file returns
with any authority, does not act as a certified tax or e-invoicing solution, and
is not affiliated with any government body. Check your obligations with a
qualified professional.
