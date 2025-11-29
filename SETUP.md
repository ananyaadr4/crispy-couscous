# Quick Setup Guide

## ✅ What's Fixed

The main issue was in `.actor/actor.json`:
- **Before**: `"input": "./.actor/input_schema.json"` (incorrect - double .actor path)
- **After**: `"input": "./input_schema.json"` (correct - relative to .actor folder)

## 🚀 Quick Start

### 1. Push to GitHub

```bash
# Navigate to the extracted folder
cd influencer-scraper-complete

# Initialize git
git init

# Add all files
git add .

# Commit
git commit -m "Initial commit: Influencer Data Scraper"

# Add your GitHub repository
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git

# Push to main branch
git branch -M main
git push -u origin main
```

### 2. Deploy to Apify

**Option A: Via Apify Console (Recommended)**

1. Go to [Apify Console](https://console.apify.com/)
2. Click "Actors" → "Create new"
3. Select "Import from GitHub"
4. Enter your repository URL
5. Click "Create & Build"
6. Wait for the build to complete
7. Test with the default input or customize it

**Option B: Via Apify CLI**

```bash
# Install Apify CLI globally
npm install -g apify-cli

# Login to Apify
apify login

# Navigate to your project
cd influencer-scraper-complete

# Initialize (if not already done)
apify init

# Push to Apify
apify push
```

### 3. Test Your Actor

Use this sample input to test:

```json
{
  "platformLinks": [
    "https://www.instagram.com/cristiano/"
  ],
  "executive": "Test User",
  "team": "Warriors",
  "category": "Sports",
  "internalComment": "Test run"
}
```

## 📁 Project Structure

```
influencer-scraper-complete/
├── .actor/
│   ├── actor.json           ← FIXED: Correct input path
│   └── input_schema.json    
├── src/
│   └── main.js              
├── Dockerfile               
├── package.json             
├── .gitignore              
└── README.md               
```

## ✨ Features

- ✅ Scrapes Instagram, TikTok, YouTube
- ✅ Extracts followers, avg views, engagement rate
- ✅ Handles multiple creators in one run
- ✅ Error handling for failed scrapes
- ✅ Customizable metadata fields

## 🔍 What Gets Scraped

| Platform  | Data Points |
|-----------|------------|
| Instagram | Name, Followers, Post likes/views, ER |
| TikTok    | Name, Followers, Video views, ER |
| YouTube   | Name, Subscribers, Video views, ER |

## ⚙️ Configuration

Edit `.actor/input_schema.json` to:
- Change default values
- Add new team options
- Modify categories
- Adjust field descriptions

## 🐛 Common Issues

**Build fails?**
- Check that all files are committed to Git
- Verify `.actor/actor.json` has correct paths
- Ensure repository is public or Apify has access

**No data scraped?**
- Social media platforms may have changed their HTML
- Profile might be private
- Try increasing wait times in code

**Timeout errors?**
- Increase `navigationTimeoutSecs` in main.js
- Check your internet connection
- Reduce number of URLs per run

## 📊 Output Format

Each creator returns:
```json
{
  "Internal Comment": "string",
  "Date": "DD/MM/YYYY",
  "Executive": "string",
  "Team": "string",
  "Creator Name": "string",
  "Category": "string",
  "Platform": "Instagram|TikTok|YouTube",
  "Platform Link": "URL",
  "Followers": number,
  "Region": "string",
  "Cost": "string",
  "Avg Views": number,
  "ER": "percentage",
  "Client Comment": "string",
  "TCE Comment": "string"
}
```

## 🎯 Next Steps

1. ✅ Download the complete project
2. ✅ Push to GitHub
3. ✅ Deploy to Apify
4. ✅ Test with sample data
5. ✅ Customize for your needs
6. ✅ Set up scheduled runs (optional)

## 💡 Tips

- Start with 1-2 URLs to test before bulk scraping
- Use Apify's scheduler for regular data collection
- Export data to Google Sheets or CSV
- Monitor your Apify usage/credits

## 📚 Resources

- [Apify Documentation](https://docs.apify.com/)
- [Crawlee Documentation](https://crawlee.dev/)
- [Puppeteer Documentation](https://pptr.dev/)

---

**Need Help?** Check the main README.md for detailed documentation.
