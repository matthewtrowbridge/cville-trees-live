# Charlottesville Tree Equity — Workshop Development Arc

**Workshop:** Design Thinking + AI Prototyping
**Setting:** UVA Batten School of Leadership and Public Policy, Social Entrepreneurship (Prof. Carmen Diaz)
**Date:** March 12, 2026
**Duration:** 90 minutes
**Participants:** Undergraduate students
**Facilitator:** Matt Trowbridge

---

## 1. The Setup

### Starting Material
A single `.csv` file: `cville-tree-inventory-sample.csv` — 200 trees from Charlottesville's tree inventory with columns for species, genus, sector (NW/NE/SW/SE), latitude, longitude, planting date, trunk diameter (DBH), managing agency, and condition rating.

### The Prompt (What Students Saw)
The prompt was intentionally open-ended — something like:

> "Here's a dataset of 200 trees from Charlottesville. Use Claude to explore this data and build something that could make a real difference for the community."

No specific output format. No wireframes. No technical requirements. The openness was the point.

### Why This Dataset
- **Local:** Students live in or near Charlottesville, so the data is personal
- **Approachable:** Trees are intuitive — everyone understands shade
- **Layered:** Simple on the surface, but connects to deep systemic issues (health, race, economics, climate)
- **Small enough:** 200 rows fit in a single Claude context window with room to spare

---

## 2. What Students Built (90 Minutes)

### Tool 1: Tree Equity Dashboard (City Council View)
**Design direction:** Dark, data-dense, analytical. Designed for a policy audience.

**What Claude did autonomously:**
- Identified that the tree data alone tells a limited story
- Found and integrated 5 additional public datasets: CDC PLACES 2025 (health by tract), ACS 2019-2023 (demographics), Charlottesville Heat Watch 2021 (temperature by tract), American Forests Tree Equity Scores, County Health Rankings (life expectancy)
- Created 10 census tract profiles with 15+ variables each
- Built an interactive bar chart with 9 switchable metrics
- Wrote a narrative analysis identifying the pattern: less shade → more heat → worse health → higher costs → shorter lives
- Highlighted the SW quadrant (10th & Page, Fifeville, Ridge Street, JPA) and its redlining history
- Calculated headline statistics: 10-year life expectancy gap, 4.3× canopy disparity, 12.8°F heat difference

**Key design decisions the AI made:**
- Color-coding by equity (red→green gradient)
- Comparison panel automatically contrasts selected tract with highest/lowest equity
- Historical context notes for each tract
- Energy burden as a metric (not obvious from tree data)

### Tool 2: Shade Score (Resident View)
**Design direction:** Warm, personal, Zillow-meets-health-app. Designed for individual residents.

**What Claude did autonomously:**
- Reframed the same data as a personal address lookup
- Created a street-name matching system so residents could type their address
- Designed a "Shade Score" ring visualization (0-100) with letter grades
- Built personalized insight cards: home value impact, cooling costs, cardiovascular health, kids & outdoor time, energy justice
- Added a "What You Can Do" action section with local organizations
- Generated a tree health visualization (healthy vs. struggling trees)
- Added property value and cooling cost estimates based on USDA Forest Service research

**Critical shift:** Same data, completely different audience, completely different emotional register. The dashboard says "here are the numbers." The Shade Score says "here's what this means for YOUR family."

---

## 3. The "One More Thing" — Post-Workshop Enhancement

After the workshop, I asked Claude Code to add features that would demonstrate the principle of "AI as thought partner" — capabilities students wouldn't think to ask for.

### Features Added

**Interactive Map (Leaflet.js)**
- Dark-themed CartoDB tiles on the dashboard
- Color-coded circle markers for each tract, synced to the active metric
- Fly-to animation when clicking a neighborhood — on the map OR the bar chart
- Light-themed mini-map on the Shade Score results showing your neighborhood

**Data Sonification (Web Audio API)**
- "Hear the Inequality" button on the dashboard
- Each neighborhood plays as a musical tone, sorted low→high equity
- Low-equity tracts: low pitch, harsh sawtooth wave
- High-equity tracts: high pitch, warm sine wave
- Final chord plays both extremes together — you literally hear the gap
- Visual equalizer bar animates in sync with playback

**Tree Planting Impact Simulator**
- Slider: 0 to 500 trees
- Real-time projected impact based on EPA/USDA research:
  - Canopy cover change (each tree ≈ 0.012% of tract canopy at maturity)
  - Temperature reduction (10% canopy ≈ 1.5°F cooling)
  - Annual energy savings (~$38/tree near homes)
  - Property value added (~$4,200/tree conservative)
  - CO₂ absorbed (48 lbs/year per mature tree)
