# Affonso Affiliate Proxy - Cloudflare Worker

<a href="https://capgo.app/"><img src='https://raw.githubusercontent.com/Cap-go/capgo/main/assets/capgo_banner.png' alt='Capgo - Instant updates for capacitor'/></a>

Proxy the [Affonso](https://affonso.io) affiliate pixel and APIs through your own domain using a Cloudflare Worker.
This is the Worker `aff` that serves `aff.capgo.app` in production.

## One-Click Deploy

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/Cap-go/affonso-cloudflare-proxy)

## How It Works

| Your Domain | Proxied To |
|---|---|
| `yourdomain.com/r/pixel.js` | `cdn.affonso.io/js/pixel.min.js` |
| `yourdomain.com/r/psl.min.js` | `cdn.affonso.io/js/psl.min.js` |
| `yourdomain.com/r/track` | `api.affonso.io/v1/track` |
| `yourdomain.com/r/v1/track` | `api.affonso.io/v1/track` |
| `yourdomain.com/r/signups` | `api.affonso.io/v1/signups` |

The `/js/pixel.min.js`, `/js/psl.min.js`, `/v1/track` and `/js/signups` aliases are also proxied. Any other path returns 404.

The visitor's real IP (`cf-connecting-ip`) is forwarded as `X-Forwarded-For` and `X-Real-IP` so Affonso fraud checks see it.

## Manual Setup

```bash
git clone https://github.com/Cap-go/affonso-cloudflare-proxy
cd affonso-cloudflare-proxy
npm install
npx wrangler deploy
```

Then attach your custom domain (for example `aff.yourdomain.com`) to the Worker in the Cloudflare dashboard.
