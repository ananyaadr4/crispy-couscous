# Influencer Data Scraper

An Apify actor that scrapes creator data from Instagram, TikTok, and YouTube platforms.

## Features

- 📊 Scrapes follower counts, average views, and engagement rates
- 🔄 Supports multiple platforms: Instagram, TikTok, YouTube
- 📝 Customizable metadata: executive, team, category, internal comments
- 🎯 Handles multiple creators in a single run
- ⚡ Built with Puppeteer and Crawlee for reliable scraping

## Project Structure

```
influencer-data-scraper/
├── .actor/
│   ├── actor.json           # Apify actor configuration
│   └── input_schema.json    # Input form schema
├── src/
│   └── main.js              # Main scraper logic
├── Dockerfile               # Docker configuration
├── package.json             # Node.js dependencies
├── .gitignore              # Git ignore rules
└── README.md               # This file
```

## Input Configuration

The actor accepts the following inputs:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `platformLinks` | Array | Yes | List of creator profile URLs |
| `executive` | String | No | Executive name |
| `team` | String | No | Team name (Warriors, Falcons, Phoenix, Eagles) |
| `category` | String | No | Content category |
| `internalComment` | String | No | Internal notes |

### Example Input

```json
{
  "platformLinks": [
    "https://www.instagram.com/shraddha.dsgn/",
    "https://www.tiktok.com/@khaby.lame",
    "https://www.youtube.com/@MrBeast"
  ],
  "executive": "Joyce",
  "team": "Warriors",
  "category": "Tech",
  "internalComment": "High-priority influencers"
}
```

## Output Format

The actor returns structured data for each creator:

```json
{
  "Internal Comment": "High-priority influencers",
  "Date": "29/11/2025",
  "Executive": "Joyce",
  "Team": "Warriors",
  "Creator Name": "Shraddha",
  "Category": "Tech",
  "Platform": "Instagram",
  "Platform Link": "https://www.instagram.com/shraddha.dsgn/",
  "Followers": 125000,
  "Region": "",
  "Cost": "",
  "Avg Views": 45000,
  "ER": "36.00",
  "Client Comment": "",
  "TCE Comment": ""
}
```

## Local Development

### Prerequisites

- Node.js 16 or higher
- npm or yarn

### Setup

1. Clone the repository:
```bash
git clone <your-repo-url>
cd influencer-data-scraper
```

2. Install dependencies:
```bash
npm install
```

3. Run locally:
```bash
npm start
```

## Deployment to Apify

### Method 1: Using Apify Console

1. Create a new actor in [Apify Console](https://console.apify.com/)
2. Go to the "Source" tab
3. Select "Git repository" as source type
4. Enter your GitHub repository URL
5. Click "Build"

### Method 2: Using Apify CLI

1. Install Apify CLI:
```bash
npm install -g apify-cli
```

2. Login to Apify:
```bash
apify login
```

3. Deploy the actor:
```bash
apify push
```

## GitHub Integration

1. Create a new repository on GitHub
2. Push your code:

```bash
git init
git add .
git commit -m "Initial commit: Influencer Data Scraper"
git branch -M main
git remote add origin <your-github-repo-url>
git push -u origin main
```

3. Connect the repository to Apify:
   - In Apify Console, go to your actor's settings
   - Under "Source", select "Git repository"
   - Enter your GitHub repository URL
   - Set branch to `main`
   - Enable "Automatic builds" if desired

## How It Works

1. **Input Processing**: The actor receives platform links and metadata
2. **Platform Detection**: Identifies whether each URL is Instagram, TikTok, or YouTube
3. **Data Extraction**: Uses Puppeteer to scrape:
   - Creator name
   - Follower count
   - Average views (from last 12 posts/videos)
   - Engagement rate (calculated as avg views / followers × 100)
4. **Data Formatting**: Structures the data with metadata and date
5. **Output**: Saves results to Apify dataset

## Supported Platforms

### Instagram
- Scrapes: Profile name, followers, post likes/views
- Calculates: Average engagement from recent posts

### TikTok
- Scrapes: Profile name, followers, video views
- Calculates: Average views from recent videos

### YouTube
- Scrapes: Channel name, subscribers, video views
- Calculates: Average views from recent uploads

## Error Handling

- Invalid URLs are logged and skipped
- Failed scrapes return error data with details
- Network timeouts are set to 90 seconds
- Each creator is processed independently

## Performance

- Processes creators sequentially for stability
- 7-second wait time for page rendering
- 90-second timeout for page navigation
- Headless mode for faster execution

## Limitations

- Social media platforms may update their HTML structure
- Rate limiting may occur with large batches
- Some profiles may be private or restricted
- Requires stable internet connection

## Troubleshooting

### Build fails with "input_schema.json does not exist"
- Ensure `.actor/input_schema.json` path is correct in `actor.json`
- Verify the file exists in the `.actor` folder

### Scraping returns zero data
- Check if the platform has updated their HTML structure
- Verify the profile is public
- Increase wait times if pages load slowly

### Docker build fails
- Ensure all dependencies are listed in `package.json`
- Check Docker image compatibility

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

MIT License - feel free to use and modify as needed.

## Support

For issues or questions:
- Check the [Apify documentation](https://docs.apify.com/)
- Review [Crawlee documentation](https://crawlee.dev/)
- Open an issue on GitHub

---

Built with ❤️ using Apify, Crawlee, and Puppeteer
