# QueueLess — Smart Canteen Management

A responsive campus canteen ordering prototype. Students can browse a menu, build a bag, place an order, receive a digital pickup token and track its kitchen status. The admin workspace can update order statuses and toggle menu availability. Rush Insights shows an hourly demand forecast and recommends a quieter pickup window.

## Run locally

**Requirements:** Node.js 18+ and npm.

```bash
npm install
npm run dev
```

Open the local URL printed by Vite (usually http://localhost:5173).

## Deploy to Vercel

1. Push this folder to a GitHub repository.
2. In Vercel, choose **Add New → Project** and import the repository.
3. Framework preset: **Vite**. Build command: `npm run build`. Output directory: `dist`.
4. Deploy. `vercel.json` includes an SPA rewrite so client-side routes work on refresh.

No environment variables are required for the built-in demo mode.

## Optional Supabase setup

The demo works immediately using browser localStorage. This is ideal for trying the prototype, but data is local to that browser and is not shared between students/devices.

To prepare a shared database:

1. Create a Supabase project.
2. Open **SQL Editor** and run `supabase/schema.sql`.
3. Copy `.env.example` to `.env.local` and add your project URL and anon/public key.
4. Restart the Vite dev server / add the same variables in Vercel Project Settings → Environment Variables, then redeploy.

The current UI writes new orders and order status updates to the configured `orders` table. Menu and order reads currently use the demo seed/local browser store; complete multi-user production operation requires wiring menu/order hydration and realtime subscriptions to Supabase.

## Demo walkthrough

- Open **Discover menu**, add dishes and open **My bag**.
- Enter a pickup name and place an order. A unique token is generated.
- Open **My orders** to view the digital token and progress timeline.
- Use the profile menu (bottom-left) → **Switch to admin** to open Kitchen Control.
- Update an order from `Order placed` to `Preparing`, `Ready for pickup`, then `Collected`.
- Open **Rush insights** to view the hourly demand forecast and recommended collection window.

## Features

- Search and category filters
- Menu cards with prep-time estimates and availability
- Cart quantity controls and subtotal
- Digital order tokens and status timeline
- Order history
- Kitchen queue and menu availability controls
- Order/revenue summary and popular item metric
- Hourly rush forecast and off-peak collection recommendation
- Responsive layout for desktop and mobile
- Local persistence using localStorage

## Important prototype notes

- Payment processing is intentionally not enabled; this prototype displays a no-payment demo checkout.
- The admin role switch is a demo convenience, **not authentication**. Do not use it to control a live canteen without adding Supabase Auth and staff role checks.
- Forecast values are illustrative seeded estimates, not a trained production ML model. For a real forecast, collect timestamped orders and train/evaluate a time-series or regression model.
- For production use, add authentication, server-side validation, rate limiting, inventory checks, secure RLS policies, and a payment provider if required.

## Tech stack

React · Vite · CSS · Supabase JS (optional database connection) · Vercel
