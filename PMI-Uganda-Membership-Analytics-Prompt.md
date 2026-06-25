# PMI Uganda Chapter, Membership Analytics, Standardized Prompt

Use this as the single source of truth when generating or revising the membership analytics artifact. It defines the data, every metric, every breakdown, every filter, the KPIs, and the branding.

---

## 1. Objective

Build a live, shareable HTML dashboard (artifact) that lets the PMI Uganda Chapter leadership analyze membership health for 2026: how active membership is growing month on month, how members break down by industry and certification, the age profile of current active members, and how many members are inactive each month. The artifact must be branded, filterable, and refreshable.

---

## 2. Data source

Workbook: `20260620_PMI JUNE MEMBERSHIP DATA 2026.xlsx`

### Sheet A, "Active members" (June 2026 active members)
This sheet is a monthly activity log. One row is written for each member for each month they are active.

| Column | Meaning | How to use it |
|--------|---------|---------------|
| B | First day of the month the member is active (activity month) | Group all metrics by this month |
| C | Member email, logged once per active month | Count of distinct emails in column C, grouped by column B, = active members that month |
| G | Certification(s) held | May contain multiple certs per cell; split before counting |
| Industry column | Member industry | Group active members by industry |
| Age group column | Member age band | Profile June 2026 active members by age |

Rule: a member counts as active in a given month only if their email appears in column C for that month (column B = that month).

### Sheet B, "All members"
Full roster, active and inactive. Use this to compute, per month:
- Total members on the roster
- Inactive members = total members minus active members
- Inactive ratio = inactive members / total members

> When reading the file, confirm the exact header names and the exact column letters for Industry and Age group, since only B, C, and G are fixed by the brief. Do not assume value lists; read the distinct values for industry, certification, and age group directly from the data.

---

## 3. Metrics to compute

### 3.1 Active membership growth (core)
For each month in 2026 (Jan to Jun, extend to full year as data arrives):
- Active members = distinct emails in column C for that month
- Month-on-month change (absolute) = active(this month) minus active(prior month)
- Month-on-month growth rate (%) = change / active(prior month) x 100
- Cumulative / year-to-date trend line
- Average monthly growth rate for the period
- Net new vs net lost members between consecutive months (entrants and drop-offs by comparing email sets month to month), if derivable

### 3.2 Industry breakdown
- Active members by industry, per month
- Industry share of total active members (%) for the selected month
- Industry trend over time (which industries are growing or shrinking)
- Top N industries ranked

### 3.3 Certification analysis (column G)
- Number of active members holding each certification, per month
- Handle multi-certification cells: split on the delimiter and count each certification separately (one member can appear in more than one certification group)
- Certification mix for the selected month (share per certification)
- Certification trend over time
- Certified vs non-certified active members, count and ratio, per month

### 3.4 Age group profile (June 2026 active members)
- Distribution of active members by age band for June 2026
- Show as count and as percentage
- Allow the same view for any selected month if age data exists across months

### 3.5 Inactive membership analysis (All members sheet)
- Total members, active members, inactive members, per month
- Inactive ratio (%) per month and its trend
- Active ratio (%) as the complement
- Flag months where inactive ratio rises

---

## 4. KPI summary cards (top of dashboard)
Driven by the latest selected month (default June 2026):
1. Total active members (selected month)
2. Month-on-month growth rate (%) with up/down indicator
3. Total members on roster
4. Inactive ratio (%)
5. Number of certified active members (and % certified)
6. Top industry by active members
7. Largest age group

---

## 5. Visualizations
- Line chart: active members trend across 2026, with a secondary line or bars for MoM growth rate (%)
- Bar chart: active members by industry (selected month), sortable, top N
- Stacked or grouped bar: certifications held by active members per month
- Donut/pie: age group distribution (June 2026)
- Line chart: inactive ratio (%) per month, with total vs active overlay
- Data table: per-month summary (active, total, inactive, inactive ratio, MoM growth) with export

Every chart updates when a filter changes. Show the underlying number on hover.

---

## 6. Filters (interactive controls)
- Month or month range (Jan to Dec 2026; default Jun 2026 for snapshot views, full year for trend views)
- Industry (multi-select)
- Certification (multi-select; includes a "Certified vs non-certified" toggle)
- Age group (multi-select)
- Member status (Active / Inactive / All)

Filters apply across all cards, charts, and the table. Persist the user's last filter selection.

---

## 7. Branding
PMI Uganda Chapter palette (confirm exact brand hex against the supplied swatch):
- Tangerine, primary accent: `#F4640C`
- Aqua, secondary: `#14BEE1`
- Violet, tertiary: `#5B1FC0`
- Black, text: `#111111`
- White, background: `#FFFFFF`

Use the PMI Uganda logo in the header. Charts should cycle through Tangerine, Aqua, Violet for series colors. Clean, executive, presentation-ready layout, since this is shown to the Chapter.

---

## 8. Data-quality handling
- Count distinct emails per month, do not double-count duplicate rows
- Parse column B as a date and bucket by year-month
- Split multi-value certification cells before counting
- Treat blank industry, certification, or age group as "Unspecified" rather than dropping the row
- Reconcile active counts between the activity log and the All members sheet; note any mismatch
- State the data window covered (which months actually have data) on the dashboard

---

## 9. Deliverable
A single self-contained, branded HTML live artifact with all KPIs, charts, filters, and the summary table, ready to share with the PMI Uganda Chapter. First version is a draft for review; refinements follow after feedback.
