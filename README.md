# Meeting Cost Calculator

Calculate the real cost of meetings in real-time. Works on any device with zero installation.

## Overview

A simple web app that calculates meeting costs as they happen, helping organisations understand the financial impact of their meetings. Works on phone and laptop, installable as a PWA, and functions offline.

## Features

- **Real-time cost counter**: Watch costs accumulate as meetings progress
- **Attendee salary input**: Anonymous or role-based salary tracking
- **Meeting history**: Track costs over time with LocalStorage
- **Mobile-friendly**: Responsive design, works on any device
- **Offline capable**: Progressive Web App (PWA)
- **Zero installation**: Just visit the URL or add to home screen
- **Export data**: Download meeting history as JSON/CSV

## Quick Start

Visit the live version at: `https://[your-github-username].github.io/cost/`

Or open `docs/index.html` locally in your browser.

On mobile: Add to home screen for app-like experience.

## Technical Stack

- **HTML/CSS/JavaScript**: Pure web technologies, no build step required
- **LocalStorage**: Client-side data persistence
- **PWA**: Progressive Web App for offline use and home screen install
- **Deployment**: GitHub Pages (free, automatic)

## Core Calculation

The calculator uses the following formula:

```
Cost per second = (Sum of attendee salaries) / (Working hours per year × 3600)
Meeting cost = Cost per second × Meeting duration (seconds)
```

Assuming:

- 52 weeks per year
- 5 working days per week
- 8 hours per day
- Working hours per year = 52 × 5 × 8 = 2,080 hours

## Development

No build step required! Just edit `docs/index.html` and refresh your browser.

### Deployment

GitHub Actions automatically deploys to GitHub Pages on every push to main.

1. Edit `docs/index.html`
2. Commit and push changes
3. GitHub Actions deploys automatically
4. Visit `https://[your-username].github.io/cost/`

### First-time Setup

Enable GitHub Pages in repository settings:
- Go to Settings > Pages
- Source: GitHub Actions
- The workflow will handle the rest

## Licence

MIT

## Contributing

Contributions welcome! Please open an issue first to discuss proposed changes.
