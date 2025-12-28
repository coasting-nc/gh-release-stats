# GitHub Advanced Release Tracker

This is a simple web-based tool to track and visualize download statistics for GitHub releases.

## Usage

1. Visit [https://ramiawar.github.io/gh-release-stats/](https://ramiawar.github.io/gh-release-stats/)
2. Enter a GitHub repository in the format `username/repository`
3. Click "Track Releases" to view the download statistics

### URL Parameters

You can bookmark specific repositories and settings using URL parameters. The URL automatically updates when you change settings in the interface.

**Available Parameters:**
- `?repo=owner/repo` - Automatically load a specific repository
- `&versions=N` - Set the number of versions to display (e.g., `&versions=10`)
- `&versions=all` - Display all available versions
- `&minDownloads=N` - Set minimum downloads filter threshold (e.g., `&minDownloads=50`)
- `&filterEnabled=true/false` - Enable or disable the downloads filter

**Examples:**
- Basic: `index.html?repo=microsoft/vscode`
- With version count: `index.html?repo=microsoft/vscode&versions=15`
- With filter: `index.html?repo=microsoft/vscode&minDownloads=100&filterEnabled=true`
- **All parameters:** `index.html?repo=microsoft/vscode&versions=20&minDownloads=50&filterEnabled=true`

## Features

### Release Statistics
- 📊 **Interactive Chart** - Visualize download counts per release with Chart.js
- 🎛️ **Version Controls** - Select how many versions to display (number input, slider, or quick-select buttons)
- 🔍 **Download Filter** - Filter releases by minimum download count to focus on popular versions
- 📈 **Asset Breakdown** - View individual asset downloads and total downloads per release
- 📋 **Detailed Table** - Browse release information in a sortable table
- 💾 **CSV Export** - Export release data for further analysis
- 🔗 **URL Bookmarking** - Save and share specific repository views with URL parameters
- 🎨 **Toggle Legend** - Show/hide chart legend for better visibility

### Traffic Analytics (Requires Authentication)
- 📈 **Page Views Chart** - Visualize total views and unique visitors over the last 14 days
- 🗺️ **Popular Paths** - See the top 10 most visited repository paths with view counts
- 🔒 **Note**: Traffic data requires repository push access. See [FUTURE_FEATURES.md](FUTURE_FEATURES.md#authentication-implementation-guide) for authentication setup instructions.

## Future Enhancements

See [FUTURE_FEATURES.md](FUTURE_FEATURES.md) for a comprehensive list of potential features and available GitHub API data that could be integrated into this tool, including detailed authentication implementation guides.