- Contextual messages at 200+ and 400+ trees planted

**Google Maps Integration**
- Direct link from each Shade Score result to Google Maps at the tract's lat/lon
- "See this neighborhood" link for street-level exploration

### Why These Features Matter Pedagogically
None of these features were in the original prompt. They demonstrate:
1. **Technical possibility space** — students don't know what browsers can do (Web Audio, Leaflet, Canvas)
2. **Cross-modal thinking** — sonification is not a "data visualization" idea, it's an accessibility/art idea applied to data
3. **Simulation as persuasion** — the tree planting slider makes abstract policy feel tangible
4. **Spatial grounding** — maps make data feel real in a way charts don't

---

## 4. The Meta-Lesson

### The Prompt IS the Lesson

The most important thing that happened in this workshop wasn't any of the tools built. It was the realization that:

> **The way you engage an AI tool matters more than what you ask it to build.**

Asking "build me a dashboard" produces a dashboard. Asking "here's some data about trees — what could we build that would make a real difference?" produces two tools with different audiences, integrated public health data the students didn't know existed, and a narrative that connects canopy to cardiovascular disease to life expectancy to racial covenants.

And then asking "what's one more thing that would blow people's minds?" produces sonification, simulation, and spatial experiences.

### The Shareable Prompt
The prompt students can take away isn't a specific instruction. It's a pattern:

1. **Start with data, not a spec:** "Here's a dataset. What's interesting about it?"
2. **Ask for audience-specific versions:** "Who would care about this? Build something for each audience."
3. **Ask for surprises:** "What could we add that I wouldn't think to ask for?"
4. **Push for cross-modal:** "Can we experience this data in a completely different way?"

Each step produces something the previous step couldn't have imagined.

---

## 5. Technical Architecture

### Stack
- Single `index.html` file (~1,100 lines)
- React 18 (CDN, in-browser Babel transpilation)
- Leaflet.js (CDN, OpenStreetMap/CartoDB tiles)
- Web Audio API (native browser, no library)
- CSS-in-JS (inline styles, no external CSS)
- Hash-based routing (`#dashboard`, `#shade`)
- No build step, no node_modules, no bundler

### Why This Stack
- **Instant deployment:** One file → Vercel → live URL
- **Zero dependencies to install:** Open `index.html` in a browser and it works
- **Transparent:** Students can view-source and see everything
- **Matches the workshop arc:** Start simple, stay simple, add capability

### Data Architecture
All data is hardcoded in the JavaScript:
- `DASHBOARD_TRACTS`: 10 tracts × 15+ variables (income, health, canopy, heat, etc.)
- `SHADE_TRACTS`: Same 10 tracts with additional personal fields (streets array, home values, park distances, history notes)
- `DASHBOARD_METRICS`: 9 metric definitions with labels, units, and color direction

No API calls. No database. No backend. The entire application is a static file.

---

## 6. Data Sources & Methodology

| Source | What It Provides | How Claude Found It |
|--------|-----------------|-------------------|
| Uploaded CSV | 200 trees: species, location, condition, agency | Starting material |
| CDC PLACES 2025 | Heart disease, asthma, hypertension, obesity, diabetes rates by tract | Claude identified health correlation with canopy |
| ACS 2019-2023 | Median income, race/ethnicity, renter %, insurance rates | Claude identified demographic dimensions |
| Charlottesville Heat Watch 2021 | Afternoon temperature by tract | Claude connected canopy to urban heat island |
| American Forests | Tree Equity Scores (0-100) | Claude found the standard scoring framework |
| County Health Rankings | Life expectancy by tract | Claude identified the ultimate outcome metric |
| Community Climate Collaborative | Energy burden (% income on utilities) | Claude connected shade to household economics |
| UVA Center for Community Partnerships | Historical context (redlining, Vinegar Hill) | Claude provided neighborhood-level narrative |
| USDA Forest Service | Property value and cooling cost estimates | Claude grounded personal impact in research |

**Note:** The data as integrated represents Claude's synthesis across sources. Some tract-level values may be interpolated or estimated where exact census-tract-level data wasn't available. This is appropriate for a workshop prototype but would need validation for policy use.

---

## 7. Learnings

### What Worked
1. **Open-ended prompt** — Giving students data without a spec produced more creative output than a wireframe would have
2. **Two audience frames** — The council view vs. resident view split happened naturally from the data, not from instruction
3. **Claude's data integration** — Finding and merging 5+ public datasets in real-time was the biggest "wow" for students
4. **Personal connection** — Students could look up their own neighborhoods in the Shade Score tool
5. **90-minute constraint** — Forced focus, prevented over-engineering, created energy

