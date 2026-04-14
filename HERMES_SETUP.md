# Hermes Setup Guide for last30days

This guide covers installing last30days on Hermes AI Agent.

## Prerequisites

1. **Hermes installed** - See https://github.com/NousResearch/hermes-agent
2. **Python 3.12+** (3.13 and 3.14 also work) - `brew install python@3.12` or similar
3. **yt-dlp** (optional, for YouTube) - `brew install yt-dlp`

## Installation

### Option 1: Via sync.sh (Recommended)

```bash
# Clone the repo
git clone https://github.com/mvanhorn/last30days-skill.git
cd last30days-skill

# Run the sync script
bash scripts/sync.sh
```

This will auto-detect Hermes and deploy to `~/.hermes/skills/research/last30days/`

### Option 2: Manual Copy

```bash
# Create directories
mkdir -p ~/.hermes/skills/research/last30days/scripts/lib

# Copy SKILL.md (use Hermes-specific version if available)
cp .hermes-plugin/SKILL.md ~/.hermes/skills/research/last30days/SKILL.md

# Copy main scripts
cp scripts/last30days.py scripts/watchlist.py scripts/briefing.py scripts/store.py \
  ~/.hermes/skills/research/last30days/scripts/

# Copy library modules
cp scripts/lib/*.py ~/.hermes/skills/research/last30days/scripts/lib/

# Copy vendor directory if present
[ -d scripts/lib/vendor ] && cp -r scripts/lib/vendor ~/.hermes/skills/research/last30days/scripts/lib/

# Copy fixtures if present
[ -d fixtures ] && cp -r fixtures ~/.hermes/skills/research/last30days/
```

## Usage

In Hermes, invoke with:

```
last30days "your research topic"
```

Or with options:
```
last30days "best mechanical keyboards 2025" --search=reddit,youtube
last30days "AI news" --days=7 --deep
```

## First Run Setup

On first run, the skill will guide you through setup:

1. **Auto setup** (~30 seconds)
   - Scans browser cookies for X/Twitter
   - Checks/installs yt-dlp for YouTube
   - Configures free sources (Reddit, HN, Polymarket)

2. **Optional: ScrapeCreators**
   - Adds TikTok, Instagram, Reddit backup
   - 10,000 free API calls
   - Sign up at scrapecreators.com

3. **Optional: API Keys**
   - XAI_API_KEY for X/Twitter (alternative to browser cookies)
   - BRAVE_API_KEY for web search

## Available Sources

### Free (No API Key)
- **Reddit** - Public discussions and comments
- **Hacker News** - Tech discussions via Algolia
- **Polymarket** - Prediction markets
- **YouTube** - Search and transcripts (requires yt-dlp)
- **GitHub** - Repository discussions, issues, and releases
- **Perplexity** - AI-powered web search and research summaries

### Requires API Key
- **X/Twitter** - xAI API key or browser cookies
- **TikTok** - ScrapeCreators API
- **Instagram** - ScrapeCreators API
- **Bluesky** - Bluesky API credentials
- **Threads** - Meta/Threads API credentials
- **Pinterest** - Pinterest API credentials
- **Web Search** - Brave Search API

## Troubleshooting

### Python not found
```bash
# Find Python 3.12+
which python3.12 python3.13 python3.14

# If not installed
brew install python@3.12
```

### yt-dlp not found
```bash
brew install yt-dlp
# or
pip install yt-dlp
```

### Check what's configured
```bash
cd ~/.hermes/skills/research/last30days
python3 scripts/last30days.py --diagnose
```

## Updating

To update to the latest version:

```bash
cd last30days-skill
git pull
bash scripts/sync.sh
```

## Support

- Original repo: https://github.com/mvanhorn/last30days-skill
- Hermes Agent: https://hermes-agent.nousresearch.com
- Hermes Agent repo: https://github.com/NousResearch/hermes-agent
- Issues: Please report in the original repo
