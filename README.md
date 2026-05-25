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


Yes — both MP profile pictures and the latest General Election (GE15, November 2022) vote counts are available from open data sources. There is no single API that provides both, but combining two or three sources gives you everything you need. Below are the specific data sources, and further down I show how to integrate them into your dashboard.

---

📸 Where to Get MP Profile Pictures

1. get_photo Tool via OpenTK MCP Server (Official Portraits)

This is the most reliable source for official parliamentary portraits. The OpenTK Model Context Protocol (MCP) Server exposes a get_photo tool which:

· Returns the official portrait photograph of an MP as a binary resource.
· Requires the MP's ID, which you can get from the list_persons tool.
· Ideal for reports, presentations, or your dashboard profiles.

Usage flow:

1. Call list_persons → get all MP IDs, names, parties.
2. Call get_photo with the relevant MP ID → binary image resource.

2. MyMP.org.my (8-bit Avatars)

MyMP generates stylised 8-bit avatars for all 222 Malaysian MPs, shown alongside constituency, election performance, and availability/ethics scores. These are not real photos, but they work well for a visually playful dashboard.

3. Sinar Project / Politikus

The Politikus platform (politikus.sinarproject.org) provides basic candidate photos for MPs, alongside party data. The Sinar Project also maintains a politically exposed persons (PEP) database with candidate profiles and photos.

4. SPR (Election Commission of Malaysia) Website

The official SPR website (spr.gov.my) publishes candidate profiles and photos during election periods. These are typically scraped and republished in datasets like Thevesh's candidates_ge15.csv.

---

🗳️ Where to Get GE15 Vote Counts

1. Tindak Malaysia — Historical Election Results (GitHub)

Tindak Malaysia maintains the most comprehensive open-access election results repository:

· HISTORICAL-ELECTION-RESULTS repository: Contains Parliament-level (federal) and DUN-level (state) election results for GE15 and earlier elections.
· GE15-Dataset-ARCHIVED-: Includes structured CSV files with parliamentary composition, candidate details, and vote counts.
· Key files:
  · MALAYSIA_2022_PARLIAMENT_COMPOSITION.csv
  · candidates_ge15.csv (via Thevesh)

Access: Clone the GitHub repository or download the CSV files directly.

2. Thevesh / Malaysian Election Corpus (MECo)

An academic-grade panel database covering all federal, state, and by-elections since 1955, including GE15.

· Repository: github.com/Thevesh/analysis-election-msia
· Key file: data/candidates_ge15.csv — contains candidate names, parties, constituencies, and vote counts.
· Also on Kaggle (search "Malaysia GE15 election results").

3. Sinar Project — GE15 Open Data

A consolidated page linking to multiple GE15 data resources, including:

· Parliamentary candidates scraped from the SPR website by Thevesh.
· Election results by Tindak Malaysia.
· Basic candidate photos and profiles from Politikus.

4. Malaysia Elections Data API

An open-source API that serves Parliamentary and State seat information, with election results and candidate data. Note: This API was last updated around 2013; verify GE15 coverage before use.

---

🔗 How to Integrate Into Your Dashboard

Step 1: Decide on Your Data Sources

Data Point Recommended Source Access Method
MP Profile Picture OpenTK MCP Server (get_photo) API call with MP ID
MP Profile Picture (fallback) Politikus / Sinar Project Scraped CSV
GE15 Vote Count Tindak Malaysia / Thevesh CSV Download CSV → parse in JS
MP Party & Position Already in your mpMaster —

Step 2: Add GE15 Vote Count to Your mpMaster

Each MP needs a new field: ge15Votes (total votes received in GE15), ge15Majority (margin of victory), and ge15VoteShare (percentage). Example:

```javascript
const mpMaster = {
    "Anwar Ibrahim": {
        name: "Anwar Ibrahim",
        party: "PKR",
        position: "Prime Minister",
        rating: 7.8,
        attendanceRate: 76.2,
        daysPresent: 46,
        // NEW: GE15 election data
        ge15Votes: 49748,       // total votes received
        ge15Majority: 3816,     // margin of victory
        ge15VoteShare: 39.8,    // % of valid votes
        ge15VoterTurnout: 78.0, // % turnout in Tambun
        photoUrl: "",           // populated dynamically
        // ... existing keywords, focusAreas, speechCount
    },
    "Abdul Hadi Awang": {
        // ...
        ge15Votes: 73115,
        ge15Majority: 41974,
        ge15VoteShare: 67.0,
        ge15VoterTurnout: 82.0,
    },
    "Hannah Yeoh": {
        // ...
        ge15Votes: 67042,
        ge15Majority: 59200,
        ge15VoteShare: 80.0,
        ge15VoterTurnout: 72.0,
    },
    // ... other MPs
};
```

