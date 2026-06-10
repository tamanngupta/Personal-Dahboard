# Personal Dashboard
### A personal life command center — built from scratch, hosted on GitHub Pages.
(In progress, 4 tabs are yet to be build)

---

## What This Is

A fully offline, no-backend personal dashboard with a visual apartment building navigation metaphor. Every section of your life lives in a glowing window. Click a window, enter that section. All data is stored in your browser's `localStorage` — nothing leaves your machine.

---

## File Structure

```
index.html          ← the building / home screen
academic.html       ← books, laptops, scholarships, skills, courses, assignments, exploring
wardrobe.html       ← wishlist, owned, dream shelf, budget, spend history, capsule planner
tools.html          ← personal app store with field notes
people.html         ← network tracker, connection graph, linkedin, birthdays
ideas.html          ← build log + shower thoughts (coming soon)
budgeting.html      ← expense planning (coming soon)
health.html         ← cycling log, workout tracker, heatmap (coming soon)
overview.html       ← north star goals + contribution map (coming soon)
README.md           ← this file
```

---

## Setup

### 1. Host on GitHub Pages

1. Create a new GitHub repository (public or private — Pages works on both with the right plan)
2. Upload all `.html` files to the root of the repo
3. Go to **Settings → Pages → Source → Deploy from branch → main → / (root)**
4. Your dashboard will be live at `https://yourusername.github.io/yourrepo/`

No build step. No npm. No config. Just files.

---

## Places You Need to Add Your Own IDs / Keys

### Google Calendar OAuth (`academic.html`)

The scholarship, course, and assignment deadline export uses Google Calendar API via OAuth. This lets you click 🗓 next to any deadline and add it directly to your Google Calendar.

**Where to add it:**
In `academic.html`, find this line near the top of the `<script>` block:

```javascript
const GCAL_CLIENT_ID = 'YOUR_CLIENT_ID_HERE.apps.googleusercontent.com';
```

**How to get your Client ID:**
1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Create a new project (or use an existing one)
3. Enable the **Google Calendar API**
4. Go to **APIs & Services → Credentials → Create Credentials → OAuth 2.0 Client ID**
5. Application type: **Web application**
6. Add your GitHub Pages URL to **Authorised JavaScript origins** (e.g. `https://yourusername.github.io`)
7. Copy the Client ID and paste it in place of `YOUR_CLIENT_ID_HERE`

> Note: While your app is in "Testing" mode in Google Cloud Console, only email addresses you add as test users can use the calendar connection. Add your own Gmail under **OAuth consent screen → Test users**.

---

### Pinterest Board (`wardrobe.html`)

The Pinterest panel in the Wardrobe → Wishlist tab loads your board in an embedded iframe. By default it points to a placeholder URL.

**Where to change it:**
In `wardrobe.html`, find the iframe inside the `pinterest-panel` div:

```html
<iframe src="https://in.pinterest.com/tommy20090/college/" ...></iframe>
```

Replace `https://in.pinterest.com/tommy20090/college/` with your own Pinterest board URL.

**Format:** `https://www.pinterest.com/yourusername/boardname/`

> Note: Pinterest blocks iframes by default. You need the **Ignore X-Frame-Options** browser extension (or similar) for this to load. Without it you'll see a blank panel — the fallback is right-clicking any pin → Copy image address → pasting into the Add Item form.

---

### LinkedIn iframe (`people.html`)

The LinkedIn tab embeds LinkedIn directly.

**Where to change it (optional):**
In `people.html`, find:

```html
<iframe id="linkedin-iframe" src="https://www.linkedin.com" ...></iframe>
```

You can change the `src` to a specific LinkedIn URL like your own profile or network feed. Same extension requirement as Pinterest applies.

---

## Features by Section

---

### Home (`index.html`)

- Apartment building at night with twinkling stars
- Each of the 10 windows links to a section
- Hover a window — it glows and a silhouette animates (cycling wheels spin, wardrobe clothes sway, budget bars bounce, etc.)
- Daily rotating greeting (mix of locked-in and chaotic energy)
- Daily rotating quote (updated once per day based on date)
- Date displayed with proper capitalisation

---

### Academic (`academic.html`)

**Books**
- Hotspot table for your reading list
- Type a title → author, genre, and cover image auto-fill from the **Google Books API** (free, no key needed)
- Track start date, end date, status (reading / done), and a Notion link for your notes
- Completed books appear in a horizontal carousel with cover art

**Laptops**
- Manual research cards — one card per laptop
- Fields: name, price, weight, battery, key specs, deal breaker, review/word-of-mouth notes, priority score
- Edit or remove any card

**Scholarships**
- Hotspot table with deadline countdown (turns red under 7 days, amber under 14)
- Fields: name, amount, deadline, eligibility, status (spotted / applying / applied / heard back), link
- 📅 button exports a `.ics` file for any deadline (opens in Google Calendar, Apple Calendar, etc.)
- 🗓 button adds directly to Google Calendar (requires OAuth setup above)
- Stats bar shows total pipeline value, actively applying count, applied count

**Skills + Courses + Assignments** (three sub-tabs)
- Skills: name, level (beginner / building / solid shown as dot indicators), why you want it, how you're learning it
- Courses: name, platform, cost, hours, skill it feeds, deadline with calendar export, link
- Assignments: name, subject, deadline with calendar export, status (to do / in progress / submitted / graded), notes

**Exploring** (formerly Career Paths)
- Cards with a gut-score dial (1–10)
- Fields: path title, what excites you, what you'd need, someone you admire in that field, gut score, last updated date

**Deadline Strip**
- A persistent bar at the top of academic.html showing your 5 nearest deadlines across all subsections
- Colour-coded: red = ≤3 days, amber = ≤7 days, green = fine

