# ThoughtPilot AI — Marketing Site

Static marketing site for [thoughtpilotai.com](https://thoughtpilotai.com).

## Architecture

| URL | Purpose |
|-----|---------|
| `thoughtpilotai.com` | This marketing site |
| `app.thoughtpilotai.com` | The product (Next.js frontend) |
| `api.thoughtpilotai.com` | Backend (Railway) |

## Deploy to Vercel

### Step 1 — Push to GitHub
```bash
git init
git add .
git commit -m "feat: marketing site v1"
git remote add origin https://github.com/muhammadokashalodhi-ux/thoughtpilot-marketing.git
git push -u origin main
```

### Step 2 — Connect to Vercel
1. Go to [vercel.com/new](https://vercel.com/new)
2. Import `thoughtpilot-marketing` repo
3. Framework preset: **Other**
4. Root directory: `/`
5. Click **Deploy**

### Step 3 — Assign your domain
1. In this new Vercel project → Settings → Domains
2. Add `thoughtpilotai.com` and `www.thoughtpilotai.com`

### Step 4 — Move your app to subdomain
1. Go to your **existing** frontend Vercel project
2. Settings → Domains → Remove `thoughtpilotai.com`
3. Add `app.thoughtpilotai.com`
4. Update your backend CORS to also allow `app.thoughtpilotai.com`

### Step 5 — Update DNS (if not using Vercel DNS)
Add these records in your domain registrar:
```
A     @        76.76.21.21
CNAME www      cname.vercel-dns.com
CNAME app      cname.vercel-dns.com
```

## Plan-aware signup links

Pricing buttons already pass `?plan=` to the app:
- Free  → `app.thoughtpilotai.com/signup?plan=free`
- Starter → `app.thoughtpilotai.com/signup?plan=starter`  
- Pro → `app.thoughtpilotai.com/signup?plan=pro`

In your frontend signup page, read the param and pre-trigger checkout:
```typescript
// app/signup/page.tsx
const plan = searchParams.get('plan') // 'starter' | 'pro' | 'free'
// Pass to your existing Stripe/Paddle checkout after account creation
```

## Local preview
```bash
npx serve .
# or just open index.html in a browser
```
