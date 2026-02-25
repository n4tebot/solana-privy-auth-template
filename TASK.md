# Task: Build Solana Privy Auth Template

Build a complete `community/privy-auth` template for the solana-foundation/templates repo.

## What This Is
A bounty submission for https://www.college.xyz/bounties/15 — a $200 Solana bounty to create a Privy authentication template for `create-solana-dapp`.

## Requirements
- Next.js + Tailwind CSS + TypeScript
- Privy SDK (@privy-io/react-auth)
- Solana dApp with Privy-based auth (social logins, embedded wallets, protected routes)
- Usable via `pnpm create solana-dapp --template privy-auth`

## Deliverables (ALL required)

### 1. Template Code (community/privy-auth/)
Complete Next.js app with:
- **PrivyProvider** wrapping the app with Solana config
- **Login button/modal** using Privy's `useLogin` hook
- **Social login providers**: Google, Twitter/X, Discord, GitHub, Email
- **Embedded wallet** creation + display (Privy auto-creates Solana wallets)
- **User profile page** showing wallet info, linked accounts
- **Protected routes** using middleware or client-side auth guards
- **Wallet connection state management** with auth status indicators
- **Logout functionality**
- **Type definitions** for Privy user objects and sessions

### 2. README.md
Cover:
- Privy account setup (get App ID from dashboard.privy.io)
- Dashboard configuration (enable Solana, configure login methods)
- Embedded wallet features explanation
- Session management approach
- Links to Privy docs
- Setup & run instructions

### 3. package.json with create-solana-dapp metadata
```json
{
  "name": "privy-auth",
  "displayName": "Privy Auth",
  "description": "Next.js + Tailwind template with Privy authentication, social logins, and embedded Solana wallets",
  "usecase": "Starter",
  "keywords": ["solana", "privy", "authentication", "social-login", "embedded-wallet", "nextjs", "tailwind", "typescript"],
  "create-solana-dapp": {
    "instructions": [
      "Copy .env.example to .env.local and add your Privy App ID:",
      "+cp .env.example .env.local",
      "Get your App ID from https://dashboard.privy.io",
      "Install dependencies:",
      "+{pm} install",
      "Start the dev server:",
      "+{pm} dev"
    ]
  }
}
```

### 4. og-image.png
Create a simple 1200x630 placeholder PNG (we'll generate proper one later).

## Tech Specifics

### Privy SDK Setup
```
npm packages: @privy-io/react-auth @solana/web3.js
```

PrivyProvider config:
```tsx
<PrivyProvider
  appId={process.env.NEXT_PUBLIC_PRIVY_APP_ID!}
  config={{
    appearance: { theme: 'dark' },
    loginMethods: ['email', 'google', 'twitter', 'discord', 'github'],
    embeddedWallets: {
      solana: { createOnLogin: 'users-without-wallets' }
    },
    solanaClusters: [{ name: 'mainnet-beta', rpcUrl: 'https://api.mainnet-beta.solana.com' }]
  }}
>
```

### Key Privy Hooks
- `usePrivy()` — auth state, login, logout, user object
- `useLogin()` — trigger login modal
- `useSolanaWallets()` — access embedded Solana wallets
- `useLogout()` — logout

### Project Structure
```
community/privy-auth/
├── package.json
├── og-image.png
├── .env.example
├── .gitignore
├── README.md
├── next.config.ts
├── tailwind.config.ts
├── tsconfig.json
├── postcss.config.mjs
├── src/
│   ├── app/
│   │   ├── layout.tsx          (PrivyProvider wrapper)
│   │   ├── page.tsx            (landing/login page)
│   │   ├── dashboard/
│   │   │   └── page.tsx        (protected route - user profile + wallet info)
│   │   └── globals.css
│   ├── components/
│   │   ├── LoginButton.tsx
│   │   ├── LogoutButton.tsx
│   │   ├── UserProfile.tsx     (wallet info, linked accounts)
│   │   ├── AuthGuard.tsx       (protected route wrapper)
│   │   ├── WalletInfo.tsx      (embedded wallet display + balance)
│   │   └── AuthStatus.tsx      (auth status indicator)
│   ├── providers/
│   │   └── PrivyClientProvider.tsx
│   └── types/
│       └── privy.ts            (type definitions)
```

## Quality Standards
- Clean, well-commented code
- Proper error handling
- Responsive design with Tailwind
- No hardcoded secrets (use env vars)
- ESLint config included
- Works out of the box after adding Privy App ID

## DO NOT
- Include any actual API keys
- Use deprecated Privy APIs
- Skip any deliverable listed above

Build the ENTIRE template. Every file. Production quality.
