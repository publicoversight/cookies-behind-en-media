
This is an interactive network map showing the third-party tracking domains embedded in 20 of the most popular english news websites.

##Nodes##
Every node is either a news outlet or a company collecting data about its readers. 
##Edges##
Every edge is a real connection detected during a live browser crawl.

##Step 1 - Playwright##
Used Playwright, a headless browser automation tool, to visit each news site the way a real reader would. 
For each visit the crawler:
- Intercepted every network request the page made
- Identified all third-party domains (any domain different from the news site itself)
- Simulated scrolling to trigger lazy-loaded trackers
- Attempted to click cookie consent banners to capture the full post-consent tracker set
- Collected all cookies set by third-party domains, including name, expiry date, and security flags
Each site was visited in a clean browser context with no prior cookies, so results were not contaminated between sites.

##Step 2 -  Enrichment with DuckDuckGo Tracker Radar##
Cross-referenced every detected domain against the DuckDuckGo Tracker Radar dataset.
It is an open database built from millions of real browser sessions. 
The goal was to retrieve:
- Owner — the real company behind the domain (e.g. Google LLC, Adobe Inc.)
- Category — what the tracker does (Ad Motivated Tracking, Analytics, CDN, Fingerprinting)
- Prevalence — how widely the tracker appears across the web

##Step 3 — Graph##
Each news outlet and each vendor is a node. 
Each detected relationship is an edge. 
Nodes are sized by the number of connections they have; the more news sites a vendor appears on, the larger its node. 
Vendor nodes are colored by category.

##Limitations##

- Consent walls: some outlets (particularly European ones) block all trackers until a user clicks "Accept All". Where our consent-click automation failed, vendor counts may be lower than reality.
- Dynamic trackers: some vendors only load after specific user interactions like video plays or ad clicks, and are not captured here.
- Point in time: tracker relationships change. This data reflects a single crawl done 1rst June 2026.

##Data files##
docs/nodes.json — all outlet and vendor nodes with owner and category metadata
docs/edges.json — all detected connections between outlets and vendors