How to get real numbers: Download candidates_ge15.csv from Thevesh/analysis-election-msia or the Parliament composition CSV from Tindak Malaysia. Parse the CSV and merge the vote data into your mpMaster object by matching on MP name or constituency.

Step 3: Fetch Profile Pictures

The OpenTK MCP Server is the cleanest programmatic method. The flow:

1. Get MP list (done once or cached):

```javascript
async function getAllMPs() {
    // Call OpenTK list_persons tool
    const response = await fetch('https://opentk-api.example.com/list_persons');
    const data = await response.json();
    // Returns array of { id, name, party, ... }
    return data;
}
```

2. Fetch photo by MP ID:

```javascript
async function getMPPhoto(mpId) {
    const response = await fetch(`https://opentk-api.example.com/get_photo?id=${mpId}`);
    if (!response.ok) return null;
    const blob = await response.blob();
    return URL.createObjectURL(blob); // converts binary to displayable URL
}
```

3. Map MP names from your dashboard to OpenTK IDs. You can do this once by calling list_persons and building a lookup table:

```javascript
// Build lookup: { "Anwar Ibrahim": "mp-00123", "Hannah Yeoh": "mp-00456", ... }
const mpIdLookup = {};
allMPs.forEach(mp => {
    mpIdLookup[mp.name] = mp.id;
});
```

Fallback: If OpenTK is unavailable, use the Sinar Project/Politikus candidate CSV which includes photo URLs for many MPs.

Step 4: Add GE15 Vote Statistics to Your UI

Add a new card or section in the sidebar (or a new tab) to display GE15 election data:

```html
<!-- Add after the Party Info section in your sidebar -->
<div class="party-info" style="margin-top: 16px;">
    <p><i class="fas fa-vote-yea"></i> GE15 Election Result</p>
    <p>🗳️ Votes: <span id="mpGE15Votes">--</span></p>
    <p>📊 Majority: <span id="mpGE15Majority">--</span></p>
    <p>📈 Vote Share: <span id="mpGE15VoteShare">--</span></p>
    <p>🏃 Voter Turnout: <span id="mpGE15Turnout">--</span></p>
</div>
```

Then update these fields inside your updateDashboard() function:

```javascript
async function updateDashboard(mpName) {
    const mp = mpMaster[mpName] || mpMaster["Anwar Ibrahim"];

    // Update GE15 data
    document.getElementById('mpGE15Votes').textContent = mp.ge15Votes.toLocaleString();
    document.getElementById('mpGE15Majority').textContent = mp.ge15Majority.toLocaleString();
    document.getElementById('mpGE15VoteShare').textContent = mp.ge15VoteShare.toFixed(1) + '%';
    document.getElementById('mpGE15Turnout').textContent = mp.ge15VoterTurnout.toFixed(1) + '%';

    // Fetch and display photo
    const mpId = mpIdLookup[mpName];
    if (mpId) {
        const photoUrl = await getMPPhoto(mpId);
        if (photoUrl) {
            document.getElementById('mpPhoto').src = photoUrl;
        }
    }

    // ... rest of existing update logic
}
```

---

⚠️ Important Notes

· OpenTK MCP Server is primarily designed for the Dutch Parliament, but it has been extended with Malaysian parliamentary data (as indicated in the search results). Verify the base URL and available endpoints before deploying.
· SPR website scraping: The SPR site changes frequently during election cycles. Thevesh's CSV snapshots are more stable for programmatic use.
· CORS: GitHub raw CSV files (raw.githubusercontent.com) allow cross-origin requests, so you can fetch() them directly from your dashboard without a backend proxy.
· Photo licensing: Official parliamentary portraits may have usage restrictions. For a public dashboard, 8-bit MyMP avatars are safer (and fun!).
· By-elections: Some seats have changed since GE15 (Nov 2022). Check the latest by-election results if you need current MP data.

---

🚀 Quick-Start Integration Plan

Step Action Time Estimate
1 Download candidates_ge15.csv from GitHub 2 minutes
2 Parse CSV → merge GE15 vote counts into mpMaster 15 minutes
3 Add GE15 stats display section to sidebar HTML 10 minutes
4 Wire up updateDashboard() to populate GE15 fields 5 minutes
5 (Optional) Integrate OpenTK get_photo for profile pictures 30 minutes
6 (Optional) Add <img id="mpPhoto"> to sidebar 5 minutes

---

If you would like me to generate the complete updated HTML with the GE15 vote count display section integrated, just let me know. I'll provide the full file ready to deploy.
