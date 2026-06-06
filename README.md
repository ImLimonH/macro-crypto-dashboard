# Macro-Crypto Dashboard

A professional, real-time dashboard that visualizes the intersection of macroeconomic indicators and cryptocurrency market data. Built with vanilla HTML/JavaScript and auto-deployed via GitHub Pages.

## 🚀 Features

- **Real-time Macroeconomic Data**: Fetches M2 Money Supply and CPI from the Federal Reserve Economic Data (FRED) API
- **Crypto Market Data**: Retrieves Bitcoin (BTC/USD) pricing from CoinGecko
- **Currency Strength Index**: Proxies DXY (US Dollar Index) via Alpha Vantage
- **Impact Score Calculation**: Computes a 0–100 impact score based on macro-crypto correlation
- **Dark Theme UI**: Modern, responsive design optimized for desktop and mobile
- **Live Updates**: Dashboard refreshes data on page load and periodic intervals

## 📊 Data Sources

| Data | Source | API | Authentication |
|------|--------|-----|-----------------|
| M2 Money Supply | FRED | Federal Reserve | API Key (client-side) |
| CPI (Inflation) | FRED | Federal Reserve | API Key (client-side) |
| Bitcoin Price | CoinGecko | CoinGecko REST API | None (public) |
| DXY Proxy | Alpha Vantage | FX Exchange Rates | API Key (client-side) |

## 🛠️ Getting Started

### Prerequisites
- A modern web browser (Chrome, Firefox, Safari, Edge)
- (Optional) Node.js for local development server

### Local Setup

1. **Clone the repository**:
   ```bash
   git clone https://github.com/ImLimonH/macro-crypto-dashboard.git
   cd macro-crypto-dashboard
   ```

2. **Open in browser**:
   ```bash
   # Option 1: Direct file open (may have CORS issues)
   open public/dashboard.html
   
   # Option 2: Use a local server (recommended)
   python3 -m http.server 8000
   # Navigate to http://localhost:8000/public/dashboard.html
   ```

3. **View live deployment**:
   Visit: https://ImLimonH.github.io/macro-crypto-dashboard/

## 🔑 API Keys

**Important**: This is a client-side demo. API keys are embedded in the code for demonstration purposes only.

### To use your own keys:

1. **FRED API**: Register at [Federal Reserve Economic Data](https://fredaccount.stlouisfed.org/)
2. **Alpha Vantage API**: Sign up at [Alpha Vantage](https://www.alphavantage.co/api/)
3. **CoinGecko API**: Free—no registration required

Update the keys in `public/dashboard.html`:
```javascript
const FRED_API_KEY = 'your-fred-key-here';
const ALPHA_VANTAGE_KEY = 'your-alpha-vantage-key-here';
```

## 📈 Impact Score Methodology

The dashboard calculates a **Macro-Crypto Impact Score (0–100)** based on:

- **M2 Growth**: Positive correlation with crypto prices
- **CPI (Inflation)**: Indicates purchasing power erosion; influences both markets
- **DXY Strength**: Inverse correlation with crypto (stronger USD = lower BTC)
- **Bitcoin Volatility**: Current price momentum

**Score Interpretation**:
- **0–33**: Low Impact (stable macro environment)
- **34–66**: Medium Impact (moderate volatility signals)
- **67–100**: High Impact (significant macro-crypto correlation detected)

## 🚀 Auto-Deployment

This repository uses **GitHub Actions** to automatically deploy changes to GitHub Pages.

### Workflow Details

- **Trigger**: Pushes to `main` branch
- **Branch**: Deployed to `gh-pages`
- **URL**: https://ImLimonH.github.io/macro-crypto-dashboard/
- **Frequency**: Automatic on every commit

### Deployment Files

- `.github/workflows/deploy.yml`: GitHub Actions workflow configuration
- `public/dashboard.html`: Deployment source

## 📁 Project Structure

```
macro-crypto-dashboard/
├── README.md                       # Project documentation
├── LICENSE                         # MIT License
├── .gitignore                      # Git exclusions
├── public/
│   └── dashboard.html             # Main dashboard (HTML + CSS + JS)
└── .github/
    └── workflows/
        └── deploy.yml             # GitHub Actions auto-deploy workflow
```

## 🔄 How It Works

1. **Data Fetching**: Dashboard makes CORS-enabled API requests on load
2. **Processing**: Raw data is normalized and scored
3. **Rendering**: Results update in real-time with styled cards
4. **Caching**: Browser caches API responses to minimize rate-limit hits
5. **Auto-deploy**: GitHub Actions runs on push → builds → deploys to `gh-pages`

## 🎨 Customization

### Styling
Edit the `<style>` section in `public/dashboard.html` to customize colors, fonts, and layout.

### Data Refresh Interval
Modify the `setInterval()` call (default: 5 minutes):
```javascript
setInterval(fetchAllData, 5 * 60 * 1000); // Change 5 to desired minutes
```

### Impact Score Formula
Adjust weights in the `calculateImpactScore()` function to reflect your analysis.

## 🚦 Status & Monitoring

- **API Health**: Check individual API response times in browser console
- **Rate Limits**: Monitor API vendor limits (FRED: 120 req/min, Alpha Vantage: 5 req/min free tier)
- **Deployment**: View status at [Actions](https://github.com/ImLimonH/macro-crypto-dashboard/actions)

## 🔮 Future Enhancements

- [ ] Treasury Yield Curve (10Y/2Y spread)
- [ ] Oil Inventory Data (EIA API)
- [ ] Purchasing Managers' Index (PMI)
- [ ] Historical data charting (Chart.js integration)
- [ ] WebSocket real-time updates
- [ ] Dark/Light theme toggle
- [ ] Data export (CSV/JSON)
- [ ] Mobile app wrapper

## 📝 License

MIT License - See [LICENSE](LICENSE) for details.

## 🤝 Contributing

Contributions are welcome! Please:
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit changes (`git commit -m 'Add feature'`)
4. Push to branch (`git push origin feature/your-feature`)
5. Open a Pull Request

## 📧 Support

For issues, questions, or suggestions, open a [GitHub Issue](https://github.com/ImLimonH/macro-crypto-dashboard/issues).

---

**Built with ❤️ by [ImLimonH](https://github.com/ImLimonH)**
