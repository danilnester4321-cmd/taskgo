# TaskGo MVP

Starter monorepo for a multilingual task marketplace (RU/EN/DE), designed for web + Android/iOS.
The included app is a **development MVP scaffold**. It supports task browsing/creation and application flows
when connected to Supabase. It does not move real money.

## Stack
- Next.js App Router + TypeScript (web/PWA foundation)
- Supabase Auth + PostgreSQL + Row Level Security
- Expo React Native can be added as a mobile client using the same API/contracts
- Future marketplace payments: Stripe Connect or another provider with country-specific marketplace support;
  PayPal payouts require a separately approved integration/provider flow.

## Quick start
1. Install Node.js 20+ and npm.
2. `npm install`
3. Copy `.env.example` to `.env.local` and fill Supabase project values.
4. Run `supabase/schema.sql` in Supabase SQL Editor.
5. `npm run dev`
6. Open http://localhost:3000

Without Supabase credentials, the UI displays a setup message rather than pretending data is persisted.

## Important money rules
- Never accept a client-provided commission, seller balance, payment status, or payout status.
- Compute commission on the server in integer euro cents: `commission = round(gross * 10%)`.
- Do not use floating-point values for money.
- A task is payable only after a provider-confirmed payment event.
- Release/payout only after an authorized completion/acceptance flow.
- Use an immutable ledger and idempotency keys for every financial event.
- Do not treat a database wallet number as stored cash. It is an accounting view of provider-confirmed ledger entries.
- Real payment integration is intentionally disabled in this scaffold.

## Suggested next implementation steps
1. Configure Supabase Auth email verification and production redirect URLs.
2. Add moderation, report/block flows, dispute workflow, rate limits and audit logs.
3. Add payment provider Connect onboarding and webhook verification after legal/provider review.
4. Add a separate Expo app in `apps/mobile` and reuse the API.
5. Complete GDPR/DSA/DAC7 and consumer/payment-services review for launch countries.

## Scripts
- `npm run dev` — local development
- `npm run build` — production build check
- `npm run lint` — lint
