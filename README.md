
This is an interactive network map showing the third-party tracking domains embedded in 20 popular english news websites.

This project reveals how modern news websites connect to advertising and analytics ecosystems through real-time browser-tracked data flows.

---

## Overview

This visualization maps the hidden data infrastructure behind news consumption.

- **Nodes** → News publishers + tracking companies  
- **Edges** → Real third-party network requests observed during live browsing  

Each connection represents a **real data exchange** between a user-facing news site and an external tracking domain.

---

## Data Collection Pipeline

### 1. Browser Simulation (Playwright)

Using **Playwright**, a headless browser automation tool, each news site was visited as a real user would experience it.

During each session, the crawler:

- Intercepted all network requests in real time  
- Identified third-party domains (non-origin requests)  
- Simulated scrolling to trigger lazy-loaded trackers  
- Attempted cookie consent interactions to capture post-consent behavior  
- Captured third-party cookies (name, expiry, security flags)

Each site was visited in a **clean, isolated browser context** to ensure data integrity.

---

### 2. Tracker Enrichment (DuckDuckGo Tracker Radar)

All detected domains were enriched using the  
**DuckDuckGo Tracker Radar dataset**, an open-source database built from large-scale web measurements.

For each tracker, we retrieved:

- Owner (e.g., Google LLC, Adobe Inc.)  
- Category (Advertising, Analytics, CDN, Fingerprinting, etc.)  
- Web-wide prevalence  

---

### 3. Graph Construction

The dataset is modeled as a bipartite graph:

- **News outlets → Tracker vendors**
- Nodes are weighted by connectivity
- Vendor nodes are categorized and color-coded

Highly connected trackers emerge as structural hubs of the modern web.

---

## Limitations

- **Consent banners** may block trackers before user interaction
-  Some trackers load only after specific interactions (video play, ad clicks, etc.)
-   Data represents a single snapshot (**1 June 2026**)
-   Tracking ecosystems evolve continuously

---

## Insight

This project exposes the **invisible infrastructure of the modern web**, showing how journalism platforms are deeply interwoven with global data collection and advertising networks.

---

## interesting Future Avenues 
- Time-series tracking of vendor changes  
- Consent-mode comparison  
- Tracker clustering by category influence  

---

## Tech Stack

- Playwright (browser automation)
- Node.js (data pipeline)
- DuckDuckGo Tracker Radar (enrichment dataset)
- JSON graph modeling