---

### Wardrobe (`wardrobe.html`)

**Wishlist**
- Add items with image URL (right-click any Pinterest pin → copy image address) or upload from device
- Fields: name, image, category, price, priority (need / want / dream), season, notes
- Filter by category
- Mark as Bought → item moves to Owned + auto-logs the spend in history
- Pinterest board panel (toggle with Pinterest button — requires extension)
- Import from Pinterest CSV (Settings → Privacy → Export your data → unzip → Connections.csv... actually for Pinterest: Settings → Privacy and data → Request your data)

**Owned**
- Same grid as wishlist, your actual wardrobe
- Filter by category

**Dream Shelf**
- Aspirational items — no budget pressure, just logged desire

**Budget**
- Per-category spending limits (tanks/crops, tees, outerwear, jeans/trousers, shorts, shoes, accessories, sets, other)
- Progress bars per category — green (under 75%), amber (75–99%), red (over)
- Total budget / total spent / remaining overview card
- Edit limits anytime

**Spend History**
- Auto-populated when you mark wishlist items as bought
- Log manually too: item name, category, amount, where you bought it, date
- Reverse chronological, deletable

**Capsule Planner**
- Pick items from your entire wardrobe (wishlist + owned + dream shelf)
- Selected pieces display together so you can visualise outfits
- Selection persists across tab switches
- Clear button to reset

---

### 🛠 Tools (`tools.html`)

- iOS-style app grid — rounded icons, name below, coloured status dot
- Status dot colours: green (daily use), amber (trying), red (dropped), grey (paused)
- Filter by status (all / daily / trying / paused / dropped)
- Filter by tags — tag filter chips auto-appear from your existing tags

**Adding a Tool**
- Paste the app URL → description, icon, and name auto-fetch from the site's metadata (og:description, og:image)
- Falls back to manual entry if fetch fails

**App Popout Panel** (slides in from right)
- Description
- Status toggle (click to change, saves immediately)
- Star rating (1–5)
- Standout feature input
- Tags — add/remove free-form tags
- Field notes — personal textarea for workflows, quirks, features you discovered
- Save / Delete buttons

---

### People (`people.html`)

**People Tab**
- Cards with avatar, name, role, company, last-talked indicator, notes preview
- Colour-coded last-talked dot: green (≤14 days), amber (≤45 days), red (overdue)
- "Reach out" nudge badge appears on stale connections
- ✓ Talked button logs today's date as last contact
- Search across name, company, notes, role
- Filter by type (friend / family / mentor / network)

**LinkedIn CSV Import**
- Export your connections from LinkedIn: Settings → Data Privacy → Get a copy of your data → Connections
- Click Import CSV, select the `Connections.csv` file
- Imports name, company, position, connected date, LinkedIn URL
- Skips duplicates automatically

**Connection Graph** (fullscreen)
- Opens as a full-screen panel
- Force-directed graph — nodes repel each other and settle organically
- **Toggle switch: Institution ↔ Role**
  - Institution mode: people sharing the same company/org are connected
  - Role mode: people in the same role bucket (Founder, Engineer, Student, etc.) are connected
- Role buckets: Founder, CEO/MD, Engineer, Designer, Intern, Student, Marketing, Analyst, Operations, Community, Creator, Entrepreneur
- Hover a node: connected nodes highlight, others dim, nearby nodes gently push away
- Click a node: opens that person's edit modal
- Drag nodes to arrange
- Scroll to zoom (zooms toward cursor)
- Pan by dragging empty space
- Simulation cools down over ~8 seconds and settles — stops jittering
- Labels toggle on/off
- Reset button randomises positions

**LinkedIn Tab**
- Embedded LinkedIn in an iframe
- Requires Ignore X-Frame-Options browser extension

**Birthdays Tab**
- Shows all people with birthdays logged, sorted by days until next birthday
- Countdown badge turns amber for anyone within 30 days

---

## Data Storage

Everything is stored in `localStorage` under these keys:

| Key | Contents |
|-----|----------|
| `books` | Reading list entries |
| `laptops` | Laptop research cards |
| `scholarships` | Scholarship entries |
| `skills` | Skills |
| `courses` | Courses |
| `assignments` | Assignments |
| `exploring` | Career path cards |
| `people` | All people / connections |
| `wishlist` | Wardrobe wishlist items |
| `owned` | Owned wardrobe items |
| `aspirational` | Dream shelf items |
| `wardrobe-history` | Spend history entries |
| `budget-limits` | Per-category budget limits (object) |
| `capsule-selected` | Currently selected capsule items (array of IDs) |
| `tools` | Tool entries |

**Backup:** Open browser DevTools → Application → Local Storage → right-click your site → copy all values. Paste into a `.json` file to back up.

**Transfer to another device:** Copy the localStorage JSON manually, or wait — a proper export/import feature is on the roadmap.

---

## Browser Requirements

- Any modern browser (Chrome, Edge, Arc, Firefox, Safari)
- For Pinterest and LinkedIn iframes: **Ignore X-Frame-Options** extension (Chrome/Edge) or equivalent
- For Google Calendar direct integration: your Google Cloud Console client ID set up as described above

---

## Roadmap (Sections Not Yet Built)

- `ideas.html` — build log + shower thoughts kanban
- `budgeting.html` — college expense planning, income tracking
- `health.html` — cycling log, workout tracker, GitHub-style heatmap
- `overview.html` — north star goals, contribution map across all sections, momentum score
- AI sidebar (Gemini free tier) — per-section "ask claude about this" button, deferred to later

---

*Built June 2026. Your world, your rules.*