### What Could Be Better
1. **Data validation** — Workshop prototypes shouldn't be presented as authoritative policy tools. Need clear "prototype" labeling.
2. **Address matching** — The street-name lookup is brittle (substring matching). A real tool would need geocoding.
3. **Mobile responsiveness** — Inline styles make responsive design harder. The dashboard works but isn't optimized for phone screens.
4. **Accessibility** — Color-coding carries information. Need alt text, ARIA labels, keyboard navigation.
5. **Student attribution** — The site credits "UVA Social Entrepreneurship students" generically. Individual/team credit would be better.

### Surprising Moments
- Claude finding the Heat Watch dataset and immediately connecting canopy % to afternoon temperature
- The energy burden metric — students didn't think of "how much of your income goes to cooling" as a tree issue
- The Vinegar Hill history appearing in the tract notes — Claude connected current canopy gaps to 1965 eminent domain
- Sonification — the sound of inequality is viscerally different from seeing it in a chart

---

## 8. Questions for Future Iterations

### Workshop Design
- **Could this work in 60 minutes?** The core loop (data → explore → build) might compress, but the reflection ("what else?") phase is where the learning happens.
- **What other datasets would work?** Water quality, air quality, food deserts, bike infrastructure, 311 requests — anything local with geographic variation and equity implications.
- **How to handle the "Claude did it" problem?** Students need to understand what Claude built vs. what they directed. The intellectual contribution is the question, not the code.
- **Should students use Claude Chat or Claude Code?** Chat is more accessible. Code produces deployable artifacts. Could do Chat for exploration, Code for packaging.

### Pedagogical Questions
- **How do you grade AI-assisted work?** The prompt, the iteration, the design decisions, and the interpretation are the student's work. The code is Claude's. How to assess?
- **What's the right balance of scaffolding?** Too much structure (wireframes, specs) kills the open-ended magic. Too little structure leaves students frozen. The dataset-as-starting-point seems right.
- **How to teach critical evaluation of AI output?** Claude's data synthesis looks authoritative but needs verification. How to build that critical lens without killing the creative momentum?

### Technical Questions
- **Should future workshops use a build step?** The single-file approach is great for deployment but limits what's possible (no TypeScript, no component imports, no testing). For a 90-minute workshop, the answer is no — simplicity wins.
- **What about real geocoding?** Could use the Nominatim API (free, OpenStreetMap-based) for real address-to-tract lookups. Adds complexity but makes the tool genuinely useful.
- **Could this connect to live data?** CDC PLACES and ACS have APIs. A real tool could pull current data instead of hardcoding. But that's a different project.

### Sharing & Impact
- **Who else should see this?** Carmen Diaz (for grading context), Batten administration (for program showcase), designing.health (as a case study), Charlottesville city council (if validated)
- **Should students present to city council?** The tools are compelling enough. But the data needs validation first.
- **How does this fit the HDS sharing strategy?** This is a proof point that the methodology works outside medical education, with undergrads, on civic data. Strong evidence for the "platform" tier of the three concentric circles.

---

## 9. Files & Links

### Repository
- **Local:** `~/Projects/cville-trees-live/`
- **GitHub:** `matthewtrowbridge/cville-trees-live`
- **Deploy:** Vercel (auto-deploy from main)

### Workshop Source Files
```
~/Documents/Work (iCloud)/Projects (Work)/MDP (iCloud)/
  MDP 4th Year Elective/10_Future Versions/
    Mini Workshops (HDS)/
      2026.03 Undergraduate DT (Batten Carmen Diaz)/
        Workshop Outputs (Batten Design Thinking)/
          ├── cville-tree-inventory-sample.csv        (200 trees, original input)
          ├── Tree Equity Dashboard/
          │   ├── cville_tree_equity_dashboard.jsx    (379 lines, React component)
          │   ├── cville_tract_equity_data.csv        (10 tracts, enriched)
          │   └── cville_trees_enriched.csv           (200 trees + tract join)
          ├── Shade Score Cville/
          │   └── shade_score_personal.jsx            (490 lines, React component)
          └── 2026.03.11 Student 90 min Workshop (Claude Session).html/.webarchive
```

### Direct Links (after deployment)
- Landing page: `<site-url>/`
- Dashboard: `<site-url>/#dashboard`
- Shade Score: `<site-url>/#shade`

---

## 10. The Arc in One Sentence

Students started with 200 rows of tree data and, in 90 minutes with Claude, built two tools that connect canopy gaps to a 10-year life expectancy disparity — then learned that the most powerful thing they could do was ask an open-ended question they didn't know the answer to.
