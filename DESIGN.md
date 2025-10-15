# Meeting Cost Calculator - Design Document

## Core Calculation Logic

### Basic Formula

```
Hourly rate = Annual salary / Working hours per year
Cost per second = Hourly rate / 3600
Meeting cost = Cost per second × Duration (seconds) × Number of attendees
```

### Constants

- Working days per year: 260 (52 weeks × 5 days)
- Working hours per day: 8
- Total working hours per year: 2,080

## CLI Implementation

### Commands

1. **start** - Start a real-time meeting cost counter
   - Options:
     - `--attendees N` or `-a N` - Number of attendees
     - `--salary N` or `-s N` - Average annual salary
     - `--salaries N1,N2,N3` - Individual salaries (comma-separated)

2. **calculate** - Calculate cost for a completed meeting
   - Options:
     - `--duration N` or `-d N` - Duration in minutes
     - `--attendees N` or `-a N` - Number of attendees
     - `--salary N` or `-s N` - Average annual salary

3. **report** - Generate meeting cost reports
   - Options:
     - `--period daily|weekly|monthly`
     - `--format json|csv|table`

### Example Usage

```bash
# Real-time counter
cost-calculator start --attendees 5 --salary 50000

# Calculate past meeting
cost-calculator calculate --duration 60 --attendees 5 --salary 50000

# Generate report
cost-calculator report --period weekly --format table
```

## Web Implementation

### Frontend Components

1. **MeetingCounter** - Real-time cost display
   - Start/stop/pause controls
   - Running cost display
   - Attendee list
   - Meeting timer

2. **AttendeeManager** - Manage meeting participants
   - Add/remove attendees
   - Role-based or anonymous salary input
   - Salary presets by role

3. **Dashboard** - Historical analytics
   - Cost trends over time
   - Most expensive meetings
   - Department comparisons
   - Efficiency metrics

4. **ReportGenerator** - Export capabilities
   - PDF reports
   - CSV exports
   - Shareable links

### Backend API Endpoints

```
POST   /api/meetings              Create new meeting
GET    /api/meetings              List meetings
GET    /api/meetings/:id          Get meeting details
PATCH  /api/meetings/:id          Update meeting
DELETE /api/meetings/:id          Delete meeting

POST   /api/meetings/:id/start    Start meeting timer
POST   /api/meetings/:id/stop     Stop meeting timer
POST   /api/meetings/:id/pause    Pause meeting timer

GET    /api/analytics             Get analytics data
GET    /api/analytics/trends      Get cost trends
GET    /api/analytics/departments Get department costs

POST   /api/reports               Generate report
GET    /api/reports/:id           Download report
```

### Database Schema

```sql
-- Meetings table
CREATE TABLE meetings (
    id UUID PRIMARY KEY,
    name VARCHAR(255),
    start_time TIMESTAMP,
    end_time TIMESTAMP,
    duration_seconds INTEGER,
    total_cost DECIMAL(10,2),
    department VARCHAR(100),
    created_at TIMESTAMP DEFAULT NOW()
);

-- Attendees table
CREATE TABLE attendees (
    id UUID PRIMARY KEY,
    meeting_id UUID REFERENCES meetings(id),
    role VARCHAR(100),
    annual_salary DECIMAL(10,2),
    is_anonymous BOOLEAN DEFAULT true
);

-- Users table (for authentication)
CREATE TABLE users (
    id UUID PRIMARY KEY,
    email VARCHAR(255) UNIQUE,
    password_hash VARCHAR(255),
    organisation VARCHAR(255),
    created_at TIMESTAMP DEFAULT NOW()
);
```

## Deployment Strategy - Zero Installation

### Primary: Static Web App (Phone + Laptop)

**Goal**: Works on any device with a browser, zero installation

**Option 1: Client-side only (PWA)**

- Single HTML file with embedded JavaScript
- All calculations in browser
- LocalStorage for persistence
- Works offline
- Installable as PWA on phone
- Deploy to GitHub Pages, Cloudflare Pages, or Netlify
- **Zero backend required**

**Option 2: Serverless with minimal backend**

- Static frontend deployed to CDN
- Serverless functions (Vercel, Netlify, Cloudflare Workers)
- Database: Supabase or Firebase (free tier)
- Authentication: Built-in auth from platform
- Still feels instant, no server to maintain

### Secondary: Optional CLI (Power Users)

- Single binary, no dependencies
- For automated reporting and scripting
- Can work with same data via API

## Implementation Phases (Revised)

### Phase 1: Static Web MVP (PWA)

**Deliverable**: Single-page app, works offline, no backend needed

- HTML/CSS/JavaScript (or simple Vite + React)
- Real-time cost calculator
- LocalStorage persistence
- Responsive design (mobile-first)
- PWA manifest for "install on home screen"
- Deploy to GitHub Pages

**Features**:

- Start/stop meeting timer
- Add attendees with salaries
- See running cost
- Save meeting history locally
- Export to JSON/CSV

### Phase 2: Enhanced Features

**Deliverable**: Better UX, more analytics

- Role-based salary presets
- Meeting templates
- Basic charts (Chart.js)
- Dark mode
- Share meeting URL with calculations

### Phase 3: Optional Backend (if needed)

**Deliverable**: Multi-device sync and team features

- Add Supabase for database
- Sync across devices
- Team/organisation accounts
- Cloud backup of history

### Phase 4: Optional CLI

**Deliverable**: Automation and power-user features

- Go binary for CLI
- Can sync with web version via API

## Recommended Tech Stack for Minimal Friction

### Ultra-minimal (Phase 1)

```
Single HTML file + vanilla JavaScript
Deploy: GitHub Pages (free, automatic)
Storage: LocalStorage
Install: Add to home screen (PWA)
```

### Slightly better DX (still minimal)

```
Vite + React + TypeScript
Deploy: Vercel/Netlify (free, git push to deploy)
Storage: LocalStorage + optional Supabase
Styling: Tailwind CSS
```

## Next Steps

1. Create single-page web app with real-time calculator
2. Make it responsive and mobile-friendly
3. Add PWA manifest for home screen install
4. Deploy to GitHub Pages
5. Test on phone and laptop
6. Iterate based on real usage
