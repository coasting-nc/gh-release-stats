# URL Update Feature Test Instructions

## Manual Testing Steps

To verify that the URL updates when you change settings:

1. **Open the application:**
   - Navigate to: `file:///C:/dev/personal/gh-release-stats/index.html`

2. **Load a repository:**
   - Enter: `coasting-nc/LMUFFB`
   - Click "Track Releases"
   - **Check URL:** Should now show `?repo=coasting-nc/LMUFFB&versions=10&minDownloads=5&filterEnabled=true`

3. **Test version count changes:**
   - Click the "15" quick select button
   - **Check URL:** Should update to `versions=15`
   - Use the slider to change to 8
   - **Check URL:** Should update to `versions=8`
   - Type "20" in the number input
   - **Check URL:** Should update to `versions=20`
   - Click "All" button
   - **Check URL:** Should update to `versions=all`

4. **Test filter changes:**
   - Uncheck the "Enable filter" checkbox
   - **Check URL:** Should update to `filterEnabled=false`
   - Check it again
   - **Check URL:** Should update to `filterEnabled=true`
   - Change minimum downloads to 50
   - **Check URL:** Should update to `minDownloads=50`

5. **Test URL persistence:**
   - Copy the current URL from the address bar
   - Open a new tab
   - Paste the URL and press Enter
   - **Verify:** All settings should load exactly as they were (version count, filter enabled/disabled, minimum downloads value)

## Expected Behavior

✅ **URL should update automatically** whenever you:
- Load a repository
- Change version count (via input, slider, or quick select buttons)
- Enable/disable the filter
- Change the minimum downloads value

✅ **URL format:**
```
index.html?repo=owner/repo&versions=N&minDownloads=N&filterEnabled=true/false
```

✅ **Example full URL:**
```
index.html?repo=microsoft/vscode&versions=20&minDownloads=50&filterEnabled=true
```

## What to Look For

1. **Address bar updates** - The URL in your browser's address bar should change immediately when you adjust any setting
2. **No page reload** - The page should NOT reload when the URL updates
3. **Bookmarkable** - You should be able to bookmark the URL and return to the exact same view later
4. **Shareable** - You should be able to copy the URL and share it with others

## Troubleshooting

If the URL doesn't update:
- Open browser console (F12)
- Check for any JavaScript errors
- Verify that you've loaded a repository first (URL won't update without a repo)
