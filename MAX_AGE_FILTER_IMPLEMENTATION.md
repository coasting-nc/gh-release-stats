# Max Age Filter Implementation

## Summary
Successfully implemented a configurable maximum release age filter to address the issue where older releases were not being displayed. The GitHub API's default behavior only returns 30 releases per request, which was limiting the data shown.

## Changes Made

### 1. **Root Cause Identified**
- The GitHub API `/repos/{owner}/{repo}/releases` endpoint returns only **30 releases by default**
- Maximum of **100 releases per page** with pagination
- The original code didn't use pagination, so it was limited to the first 30 releases

### 2. **New Features**

#### UI Controls
Added a new "Maximum release age to fetch" section with:
- **Numeric input field**: Allows manual entry of days (-1 for unlimited)
- **Quick select buttons**: 
  - 2 weeks (14 days)
  - 1 month (30 days)
  - 3 months (90 days)
  - 6 months (180 days)
  - 1 year (365 days)
  - Unlimited (-1)

#### URL Parameter Support
- New `maxAge` parameter (e.g., `?maxAge=90` or `?maxAge=-1`)
- Automatically persists in URL when changed
- Loads from URL on page initialization

#### Backend Implementation
- **Pagination**: Fetches up to 100 releases per page, continuing until all matching releases are retrieved
- **Age filtering**: Calculates cutoff date based on `maxAge` setting
- **Smart fetching**: Stops fetching when releases older than cutoff are encountered
- **Unlimited mode**: When `maxAge=-1`, fetches all available releases

### 3. **Test Results**

#### Repository: `coasting-nc/LMUFFB`
- **Unlimited (-1)**: Fetched **73 releases** (all available)
- **3 months (90 days)**: Fetched **73 releases** (all within timeframe)
- **2 weeks (14 days)**: Fetched **30 releases** (correctly stopped at cutoff)

#### Repository: `google/zx`
- **Unlimited (-1)**: Fetched **100 releases** (pagination working)
- **3 months (90 days)**: Fetched **1 release** (correctly filtered)

### 4. **Technical Details**

#### Pagination Logic
```javascript
while (hasMore) {
    const url = `https://api.github.com/repos/${repo}/releases?per_page=${perPage}&page=${page}`;
    const releases = await response.json();
    
    // Filter by age if cutoff date is set
    // Stop when older releases are encountered
    // Continue to next page if needed
}
```

#### Age Filtering
- Cutoff date calculated as: `currentDate - maxAgeDays`
- Releases with `published_at >= cutoffDate` are included
- Fetching stops when first release older than cutoff is found

### 5. **Known Issues**
- **Minor UI bug**: The active styling (blue background) on quick select buttons doesn't always update correctly when switching between options. The functionality works correctly (data fetches properly), but the visual feedback could be improved.

## Usage Examples

### URL Examples
```
# Fetch releases from last 3 months
index.html?repo=coasting-nc/LMUFFB&maxAge=90

# Fetch all releases (unlimited)
index.html?repo=coasting-nc/LMUFFB&maxAge=-1

# Combine with other parameters
index.html?repo=coasting-nc/LMUFFB&maxAge=90&versions=10&minDownloads=5
```

### Default Behavior
- Default setting: **-1 (unlimited)** - fetches all available releases
- This ensures backward compatibility and maximum data visibility

## Benefits
1. **Solves the original issue**: Older releases are now accessible
2. **Flexible filtering**: Users can limit data by age for performance
3. **URL shareable**: Settings persist in URL for easy sharing
4. **Efficient fetching**: Stops early when age limit is reached
5. **Backward compatible**: Default unlimited setting maintains existing behavior
