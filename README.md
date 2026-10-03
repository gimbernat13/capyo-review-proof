# Capyo ChatGPT Ads Pixel & ROAS — proof of resolution (requirement 2.1.3)

Review feedback (2026-10-01): during testing of the Plans page, selecting a paid plan led to a
web error ("There's no page at this address") instead of an interactive billing approval screen.

## Root cause

The app's plans in the Partner Dashboard were still configured under legacy manual pricing
(Billing API), while the in-app Plans screen links merchants to Shopify's hosted plan selection
page (Shopify App Pricing). With App Pricing not enabled for the app, the hosted plan selection
page returned a 404.

## Resolution

Completed Shopify's "Update to App Pricing" migration in the Partner Dashboard. Shopify App
Pricing is now the app's active pricing method, with the same three public plans (Free,
Growth $19/month or $190/year, Pro $39/month or $390/year, 7-day free trials). All billing,
trials and cancellations are handled by Shopify.

## Verified flow (screenshots above, modeled on the reviewer's screenshots)

1. `01-app-plans-page.png` — in-app Plans page: Free / Growth / Pro plan cards with
   "Choose this plan" buttons (mirrors screenshot 1).
2. `02-hosted-select-plan-page.png` — selecting a paid plan opens Shopify's hosted
   "Select a plan" page. This is the page that returned "There's no page at this address";
   it now renders the plan cards correctly (mirrors screenshot 2, resolved state).
3. `03-approve-charge-screen.png` — selecting the paid plan opens the interactive Shopify
   billing approval screen ("Approve charge"), where the merchant approves the
   Shopify-managed subscription. Charges are $0 on development stores.

Captured 2026-10-02 against the live app deployment on development store
kliq-demo.myshopify.com, and independently verified on a second development store with a
fresh install (Free plan, no subscription — matching the reviewer's starting state).
