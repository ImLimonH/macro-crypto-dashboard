# Macro-Crypto Dashboard

A dark GitHub Pages dashboard for monitoring macro signals that often matter to crypto markets: M2 liquidity, CPI inflation, USD strength, 10Y Treasury yields, oil inventories, PMI, and BTC/USD.

Live site: https://imlimonh.github.io/macro-crypto-dashboard/

## What It Shows

| Signal | Function | Source |
| --- | --- | --- |
| M2 Money Supply | `fredM2()` | FRED public CSV `M2SL` |
| CPI Inflation | `fredCPI()` | FRED public CSV `CUSR0000SETA02` |
| DXY Proxy | `alphaDXY()` | Alpha Vantage EUR/USD inverse proxy |
| 10Y Treasury Yield | `alphaTreasury10Y()` | Alpha Vantage Treasury Yield |
| Oil Inventories | `eiaOil()` | EIA petroleum weekly stocks |
| US PMI | `tePMI()` | TradingEconomics free guest endpoint |
| BTC/USD | `coingeckoBTC()` | CoinGecko public API |

## API Usage

The dashboard is a static GitHub Pages app. FRED M2 and CPI use public no-key CSV endpoints, which avoids the browser CORS failure that affected the previous FRED API calls. If the direct FRED CSV request is blocked, the page retries through a public CORS proxy because no API key is involved.

Keyed APIs are direct-only and are not sent through public CORS proxy services. Enter keys in the dashboard settings row; the browser stores them in `localStorage` for that device only.

Needed keys:

| Key | Used For |
| --- | --- |
| Alpha Vantage API key | DXY proxy and 10Y Treasury yield |
| EIA API key | Oil inventories |
| TradingEconomics client | PMI, defaults to `guest:guest` |

Important: public GitHub Pages cannot keep API keys secret if they are hardcoded into HTML or JavaScript. For production-grade security, move vendor requests into a private backend or serverless worker and keep keys in server-side environment variables.

## Run Locally

Clone the repository:

```bash
git clone https://github.com/ImLimonH/macro-crypto-dashboard.git
cd macro-crypto-dashboard
```

Start a local static server:

```bash
python -m http.server 8000
```

Open:

```text
http://localhost:8000/public/dashboard.html
```

The root `index.html` redirects to `public/dashboard.html`, so this also works:

```text
http://localhost:8000/
```

## Auto-Deploy

The workflow at `.github/workflows/deploy.yml` deploys the repository to GitHub Pages on every push to `main`.

Deployment flow:

1. Checkout the repository.
2. Configure GitHub Pages.
3. Upload the static site as a Pages artifact.
4. Deploy to GitHub Pages.

The dashboard is available at the repository homepage after the workflow completes:

https://imlimonh.github.io/macro-crypto-dashboard/

## Impact Score

The Crypto Impact Score is a weighted 0-100 signal:

| Component | Weight |
| --- | ---: |
| M2 liquidity trend | 24% |
| CPI inflation | 18% |
| USD strength and 10Y yields | 26% |
| Growth, oil shock, and BTC momentum | 32% |

Interpretation:

| Score | Level |
| --- | --- |
| 0-33 | Low |
| 34-66 | Medium |
| 67-100 | High |

The score is directional and informational, not financial advice.

## Project Structure

```text
macro-crypto-dashboard/
├── index.html
├── public/
│   └── dashboard.html
├── .github/
│   └── workflows/
│       └── deploy.yml
└── README.md
```

## Roadmap

- Add a private serverless proxy for true key protection.
- Add richer Treasury yield views, including 2Y/10Y spread.
- Expand EIA support for crude, gasoline, and distillate inventories.
- Replace TradingEconomics guest access with authenticated credentials if needed.
- Add historical charts and local caching.
- Add CSV export for indicator snapshots.

## License

MIT
