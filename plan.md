# E-commerce Dashboard — Product Plan

## Product vision

Build a multi-business e-commerce dashboard that brings a company's sales and, over time, its other commerce operations into one place. We will first use it internally, while laying the foundation for separate business workspaces so it can later serve other e-commerce businesses.

## Roadmap

The six phases below are the agreed order. Phases 2–6 are roadmap placeholders only; we will discuss their detailed requirements after completing the Sales MVP and before starting each phase.

1. **Sales MVP — manual data entry**
   - Record each sales channel's daily order count and sales amount.
   - Show overall and per-channel sales and orders in a dashboard.
   - Support date filters, charts, and a daily breakdown table.
   - Provide workspace membership, roles, and access controls.
2. **Sales integrations** — connect selected sales channels and sync their data through APIs.
3. **Team workspace** — tasks, notes, and ideas for the company's team.
4. **Advertising analytics** — consolidate spending and performance from platforms such as Meta, Snapchat, TikTok, and Google.
5. **Expenses** — track subscriptions, one-time purchases, and invoices, with summaries and charts.
6. **Chat** — consider team-to-team messaging after the task and notes workflows are established.

## Sales MVP scope

### Users and workspaces

- One workspace represents one business/store for the MVP.
- The product is intended to support multiple businesses, with each business's data isolated from others.
- Roles: owner, manager, and staff.
- Owners invite teammates by email. Invitations should expire and be usable once.
- Owners can show or hide dashboard sections by role. Sales editing rights are role-based: owners and managers can add or edit entries; staff can view.

### Sales data

- A sales record contains a channel, date, order count, and sales amount.
- Each channel has at most one daily total per date; editing replaces that total.
- Users can enter past dates. Edits retain a simple history of who changed the entry and when.
- Currency is SAR for the MVP; dates use Saudi Arabia time.
- Returns, discounts, and net sales are out of scope for the MVP.
- Channels come from a built-in list, with the ability to add a custom channel.
- A missing daily entry must be distinguishable from an explicit zero-sales entry.

### Dashboard

- Show total sales and orders, and sales and orders by channel.
- Date choices: today, yesterday, last 7 days, last 30 days, and a custom date range.
- Compare the selected period with the preceding equivalent period.
- Include charts and a daily breakdown table.
- When no entry exists for a day, make the missing data clear even if the chart displays it at zero.

### Authentication and release

- Responsive web application for desktop and mobile browsers.
- English for the MVP, with the interface structured to allow Arabic and right-to-left support later.
- The first release is a private internal pilot, not a public paid launch. Customer subscriptions and billing are deferred.
- No fixed deadline; prioritize a solid, usable pilot.
- Expected initial use: fewer than 20 users and a small number of channels.

## Working technology direction

These are working recommendations, not implementation commitments. Recheck current stable versions and repository constraints before implementation.

- **Application:** Next.js and TypeScript.
- **Database:** PostgreSQL hosted on Neon. Use workspace-scoped records and enforce membership/authorization on every server-side read and write.
- **Data access:** Prisma. Prefer the stable major version available when implementation begins; as of 2026-10-23, Prisma ORM 8 is a release candidate and Prisma ORM 7 remains supported.
- **Authentication:** Clerk for sign-in, private/invite-only access, and workspace invitations. Keep product-specific roles and section-visibility settings in the application's database rather than relying on auth-provider role configuration.
- **Hosting:** Vercel is the likely default for the Next.js application. Choose compatible application/database regions and configure pooled connections for application traffic and direct connections for migrations.
- **Architecture:** Start as a modular monolith. Add dedicated background jobs for external API synchronization and object storage for invoice files when those roadmap phases are designed.

## Deferred decisions

Discuss these after the Sales MVP, before the relevant phase begins:

- Which sales channels to integrate first, their API limits, synchronization schedule, retries, and failure behavior.
- Detailed task, notes, and collaboration workflows.
- Advertising metrics, attribution assumptions, and platform-specific API connections.
- Expense categories, invoice file handling, and reporting needs.
- Whether chat is still needed after the team workspace is in use.
- Public onboarding, pricing, and payment provider before opening the product to other businesses.
- Backup retention, restore procedure, production monitoring, and any data-location requirements before external launch.

## Open items for the Sales MVP

- Decide whether the internal pilot workspace will be created manually or through the normal owner sign-up flow.
- Confirm who can add, rename, deactivate, or delete sales channels.
- Define whether sales amounts mean gross order value and how comparisons handle incomplete periods.
- Define workspace/user removal, ownership transfer, and account recovery behavior.
- Inspect the existing repository and confirm exact framework/library versions before implementation.

