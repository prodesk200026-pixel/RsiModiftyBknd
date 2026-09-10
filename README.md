# Bharati Universal Backend — Dhan Data Gateway

Broker-data-only backend for Bharati RSI / PRO TERMINAL and future frontends.

## Responsibilities
- Dhan authentication stays server-side.
- Normalized live market ticks over `/ws`.
- Dedicated Dhan 20-level depth/L20 feed.
- Normalized option-chain snapshots: LTP, OI, volume, IV, bid/ask and Dhan Greeks.
- Intraday historical candles.
- Instrument-master lookup.
- Market-data analytics: PCR, OI walls, Max Pain, IV smile, plus explicitly model-derived GEX/dealer-pressure proxies.
- No order placement.
- No RSI/HMA/BBP/strategy execution; those belong to the PWA.

## Render
Build: `npm install`
Start: `npm start`

Set the variables in `.env.example`. Never put Dhan credentials into the PWA.

## REST
- `/api/health`
- `/api/status`
- `/api/auth-status`
- `/api/config`
- `/api/state`
- `/api/ticks`
- `/api/tick?segment=...&securityId=...`
- `/api/option-chain`
- `/api/analytics`
- `/api/depth?segment=NSE_FNO&securityId=...`
- `/api/history?segment=IDX_I&securityId=13&interval=1`
- `/api/instruments?search=NIFTY&limit=20`

## WebSocket
`wss://YOUR-RENDER-HOST/ws`

Events: `hello`, `state`, `status`, `tick`, `optionChain`, `analytics`, `depth`, `error`.

Subscribe example:
```json
{"type":"subscribe","instruments":[{"ExchangeSegment":"NSE_FNO","SecurityId":"12345"}]}
```
