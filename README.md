```markdown
# 🇲🇾 MY MP Dashboard – GE-15 Results + Live News

An interactive web dashboard that visualizes Malaysia’s 15th General Election (GE-15) results, MP performance metrics, and fetches the latest news headlines for each elected representative using the **GNews API**.

![Dashboard Preview](https://via.placeholder.com/800x400?text=MP+Dashboard+Screenshot)  
*(Replace with actual screenshot if available)*

## ✨ Features

- **🗳️ GE-15 Data** – Complete parliamentary results for all 222 seats (winners, votes, majorities).
- **📊 MP Profile** – Shows party, constituency, vote share, majority, and a calculated performance rating (1–10).
- **📰 Live News Headlines** – Fetches the 3 most recent English news articles for the selected MP (via GNews API). Displays `N/A` if none found.
- **📈 Interactive Charts**:
  - Party seat distribution
  - Seats by state
  - Coalition strength (PH, PN, BN, GPS, etc.)
  - Top 10 MPs by majority & vote share
- **🔍 Search & Select** – Dropdown or type‑ahead search for any winning MP.
- **📱 Responsive** – Works on desktop, tablet, and mobile.

## 🚀 Demo

You can try the dashboard live (if hosted) or run it locally.  
👉 [Live Demo](#) *(add your hosting link here)*

## 🛠️ Tech Stack

- HTML5 / CSS3 / JavaScript (Vanilla)
- [Chart.js](https://www.chart.js/) – for all visualizations
- [Font Awesome](https://fontawesome.com/) – icons
- [GNews API](https://gnews.io/) – news headlines

## 📦 Getting Started

### Prerequisites

- A modern web browser (Chrome, Firefox, Edge, etc.)
- (Optional) A free **GNews API key** – [sign up here](https://gnews.io/register/) (100 requests/day free)

### Installation

1. **Clone or download** this repository.
2. **Open `index.html`** in your browser – the dashboard will load with embedded election data.
3. **To enable live news headlines:**
   - Obtain your free API key from [gnews.io](https://gnews.io/).
   - Open `index.html` in a text editor.
   - Locate the line:
     ```js
     const NEWS_API_KEY = "YOUR_API_KEY_HERE";
     ```
   - Replace `"YOUR_API_KEY_HERE"` with your actual API key.
   - Save the file and refresh the browser.

> ⚠️ **Note**: The news feature will only work if you provide a valid API key. Without it, you will see a message prompting you to add the key.

## 📂 Project Structure

```

.
├── index.html          # Main dashboard (all CSS, JS, and data embedded)
├── README.md           # This file
└── assets/             # (optional) – no external assets needed

```

## 📊 Data Sources

- **GE-15 Election Results** – Extracted from the official SPR (Election Commission) data and embedded directly into the HTML as a CSV‑like structure. All 222 constituencies and their winners are included.
- **News Headlines** – Provided by the [GNews API](https://gnews.io/), which aggregates articles from over 80,000 global sources. The dashboard searches for the MP’s name, filters by country `my` (Malaysia) and language `en` (English).

## 🧪 How It Works

1. **Election Data** – The CSV data is parsed in JavaScript. Winners are identified by `result=1`.
2. **MP Profile** – When you select an MP, the dashboard:
   - Looks up their constituency, votes, runner‑up votes, and majority.
   - Calculates a performance rating based on vote share and margin.
   - Updates the chart showing vote comparison.
3. **News Fetching** – On MP selection (or when switching to the News tab), the dashboard calls:
```

GET https://gnews.io/api/v4/search?q=MP_NAME&country=my&lang=en&max=3&apikey=YOUR_KEY

```
- If articles are returned, they are displayed as clickable cards with source and date.
- If none are found, a “N/A” placeholder appears.
4. **Charts** – Use Chart.js to render seat distributions, coalition breakdowns, and top rankings.

## 🔧 Customisation

- **Add more MPs** – Extend the embedded CSV data inside `index.html` (the `fullCSVData` variable) with additional rows.
- **Change rating formula** – Modify the `rating` calculation inside the `updateMPProfile()` function.
- **Styling** – Adjust CSS variables or class names to match your brand.

## 📌 Known Limitations

- The GNews API free tier allows **100 requests per day**. Heavy usage may exceed this limit.
- News articles are in **English only** (you can change `lang=ms` for Malay, but coverage may be lower).
- The dashboard does not include a backend proxy, so your API key is exposed in the frontend. For production, **move the API call to a backend** (e.g., Node.js, Cloudflare Worker).

## 🤝 Contributing

Contributions are welcome! Feel free to open an issue or submit a pull request for:
- Additional data visualisations
- Support for more languages/news sources
- Backend proxy example

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🙏 Acknowledgements

- [GNews](https://gnews.io/) for providing a simple news API.
- [Chart.js](https://www.chart.js/) for elegant charts.
- Malaysia’s Election Commission (SPR) for making election data public.

---

**Built with ❤️ for Malaysian democracy and transparency.**  
For questions or feedback, please open an issue on GitHub.
```