# SNUVC — SNU Venture Consulting

> *Global VC insight for student founders — delivered by Seoul National University undergraduates.*

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Google Apps Script](https://img.shields.io/badge/Google%20Apps%20Script-4285F4?style=flat&logo=google&logoColor=white)

**[▶ Live site](https://snuvc-venture-consulting.vercel.app)**

## Overview

SNUVC is the marketing and landing site for **Seoul National University Venture Consulting**, an undergraduate club that meets top-tier venture capitalists in Korea and Silicon Valley and channels those insights into hands-on consulting and acceleration for student and early-stage founders. The site is a single, self-contained `index.html` page — no build step, no runtime dependencies — that presents the club's value proposition, its investor and professor network, the team, and a working contact form. Lead submissions are captured serverlessly through a Google Apps Script Web App that writes into a Google Sheets backend.

## Technical Highlights

- **Zero-dependency single-page site.** The entire experience lives in one `index.html` file with all styling hand-written inline in a `<style>` block, after migrating off the Tailwind CDN. This removes any external CSS/JS dependency and lets the page render fully offline or from any static host.
- **Section architecture.** The page is composed as a sequence of semantic `<section>` blocks — Hero, About, Investor Network, Team, Services, and Contact — alternating between black / white / gray background themes (`.section-bg-black`, `.section-bg-white`, `.section-bg-gray`) for visual rhythm, with a fixed top navigation bar linking to each anchor.
- **Investor & professor network.** A dedicated `#investors` section splits contacts into **Korea** and **Silicon Valley** groups. Korea features real partners (한국투자증권, 블루포인트파트너스, Intervest) and a featured SNU Business School professor (이영민), each rendered as an `.investor-card` with name, position, and an insight description. Placeholder `.investor-card-coming` "Coming Soon" cards mark the in-progress Silicon Valley network expansion.
- **Team showcase.** The `#team` section renders six members as circular-avatar `.team-card`s, each with a cropped photo (`images/1.jpg`–`6.jpg`, `object-fit: cover` in a `border-radius: 50%` frame), name, department, and admission year.
- **Contact form → Google Apps Script → Google Sheets.** The contact form is wired to a Google Apps Script Web App endpoint. On submit, vanilla JS intercepts the event, collects `name` / `email` / `company` / `message` plus an auto-generated `ko-KR` `timestamp`, and POSTs the payload as JSON via the `fetch` API in `mode: 'no-cors'` to bypass CORS. The submit button is disabled during transmission to prevent duplicate sends, and success/error feedback is surfaced through a `.status-message` element before the button re-enables after a 3-second cooldown.
- **Scroll interactions.** Smooth anchor scrolling is implemented by intercepting every `a[href^="#"]` click and calling `scrollIntoView({ behavior: 'smooth' })`. An `IntersectionObserver` watches each section and applies a `fade-in` class (a CSS `@keyframes` opacity + translateY animation) as sections enter the viewport.
- **Responsive layout.** Card grids use CSS Grid with `repeat(auto-fit, minmax(...))` so column counts adapt fluidly to viewport width. A `max-width: 768px` media query collapses grids to a single column, hides the desktop nav links, and scales down hero/section typography and form padding for mobile.

## Features

- Fixed, theme-aware navigation with smooth in-page scrolling
- Hero section with a clear value proposition and call-to-action
- Investor & professor network split by region (Korea / Silicon Valley)
- Team profile cards with photos, departments, and class years
- Services breakdown (venture consulting + acceleration) with checkmark lists
- Serverless contact form backed by Google Apps Script + Google Sheets
- Scroll-triggered fade-in animations via Intersection Observer
- Fully responsive, mobile-first layout

## Tech Stack

| Layer | Technology |
| --- | --- |
| Markup | HTML5 (semantic sections) |
| Styling | Hand-written inline CSS3 (Grid, Flexbox, media queries, keyframe animations) |
| Interactivity | Vanilla JavaScript (Fetch API, Intersection Observer) |
| Backend | Google Apps Script Web App → Google Sheets |

## Getting Started

This is a static site with no build step. Clone the repository and open the page directly:

```bash
git clone https://github.com/hyunsoo3318-oss/SNUVC_venture_consulting.git
cd SNUVC_venture_consulting
open index.html        # macOS — or just double-click the file
```

### Configuring the contact form

The form posts to a Google Apps Script Web App URL defined as `SCRIPT_URL` in the inline `<script>` of `index.html`. To point it at your own Google Sheets backend, deploy an Apps Script Web App (`doPost` handler that appends rows to a Sheet) and replace the `SCRIPT_URL` constant with your deployment URL.

---

© 2025 SNUVC. All rights reserved.
