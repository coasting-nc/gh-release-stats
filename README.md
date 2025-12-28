# GitHub Advanced Release Tracker

This is a simple web-based tool to track and visualize download statistics for GitHub releases.

## Usage

1. Visit [https://ramiawar.github.io/gh-release-stats/](https://ramiawar.github.io/gh-release-stats/)
2. Enter a GitHub repository in the format `username/repository`
3. Click "Track Releases" to view the download statistics

### URL Parameters

You can bookmark specific repositories and settings using URL parameters:

- `?repo=owner/repo` - Automatically load a specific repository
- `&versions=N` - Set the number of versions to display (e.g., `&versions=10`)
- `&versions=all` - Display all available versions

**Examples:**
- `index.html?repo=microsoft/vscode`
- `index.html?repo=microsoft/vscode&versions=15`
- `index.html?repo=microsoft/vscode&versions=all`

## Features

- 📊 **Interactive Chart** - Visualize download counts per release with Chart.js
- 🎛️ **Version Controls** - Select how many versions to display (number input, slider, or quick-select buttons)
- 📈 **Asset Breakdown** - View individual asset downloads and total downloads per release
- 📋 **Detailed Table** - Browse release information in a sortable table
- 💾 **CSV Export** - Export release data for further analysis
- 🔗 **URL Bookmarking** - Save and share specific repository views with URL parameters
- 🎨 **Toggle Legend** - Show/hide chart legend for better visibility

## Future Enhancements

See [FUTURE_FEATURES.md](FUTURE_FEATURES.md) for a comprehensive list of potential features and available GitHub API data that could be integrated into this tool.
