# Cypherpunk

Telegram-first Polymarket research desk. Free tape is public. Paid desk unlocks the full feed and backtests with **USDC on Solana**.

This is research, not auto-trading, and not financial advice.

**Site:** [cypherpunk-code.com](https://www.cypherpunk-code.com/)
· **Waitlist:** [@Cypherpunk_Waitlist_bot](https://t.me/Cypherpunk_Waitlist_bot)
· **Methodology:** [docs/HOW_IT_WORKS.md](docs/HOW_IT_WORKS.md)

## Time machine

A Polymarket YES token is already a probability. We reduce the series to a few numbers, then three independent rules either fire a call or stay silent.

```mermaid
flowchart LR
  tape[YES implied-prob tape] --> feat["tapeFeatures
start · last · range · momentum"]
  feat --> m[momentum-v1]
  feat --> r[mean-revert-v1]
  feat --> d[event-drift-v1]
  m --> sig[Signal]
  r --> sig
  d --> sig
  sig --> free[Free tape]
  sig --> paid[Paid desk]
  paid --> bt[1-share backtest]
```

A tiny wiggle is not a call. Rules return `null` unless the move clears a threshold.

## One object

Model rules, AI notes, desk calls, and community ideas all land on the same `Signal`.

```ts
type Signal = {
  market: string
  side: "yes" | "no"
  confidence: number
  rationale: string
  source: "model" | "ai" | "manual" | "community"
  tier: "free" | "paid"
  strategyId?: "momentum-v1" | "mean-revert-v1" | "event-drift-v1"
}
```

```mermaid
flowchart LR
  model --> Signal
  ai --> Signal
  manual --> Signal
  community --> Signal
  Signal --> free[public tape]
  Signal --> paid[membership lock]
```

Free fields are public. Paid fields never leave the server until membership is active.

## Desk

Strangers apply on the waitlist bot. The operator admits by hand. The desk is Telegram chat, not a web tab.

```mermaid
flowchart TB
  wl[Waitlist bot] -->|application| op[Operator inbox]
  op -->|admit / reject| user[Telegram user]
  user --> chat["Desk bot
/ask · /signals"]
  chat -->|USDC on Solana| engines["Paid engines
/paid · /backtest"]
```

## How to start

[Join the waitlist](https://t.me/Cypherpunk_Waitlist_bot). Access is reviewed by hand. If you're in, the bot messages you.

## Founder

[Anon Rothschild](https://github.com/9lordisgod) · [@williemdoe](https://x.com/williemdoe)
