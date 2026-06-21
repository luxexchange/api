# @luxexchange/api

Dev-server proxy middleware for the Lux Exchange frontend.

Three small [`http-proxy-middleware`](https://github.com/chimurai/http-proxy-middleware)
handlers that forward local requests to upstream services, rewriting paths and
injecting the headers those upstreams expect. Intended for use as serverless /
local dev-server routes so the browser can talk to cross-origin APIs without
CORS friction.

| Entry | Mount | Upstream |
|-------|-------|----------|
| `index.js` | `/api`  | `https://api-exchange.lux.network/v1/graphql` |
| `beta.js`  | `/beta` | `https://api-exchange.lux.network/v1` |
| `cmc.js`   | `/cmc`  | CoinMarketCap data API |

## Usage

Each module exports a request handler `(req, res)` with the raw middleware
available as `.middleware`:

```js
const proxy = require('@luxexchange/api') // index.js

// e.g. as a Vercel/serverless function, or mounted in Express/Connect
module.exports = proxy
// or:  app.use(proxy.middleware)
```

## License

MIT — Copyright (c) 2020-2026 Lux Industries, Inc. See [LICENSE](./LICENSE).

Extracted from the `luxfi/exchange` monorepo. This proxy code is Lux-original
and is **not** covered by the GPL of the exchange frontend (which derives from
the Uniswap interface).
