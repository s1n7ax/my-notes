# FlareSolverr Setup Guide Summary

## What is FlareSolverr?

FlareSolverr is a proxy server designed to bypass Cloudflare and DDoS-GUARD protection.

## Important Status Information

⚠️ **FlareSolverr is currently non-functional** and is being monitored by the Cloudflare team, making it unlikely to be fixed.

**Workaround:** If you need FlareSolverr for an indexer, try different base URLs until you find one that works. If none work, you're out of luck.

## Key Usage Rules

- FlareSolverr proxy is only used when Cloudflare is detected by Prowlarr
- Proxy is only used if the proxy and indexer have matching tags
- A proxy without tags or without matching indexer tags will be disabled

## Installation Steps

### 1. Install FlareSolverr

Follow the official installation instructions from the [FlareSolverr GitHub repository](https://github.com/FlareSolverr/FlareSolverr#installation).

### 2. Add FlareSolverr to Prowlarr

1. Go to **Settings** → **Indexers**
2. Click the **+** sign and select **FlareSolverr**
3. Configure the following:
   - **Name**: Choose a name for the proxy in Prowlarr
   - **Tags**: Set tags for this proxy
   - **Host**: Full host path (including http and port) to your FlareSolverr instance
   - **Request Timeout**: Set between 1-180 seconds (default: 60 seconds)
4. Test the connection
5. Click **Save** if the test works

### 3. Configure Indexer to Use FlareSolverr

1. Select the indexer you want to use with FlareSolverr
2. Scroll to the bottom and add the tag you configured in step 2
3. Click **Test** and **Save**

The indexer should now use FlareSolverr when needed.

## Support Information

- For FlareSolverr-specific issues, use their [GitHub support](https://github.com/FlareSolverr/FlareSolverr/issues/1253)
- Servarr/Sonarr support cannot help with FlareSolverr issues unrelated to Prowlarr integration
- For general questions about this guide, contact [Trash Guides Discord](https://trash-guides.info/discord)
