# SidelineReel: Human-in-the-Loop Roster Tagging Confidence Flow
> **Ajaia LLC - Product Manager Assessment**  
> **Candidate:** Ayush Kabra (`akabra392@gmail.com`)  
> **Live Prototype:** Open `index.html` in any modern web browser or deploy via GitHub Pages.

---

## 🎯 Executive Summary & The Roadmap Call

### The Situation
SidelineReel is Ajaia's youth sports highlight application. The product promise is simple: a coach uploads game footage, and SidelineReel uses computer vision to detect each child’s moments (goals, saves, tackles), cuts them into a personalized reel for that child, and auto-assembles a weekly team recap sent to families.

### The Deliberate Trap in the Assessment Materials
1. **The Loudest Signal (Materials 1 & 4):** Carla Reyes (Ridgeline Youth SC, $180k/yr account) and Jamal Whitfield (VP of Sales) urgently demand **full live streaming** in six weeks, threatening non-renewal.
2. **The Say/Do Trap (Material 2):** 58% of parents surveyed ask for *"More editing controls"*. Yet telemetry shows only 6% ever open the editor, and fewer than 1% finish an edit.
3. **The Root Cause (Materials 3 & 5):** 
   - Support tickets across three separate clubs show swapped jersey digits (e.g., #14 misidentified as #4, #1 misidentified as #11).
   - The headline "92% Reel Share Rate" is a vanity metric calculated **only on opened reels**.
   - Footnote: **~30% of reels are never opened at all**—primarily because the video thumbnail shows the wrong child or notifications drop late at night.

### Why Livestreaming and Reel Editor are Deliberately NOT Built Next
- **Reel Editor (Say/Do Gap):** Building complex mobile editing tools solves what parents *say*, not what they *do*. Parents want effortless, accurate highlights delivered to their phones.
- **Livestreaming (Strategic Discipline):** Live streaming requires high-bandwidth sideline uplink hardware, substantial streaming server infrastructure, and low latency video ingestion—a massive multi-quarter distraction. Furthermore, Carla herself confirms: *"SidelineReel's highlight reels are a big part of why half our parents renewed this year, genuinely."* If reels feature the wrong kids and go unopened, the core foundation collapses.
- **The Correct Move:** We resolve Carla's renewal by guaranteeing **100% accurate reels and thumbnail reliability**, while committing to a structured discovery/scoping track for livestreaming, protecting our core value proposition first.

---

## 🚀 The Solution: Human-in-the-Loop Roster Tagging Review

When computer vision digit identification falls below **75% confidence** (due to folded jerseys, motion blur, or partial shadows):
1. **Flag Ambiguity:** SidelineReel isolates the low-confidence clip and prevents it from contaminating a child's reel.
2. **Side-by-Side Candidate Resolution:** The coach is presented with candidate roster matches (e.g., #14 Mia vs #4 Leo) with field location and position context.
3. **Sub-30-Second Coach Review:** The coach confirms the correct child with a single tap.
4. **Optimized Delivery Window:** Recaps are scheduled for peak family viewing (6:30 PM) rather than late-night batch deliveries, eliminating unopened reels.

---

## 📱 Prototype Architecture (The 3 Core Screens)

This repository contains a standalone, zero-dependency, clickable prototype built in HTML5, Tailwind CSS, and vanilla JavaScript:

### Screen 1: Coach Dashboard
- Match processing summary (Ridgeline U12 Boys, 24 highlights detected).
- High-visibility action banner: `⚠️ 3 clips need review — jersey number unclear before auto-recap sends tonight`.
- Status showing 21 auto-verified clips (95%+ confidence) and scheduled delivery countdown (6:30 PM).

### Screen 2: Interactive Review Screen (Confidence Verification)
- Computer vision simulation: detected jersey `#4?` at **62% AI confidence** with detected digit fold explanation.
- Candidate comparison cards: **Mia Thompson (#14 - Forward)** vs. **Leo Vance (#4 - Center Back)** with position and statistical likelihood.
- Action triggers:
  - `[Confirm #14 & View Updated Reel]` (Instant one-click demo path)
  - `[Confirm & Next Clip]` (Review remaining queue: Lucas #11 vs #1, Sophia #17 vs #7)
  - `[Skip / Leave Unassigned]` (Excludes clip from private reel while preserving raw footage)

### Screen 3: Confirmation & Auto-Recap Delivery Preview
- Hero confirmation banner: `🎉 Reel Updated — Correct kid tagged!`
- Value-add badge: `Prevented 1 false notification & wrong thumbnail delivery to Mia's family`.
- Verified personal reel with club watermark in corner (resolving Material 3 coach ticket).
- Scheduled delivery card for 18 roster families at 6:30 PM dinner window.

---

## 💻 How to Run & Test

### Option 1: Instant Local Run (No Installation Required)
Simply double-click or open `index.html` in Google Chrome, Apple Safari, Microsoft Edge, or Mozilla Firefox.

### Option 2: Run via Any Local HTTP Server
```bash
# Python 3
python -m http.server 8000

# Node.js
npx serve .
```
Navigate to `http://localhost:8000`.

---

## 🌐 Deploy to GitHub Pages (2 Minutes)

To submit this prototype as a live URL:
1. Initialize git and push to your GitHub account:
   ```bash
   git init
   git add .
   git commit -m "feat: SidelineReel Roster Tagging prototype for Ajaia assessment"
   git branch -M main
   git remote add origin https://github.com/<your-username>/sidelinereel-prototype.git
   git push -u origin main
   ```
2. In your GitHub repository:
   - Go to **Settings** > **Pages**.
   - Under **Build and deployment** > **Branch**, select `main` and root `/`.
   - Click **Save**.
3. Your live prototype will be published at:  
   `https://<your-username>.github.io/sidelinereel-prototype/`

---

## 📋 Complete Assessment Specification (Task 2 Mapping)

| Spec Component | Implementation in Prototype |
| :--- | :--- |
| **Outcome** | Reduce unopened generated reels from 30% to &lt;10%; achieve zero false-kid highlight deliveries across all pilot clubs. |
| **In Scope** | Confidence threshold flagging (&lt;75%); side-by-side roster disambiguation UI; coach single-tap confirmation; scheduled 6:30 PM push notifications. |
| **Out of Scope** | Full in-app video trimming/editing suite; live streaming infrastructure; real-time camera hardware integration. |
| **Human in the Loop** | Coach is prompted only when AI confidence is ambiguous (&lt;75%). If coach doesn't review by 6:00 PM, clip is excluded from personal reels and kept in full match replay. |
| **Top 2 Failure Modes** | **1. Coach Fatigue:** Too many clips flagged. *Mitigation:* Cap review queue at max 5 clips per match; auto-omit remainder from personal reels. <br>**2. Coach Inaction:** Coach ignores notification. *Mitigation:* Fail-safe rule: unverified clips never enter individual kid reels. |
