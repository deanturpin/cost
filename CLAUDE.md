# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A single-page web application that calculates meeting costs in real-time. Pure HTML/CSS/JavaScript with no build step or dependencies. Designed to work on any device (phone and laptop) with zero installation.

## Architecture

**Single-file application**: The entire application is contained in `index.html` with embedded CSS and JavaScript. This deliberate design choice enables:

- Zero build step
- Instant deployment
- Works offline
- No dependency management
- Add to home screen on mobile (PWA-ready)

**Core calculation**: Meeting cost = (salary / 2,080 working hours per year / 3,600 seconds per hour) × attendees × elapsed time

**State management**: Simple JavaScript variables track meeting state (active/inactive, start time, interval timer). No framework needed.

**Visual feedback system**: The cost display changes colour and animation intensity based on cost thresholds:

- < £50: Blue/purple gradient (calm)
- £50-100: Orange tones with pulse animation (intense)
- £100-200: Red tones with faster pulse (very intense)
- £200+: Deep red with rapid pulse (extremely intense)

Font size dynamically scales down as numbers grow to prevent overflow, whilst maintaining drama for smaller costs.

## Development Workflow

### Local development

Simply open `index.html` in a browser. Make changes, save, and refresh. No build step required.

### Deployment

```bash
make deploy
```

This will add all changes, commit, and push to GitHub. GitHub Pages will automatically deploy the updated version.

### Testing changes

Test on both desktop and mobile browsers. The datetime-local input behaves differently across browsers and devices, so verify the user experience on target platforms.

## Code Style

**British English**: Use British spellings (colour, behaviour, etc.) throughout code and comments.

**No dead code**: Remove unused code completely rather than commenting it out. Trust version control.

**Timing precision**: The display updates 10 times per second (every 100ms) for dramatic effect, but cost calculations use precise milliseconds to maintain accuracy.

## Design Constraints

**Must remain a single file**: Do not split into separate JS/CSS files unless absolutely necessary. The single-file design is a feature, not a limitation.

**No dependencies**: Avoid introducing npm, frameworks, or build tools. If functionality requires external libraries, reconsider the approach or embed minimal code inline.

**Mobile-first**: Any UI changes must work well on small screens. Test responsiveness at narrow widths.

## Future Enhancements (per DESIGN.md)

The DESIGN.md outlines ambitious features (backend API, database, CLI, analytics dashboard), but the current implementation deliberately stays minimal. Only add complexity if explicitly requested, and favour client-side solutions (LocalStorage for history, CSV export via data URLs, etc.) over backend infrastructure.
