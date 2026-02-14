# Moving to Czechia - n8n Workflows

A collection of [n8n](https://n8n.io/) automation workflows to help families and individuals relocating to Czechia.

## Sreality Search & Filter

An automated apartment search workflow that monitors [Sreality.cz](https://www.sreality.cz/) for rental listings matching your criteria and sends email notifications with matching results.

### What it does

1. Runs on a schedule (every 4 hours by default)
2. Fetches rental listings from the Sreality API for your chosen city and districts
3. Filters by **price**, **usable area**, and **commute time** (via Google Maps)
4. Skips apartments you've already been notified about
5. Sends an email summary of new matching apartments via Gmail

### Prerequisites

- An **n8n instance** (self-hosted or cloud)
- A **Google Maps API key** with the Distance Matrix API enabled ([get one here](https://console.cloud.google.com/apis/credentials))
- **Gmail OAuth credentials** configured in n8n ([n8n Gmail docs](https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.gmail/))

### Setup

1. **Import the workflow** into n8n:
   - Open your n8n instance
   - Go to **Workflows** > **Add workflow** > **Import from file**
   - Select `workflows/sreality-search-filter.json`

2. **Configure the parameters** — open the node called **"Set Parameters - Only thing to setup"** and fill in:

   | Parameter | Type | Description | Example |
   |-----------|------|-------------|---------|
   | `maxPrice` | Number | Maximum rent in CZK | `40000` |
   | `minUsableArea` | Number | Minimum usable area in m² | `60` |
   | `maxDistanceTime` | Number | Max commute time in **minutes** (public transit) | `20` |
   | `maxDistanceLatLon` | String | Target address as `lat,lon` (e.g. your workplace or school) | `50.0755,14.4378` |
   | `googleMapsApiKey` | String | Your Google Maps API key | |
   | `emailRecipient` | String | Email recipients, comma-separated | `you@gmail.com` |
   | `maxLastUpdateDays` | Number | Ignore listings older than N days (useful for first run) | `7` |
   | `city` | String | Sreality city ID (`10` = Prague) | `10` |
   | `regions` | String | District IDs, separated by `%7C` (URL-encoded `\|`) | `5001%7C5002%7C5005` |

   > **City & region codes:** The Sreality API is undocumented. `10` = Prague, and the 5000-series are Prague districts (5001 = Prague 1, 5002 = Prague 2, etc.). For other cities, try asking an AI assistant for the codes.

3. **Set up Gmail credentials** — open the **"Send a message"** node and connect your Gmail OAuth credentials.

4. **Activate the workflow** — toggle it on. It will run every 4 hours and email you any new matching apartments.

### How it works internally

- On first run, the workflow automatically creates two n8n data tables (`sreality_hash_ids` and `Valid Apartments`) for state management
- `sreality_hash_ids` tracks apartments you've already seen (deduplication)
- `Valid Apartments` is a temporary table used during each run to collect results before emailing
- Old entries are automatically cleaned up after 7 days
- A 10-second delay between API calls avoids rate limiting from Sreality

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on how to contribute workflows, report bugs, or suggest improvements.
