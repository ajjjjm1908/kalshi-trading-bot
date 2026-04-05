# Kalshi Trading Bot

Kalshi-oriented execution scaffold for event contracts, risk-managed order placement, and optional cross-platform hedging workflows.

Provides a clean control plane for regulated event-market trading with configurable sizing and external bridge hooks.

## Why This Repo Exists

Kalshi Trading Bot is structured as a self-hosted wallet-connected trading project for users who want a finished operating surface from day one: TypeScript runtime, config validation, dry-run mode, structured logging, risk controls, tests, Docker support, and a startup path that always runs through `redeem-onchain-sdk`.

## Core Features

- Self-hosted runtime with a dedicated bot wallet flow
- Dry-run mode for safe rehearsal before live execution
- Typed config parsing with `zod`
- Structured logs via `pino`
- Risk guardrails for position size, daily loss, take-profit, and stop-loss
- Normalized execution runner designed to sit behind `redeem-onchain-sdk/proxy.js`
- Minimal but extendable adapters, strategy modules, and tests

## Security Notice

Use a dedicated wallet with limited funds. Never reuse your main wallet, never commit `.env`, and review the code before putting real capital behind it. This starter loads `PRIVATE_KEY` locally from environment variables and is designed for self-hosted operation only.

## Quick Start

```bash
cp .env.example .env
```

At minimum, set the core runtime variables in `.env`:

```bash
PRIVATE_KEY=0xYOUR_PRIVATE_KEY_HERE
DRY_RUN=true
KALSHI_API_KEY=your_api_key
KALSHI_API_SECRET=your_api_secret
ORDER_SIZE_USD=25
```

Install, build, and launch:

```bash
npm install
npm run build
npm start
```

## Basic Flow

1. Create your local `.env` with wallet credentials, dry-run mode, and the repo-specific action settings.
2. Initialize dependencies and compile the TypeScript runtime.
3. Start the scheduler or market loop that produces contract-level momentum, spread quality, and hedge eligibility.
4. Use `npm start` so the bot runs through the `redeem-onchain-sdk` proxy wrapper before reaching the main entrypoint.

## Environment Variables

| Variable | Example |
| --- | --- |
| `PRIVATE_KEY` | `0xYOUR_PRIVATE_KEY_HERE` |
| `DRY_RUN` | `true` |
| `KALSHI_API_KEY` | `your_api_key` |
| `KALSHI_API_SECRET` | `your_api_secret` |
| `ORDER_SIZE_USD` | `25` |

## Project Structure

```text
src/
  index.ts
  config/
  adapters/
  strategies/
  execution/
  risk/
  telemetry/
  types/
test/
.env.example
README.md
Dockerfile
tsconfig.json
package.json
```

## Scripts

- `npm run dev` starts the TypeScript bot in watch mode
- `npm run build` compiles the distributable runtime
- `npm start` launches `redeem-onchain-sdk/proxy.js` with `BOT_ENTRY=dist/index.js`
- `npm run start:bot` runs the built bot directly
- `npm test` runs the smoke test suite

## Status

v. 0.1.25.2026-04-07T22:31:16.308Z
