# Acme Casino — test integration

Single-page static site that simulates a fictional crypto casino operator
embedding the Vault Breaker Studios game catalogue.

Used to validate the operator-facing iframe + CSP `frame-ancestors` flow
end-to-end before a real operator integration.

## Deploy

```bash
vercel deploy --prod
```

Site is purely static (single `index.html`) — no build step required.

## What it does

- Renders three game tiles (Vault Breaker, Pressure Plate, Cipher Crack).
- On click, opens a full-page iframe pointing at
  `https://vaultbreaker.dev/play/<slug>?operator=demo&currency=USDT`.
- "← Back to lobby" closes the iframe and returns to the lobby view.
- Esc also closes the iframe.

## What needs to be true on the Vault Breaker side

This site's origin must be listed in the Vault Breaker `vercel.json`
`Content-Security-Policy: frame-ancestors` directive on the `/play/*` route.
Without that, browsers block the iframe.
