---
name: firstpromoter-integrate
description: Integrate FirstPromoter affiliate and referral tracking into a website or app. Use when adding FirstPromoter to a codebase, setting up click, signup/referral or sales tracking, connecting a billing provider (Stripe, Chargebee, Paddle, Recurly, Braintree) or the Tracking API, or debugging why clicks, referrals or sales are not being tracked.
license: MIT
metadata:
  author: FirstPromoter
  version: "1.0.0"
---

# Integrate FirstPromoter

Set up FirstPromoter so every affiliate click, signup and sale in this project is tracked and credited to the right affiliate, then prove it works with an end-to-end test.

## Sources of truth

These docs are always more current than this skill. Fetch the page you need before writing code; do not guess snippets or endpoints.

- Index of every docs page: https://docs.firstpromoter.com/llms.txt
- Website integration guide: https://docs.firstpromoter.com/guides/integrate-your-website
- fpr.js reference: https://docs.firstpromoter.com/script-docs/fpr-js-docs
- Framework examples (Next.js, React, Vue...): https://docs.firstpromoter.com/integrations/tracking/custom/js
- Tracking without fpr.js (server only): https://docs.firstpromoter.com/guides/tracking-without-fprjs
- Billing providers: https://docs.firstpromoter.com/integrations/billing/stripe (also `chargebee`, `paddle`, `recurly`, `braintree`, `api`)
- Ad-blocker proxy: https://docs.firstpromoter.com/guides/proxy-setup

If the FirstPromoter MCP server (`https://mcp.firstpromoter.com`) is connected, use it to read the account's real settings instead of asking the user. It is optional for this skill.

## Workflow

### 1. Inspect the project

Find out, from the code, before asking anything:

- **Framework and where `<head>` is rendered** (plain HTML, Next.js app/pages router, Nuxt, React/Vite SPA, Rails/Django templates, WordPress...).
- **The signup success point**: the callback, server action or thank-you page that runs *after* a user account or lead is created.
- **The billing provider**: look for `stripe`, `chargebee`, `paddle`, `recurly`, `braintree` SDKs, keys or webhooks.
- **Whether marketing site and app are separate** (different repos or domains). Click tracking goes on every public page; referral tracking goes where signup completes.

### 2. Get the Account ID

The Account ID is public (it ships in the page). Get it from MCP `get_integrations`, or ask the user to copy it from **Settings → Integrations** in the FirstPromoter dashboard. Put it in the project's existing public config or env pattern (for example `NEXT_PUBLIC_FPR_CID`) rather than hard-coding it in several places.

The API key is secret. Never commit it, print it or put it in client-side code. Read it from a server-side environment variable (for example `FIRSTPROMOTER_API_KEY`) and tell the user to set it.

### 3. Click tracking

Add the fpr.js snippet from the website integration guide to the `<head>` of **every public page**, using the framework pattern from the docs (for Next.js, Nuxt and SPAs follow the framework example page; for GTM follow the GTM guide). It loads async and must be on all pages, not just the homepage, because affiliates can link anywhere.

### 4. Referral (signup) tracking

Call `fpr("referral", {email, uid})` **after** signup succeeds:

- Pass the user's real email. Also pass `uid` when you have a stable ID at that point; prefer the billing provider's customer ID (for example the Stripe `cus_...` ID) so later sales match even if the email changes.
- Do not call it before the account exists, and do not redirect in the same tick: the browser can cancel the request. If the flow redirects immediately, put the call on the confirmation page.
- Server-only signup flows: use the Tracking API signup endpoint from the backend instead (see "Tracking without fpr.js").

### 5. Sales tracking

- **Supported billing provider**: connecting it is a dashboard step, not code. Tell the user to connect it at **Settings → Integrations**. In code, make sure the customer created in the billing provider has the same email (or the `uid` you sent) as the referral. For Stripe Checkout, Payment Links or Pricing Table, follow the matching Stripe page in the docs.
- **Other or custom billing**: send a sale from the backend when payment is confirmed, using the Tracking API `POST /api/v2/track/sale` with the `Account-ID` header and `Authorization: Bearer <API key>`. `sale_amount` is in **cents**. Always send `event_id` (the transaction ID): it is required to avoid duplicate sales on retries. Track refunds too if the provider supports them.

### 6. Test end to end

Walk the user through, and verify with MCP where available:

1. Open an affiliate's referral link; confirm the click (MCP `get_integrations` shows when the last click was tracked).
2. Sign up as a test user through that link; confirm a new lead appears (MCP `list_referrals`, newest first).
3. Make a test purchase (Stripe test mode / test card); confirm the sale and commission appear (MCP `get_referral` shows the event log, `list_commissions`).
4. Check the browser console for errors. Most failures are a wrong Account ID, the referral call running before fpr.js loaded, or an ad blocker (offer the proxy setup).

## Finish

Summarize for the user: files changed, env vars they must set, dashboard steps still to do (billing connection), and the test results. Do not mark the integration done until a test referral and a test sale have been seen in FirstPromoter.
