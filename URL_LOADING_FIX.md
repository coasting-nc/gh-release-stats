# Fix Applied - URL Loading Issue

## Problem
When loading the page with URL parameters like:
```
?repo=coasting-nc/LMUFFB&versions=all&minDownloads=58&filterEnabled=true
```

The URL was being corrupted to:
```
?repo=coasting-nc/LMUFFB&versions=all&minDownloads=58&filterEnabled=
```

This caused the page to fail loading with "Failed to fetch release data."

## Root Cause
During initial page load from URL parameters:
1. URL parameters were being parsed
2. Settings were being applied (version count, filter, etc.)
3. Each setting change triggered `updateURL()`
4. `updateURL()` was overwriting the URL before all parameters were fully loaded
5. This created a race condition where the URL could be partially written

## Solution
Added `isLoadingFromURL` flag that:
- Is set to `true` when loading from URL parameters
- Prevents `updateURL()` from running during initial load
- Is set back to `false` after `trackReleases()` completes
- Improved empty string handling for `filterEnabled` parameter

## Changes Made
1. Added `isLoadingFromURL` global flag
2. Set flag to `true` at start of URL parameter loading
3. Modified `updateURL()` to return early if flag is true
4. Clear flag after `trackReleases()` completes
5. Improved `filterEnabledParam` check to handle empty strings

## Testing
Try these URLs - they should now work correctly:

1. **Basic:**
   ```
   file:///C:/dev/personal/gh-release-stats/index.html?repo=coasting-nc/LMUFFB
   ```

2. **With all parameters:**
   ```
   file:///C:/dev/personal/gh-release-stats/index.html?repo=coasting-nc/LMUFFB&versions=15&minDownloads=5&filterEnabled=true
   ```

3. **With filter disabled:**
   ```
   file:///C:/dev/personal/gh-release-stats/index.html?repo=coasting-nc/LMUFFB&versions=all&minDownloads=50&filterEnabled=false
   ```

## Expected Behavior
✅ Page loads successfully
✅ All parameters are applied correctly
✅ URL remains unchanged during initial load
✅ URL updates when you change settings after load completes
✅ No "Failed to fetch release data" error
