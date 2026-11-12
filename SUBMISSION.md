# Ajaia LLC - Product Manager Assessment: SidelineReel
**Candidate:** Ayush Kabra  
**Email:** akabra392@gmail.com  
**Working Prototype Link:** [GitHub Repository / Live Demo](https://github.com/akabra392/sidelinereel-prototype) *(or local `index.html` file submitted)*  
**Video Walkthrough Link:** [Public Loom / YouTube Video Link](https://youtu.be/...)

---

## Task 1. The Roadmap Call

### 1. The Core Strategic Assessment & The Deliberate Trap
A cursory reading of the assessment materials suggests an urgent crisis: Carla Reyes (Executive Director of Ridgeline Youth Soccer Club, our largest account at $180k/season) and Jamal Whitfield (VP of Sales) are forcefully demanding **live streaming** within six weeks, threatening non-renewal (Materials 1 & 4). 

However, evaluating the materials as a cohesive system reveals that this is a classic B2B trap. The real existential threat to SidelineReel is not the absence of livestreaming; it is that **our core product promise—delivering reliable, automated personal highlight reels to families—is failing silently.**

### 2. Evidence-Based Synthesis Across Materials
* **Material 3 (Systemic Roster Tagging Failure):** Support tickets across three separate clubs (soccer, lacrosse, baseball) report identical failures: jersey numbers with similar digits are swapped (14→4, 1→11, swapped digits). This is not an edge case; optical character recognition (OCR) on folded athletic jerseys suffers predictable digit ambiguity.
* **Material 5 (The Vanity Metric Exposed):** The internal dashboard boasts a **92% Reel Share Rate**, but the footnote reveals this is calculated *only on reels that were opened*. **~30% of generated reels are never opened at all.** Why? Because the notification arrives late at night, or because the reel’s thumbnail features the wrong child due to the jersey tagging bug. A parent whose thumbnail shows a stranger's kid will never click open, masking the churn signal.
* **Material 2 (The Say/Do Trap):** In quarterly surveys, 58% of parents requested *"More editing controls."* Yet behavioral telemetry reveals only 6% ever open the editor, and fewer than 1% complete an edit. Building more editing tools would be wasting engineering capacity on stated preference rather than revealed preference.
* **The Auto-Recap Anchor (Material 2 & Carla's Note):** The weekly auto-recap Share button is used in **90%** of recaps sent. Carla herself explicitly admits: *"SidelineReel's highlight reels are a big part of why half our parents renewed this year, genuinely."* If we fail on reels, livestreaming will not save the account.

---

### 3. Ranked Roadmap Candidates

| Rank | Feature / Initiative | Strategic Rationale & Evidence | Impact & Effort |
| :--- | :--- | :--- | :--- |
| **1 (Top Build)** | **Human-in-the-Loop Roster Tagging Confidence Verification** | Directly solves the digit-swap bug (Material 3) and eliminates the wrong-kid thumbnails driving the ~30% unopened reel rate (Material 5). Guarantees trust in our core value proposition before family signups open. | **High Impact / Medium Effort** |
| **2** | **Automated Recap Delivery Scheduling (Peak Engagement Window)** | Material 5 notes late-night notifications directly cause unopened reels. Shifting delivery from midnight cron batches to a dynamic local window (6:00–7:30 PM dinner hour) immediately rescues unopened reels at almost zero cost. | **High Impact / Low Effort** |
| **3** | **Health Metric Correction: True End-to-End Reel Open & Share Rate** | Re-instrument the dashboard to measure `Shares / Total Generated Reels` rather than conditioning on opened reels. Eliminates organizational blind spots. | **High Impact / Low Effort** |
| **4** | **Branded Watermark & Export Reliability Polish** | Fix the missing team logo watermark on phone camera roll exports (Material 3 ticket) to preserve organic viral acquisition when parents post to Instagram/TikTok. | **Medium Impact / Low Effort** |
| **5 (De-prioritized)** | **Multi-Sport App Icon Refresh** | Batch into the next scheduled seasonal app store release. Cosmetic improvement with low retention impact. | **Low Impact / Low Effort** |

---

### 4. What We Deliberately Will NOT Build Next (and Why)

#### 1. Full Live Streaming for Ridgeline (Explicit "NOT NEXT")
* **Why:** Full live streaming is a fundamentally different business requiring high-bandwidth field uplink, real-time cellular bonding/Wi-Fi infrastructure, high-concurrency RTMP streaming servers, and substantial latency management. In a 6-week timeframe, committing to build production live streaming across an entire league would result in broken streams, degraded video quality, and catastrophic churn.
* **How we handle Carla & Jamal:** Carla stated that highlight reels are why half her parents renewed. We defend the $180k renewal by delivering 100% accurate reels, guaranteed watermark branding for scouts, and an explicit commitment to a structured **Live Streaming Discovery Pilot** for next season (e.g., scoping a low-lift RTMP ingest or partner integration), rather than jeopardizing the roadmap with an impossible 6-week engineering commitment.

#### 2. Advanced Reel Editor (Say/Do Disqualification)
* **Why:** 58% of survey respondents asked for more editing controls, but usage data shows only 6% open it and &lt;1% finish. Youth sports parents are time-starved; they do not want to become video editors. They want an effortless, magical recap delivered automatically. Building what users *say* rather than what they *do* would destroy team focus.

---

## Task 2. The Product Specification: Human-in-the-Loop Roster Tagging Verification

### 1. Desired Outcome & Success Metrics
* **Primary Outcome:** Eliminate incorrect player tags in generated reels and weekly team recaps caused by jersey digit ambiguity.
* **Target Metrics:**
  * **Unopened Reel Rate:** Reduce unopened reels from ~30% to &lt;10% within 45 days of rollout.
  * **Tagging Accuracy:** Increase verified player tag precision to 99.5%+.
  * **Coach Time-to-Review:** 80%+ of flagged clips reviewed by coaches in under 45 seconds per game.
  * **True Reel Share Rate:** Increase overall share rate across *all generated reels* from ~64% to 80%+.

---

### 2. Scope

#### In Scope (V1 MVP)
1. **Confidence Threshold Trigger:** Any player detection where optical OCR confidence falls between **50% and 75%** (or where visual digit similarity is detected, e.g., 1 vs 11, 4 vs 14) is marked as `Needs Review`. Clips with >75% confidence auto-publish.
2. **Coach Review Dashboard Banner:** High-visibility banner on the post-match processing screen: *"X clips need review — jersey number unclear before family recaps send tonight"*.
3. **Side-by-Side Disambiguation UI:** A 1-tap review card displaying the ambiguous clip frame, the detected digit with confidence score, and candidate roster profiles with contextual clues (player name, position, on-field stats, headshot).
4. **Action Triggers:** Three explicit choices: `Confirm Candidate A`, `Confirm Candidate B`, or `Skip / Leave Unassigned`.
5. **Scheduled Delivery Safeguard:** Automated recap push notifications are scheduled for 6:30 PM local time. If a coach does not review by 6:00 PM, unverified clips are automatically excluded from private player reels and preserved in the full match archive.

#### Explicitly Out of Scope
* Manual video clipping or re-trimming tools.
* Live streaming capture or RTMP broadcasting.
* Full manual tagging of every player from scratch (AI handles 90%+ automatically).
* Direct parent-facing tagging or crowdsourced tagging (to protect child privacy and prevent parental disputes).

---

### 3. Where a Human Stays in the Loop
The system relies on **selective exception handling**. Instead of asking coaches to tag an entire 60-minute match, the AI handles all high-confidence detections (>75%) autonomously. A human (the coach) is looped in **only when the algorithm identifies mathematical ambiguity between rostered digits**. The coach acts as the high-accuracy validator in under 30 seconds, turning a potential point of failure into a trust-building moment.

---

### 4. Acceptance Criteria

| ID | Given | When | Then |
| :--- | :--- | :--- | :--- |
| **AC-1** | A match is processed and a jersey detection confidence is &lt;75% | The match processing completes | The clip is flagged as `Needs Review`, excluded from private reels, and surfaced in the Coach Dashboard banner. |
| **AC-2** | A coach opens the Review screen | The coach inspects an ambiguous clip | The screen displays side-by-side roster candidates with photo, position, and field context, along with `Confirm [Name]` and `Skip` buttons. |
| **AC-3** | The coach taps `Confirm [Player Name]` | The action is registered | The clip is immediately tagged to that player's personal highlight reel and team recap, updating the thumbnail hero frame. |
| **AC-4** | A coach taps `Skip / Leave Unassigned` | The action is registered | The clip remains in the raw full match replay but is omitted from individual player highlight reels. |
| **AC-5** | Auto-recap delivery time (6:30 PM) is reached and flagged clips remain unreviewed | The automated cron trigger fires | The system publishes reels using only verified clips. Unreviewed clips are silently withheld to prevent wrong-kid notifications. |

---

### 5. Top Two Failure Modes & Detection Mechanisms

#### Failure Mode 1: Coach Notification Fatigue & Low Review Completion
* **The Risk:** Coaches find the review requests annoying or ignore them, causing clips to sit unreviewed and kids to miss highlights.
* **What Catches It:** **Review Drop-off Telemetry & Cap Limits.**
  * *Telemetry Guard:* We track the `Review Completion Rate` (% of flagged clips reviewed before 6:00 PM). If this drops below 70%, an alert triggers.
  * *Product Safeguard:* Hard-cap the review queue at a maximum of **4 clips per match**. Any lower-priority ambiguities are automatically handled by fail-safe withholding.

#### Failure Mode 2: Coach "Rubber-Stamping" (Careless Confirmation)
* **The Risk:** Coaches rush through the UI and blindly tap the first candidate, inadvertently confirming the wrong child.
* **What Catches It:** **Parent Support Inquiries & Confidence Discrepancy Audits.**
  * *Telemetry Guard:* Track post-delivery support tickets citing *"wrong kid in reel"* tagged by account ID.
  * *UX Safeguard:* Candidate cards are dynamically ordered based on positional and field tracking probability, requiring a deliberate tap with clear player names, numbers, and headshots.

---

## Task 3. Working Prototype Summary
* **Prototype Artifact:** A high-fidelity, interactive, mobile-first web application created in `index.html`.
* **Repository Path:** `C:\Users\Ayush\sidelinereel-prototype\index.html`
* **Core Screens Demonstrated:**
  1. **Coach Dashboard:** Ridgeline U12 Boys match processing status, showing 21 verified clips and the amber banner: *"3 clips need review — jersey number unclear before auto-recap sends tonight"*.
  2. **Review Screen (Confidence Disambiguation):** Simulated match footage with bounding box detecting `#4? (62% confidence)`. Side-by-side roster comparison between **Mia Thompson (#14, Striker)** and **Leo Vance (#4, Defender)** with one-tap confirmation.
  3. **Confirmation & Recap Preview:** Instant confirmation showing *"Reel updated — Mia Thompson (#14) tagged correctly"*, thumbnail verification with watermark, and scheduled 6:30 PM delivery preview for 18 families.
  4. **Interactive Controls:** Toggle between realistic Mobile Device Frame and Expanded Desktop view, plus an interactive "PM Spec Logic" inspector drawer.

---

## Task 4. AI Workflow Note

* **What I Used AI For:**
  * Synthesizing and cross-referencing qualitative support tickets against quantitative usage telemetry to isolate the digit-swap OCR pattern.
  * Generating the boilerplate HTML5/Tailwind responsive mobile frame and state machine logic for the 3-screen interactive prototype.
  * Drafting initial table schemas for acceptance criteria and edge-case failure modes.
* **What I Deliberately Kept Human:**
  * **The Strategic Roadmap Judgment:** Choosing to rank the $180k account's loud demand (livestreaming) down and defending it with data. AI models frequently succumb to client urgency bias and recommend building whatever the highest-paying customer demands.
  * **Identifying the Vanity Metric Trap:** Recognizing that the 92% share rate was calculated over an artificially filtered denominator (opened reels only) and connecting the footnote to the support tickets.
  * **The "Say/Do" Product Call:** Deliberately refusing to build the Reel Editor despite 58% survey demand, grounding the decision in behavioral telemetry (<1% completion).
* **One Specific Thing an AI Tool Got Wrong / Chose Not to Use:**
  * In early brainstorming, AI suggested building a *"Crowdsourced Parent Tagging Flow"* where parents could tag each other's kids. I rejected this entirely: allowing competitive youth sports parents to tag and re-tag other parents' children in private highlight reels creates severe privacy, moderation, and social friction. Keeping the coach as the single authoritative human-in-the-loop is essential.

---

## 🎥 Video Walkthrough Script (5–7 Minute Target)

### [0:00 - 1:15] Task 1: The Roadmap Call & Avoiding the $180k Trap
> *"Hi everyone, I'm Ayush Kabra. When looking at the five materials for SidelineReel, the most obvious signal is Carla from Ridgeline Youth SC—our $180k marquee account—demanding livestreaming in six weeks under threat of non-renewal.*  
>  
> *A junior PM would immediately put livestreaming at the top of the roadmap to satisfy sales. But when you synthesize all the data, that is a trap.*  
>  
> *Look at Carla's own email: she says, 'SidelineReel's highlight reels are a big part of why half our parents renewed this year.' Highlight reels are our core retention driver. Yet when you inspect Material 3 and Material 5, our core is leaking:*  
> *1. Three support tickets from different clubs show jersey numbers with similar digits getting swapped—14 to 4, 1 to 11.*  
> *2. Our dashboard shows a 92% share rate, but that only counts reels that parents opened. 30% of generated reels are NEVER opened at all—because the notification comes late at night, or because the thumbnail shows the wrong kid.*  
>  
> *Furthermore, Material 2 shows a massive Say/Do gap: 58% of parents asked for an editor, but fewer than 1% ever finish an edit. We do NOT build the editor, and we do NOT build livestreaming next. We fix roster tagging first, because if reels show the wrong kids, Ridgeline will churn regardless."*

### [1:15 - 2:30] Task 2: The Spec (Human-in-the-Loop Confidence Flow)
> *"For our top roadmap item, the spec introduces a Human-in-the-Loop Confidence Verification system.*  
>  
> *The AI autonomously tags and publishes all high-confidence detections above 75%. But when jersey creases, motion blur, or single/double digit ambiguity occurs—such as #14 versus #4—the system isolates the clip and prompts the coach.*  
>  
> *Our goal is to reduce unopened reels from 30% to under 10%. We keep the coach in the loop for under 30 seconds by presenting pre-matched candidate cards with field positions and stats.*  
>  
> *If the coach doesn't review by 6:00 PM, our fail-safe rule kicks in: unverified clips are excluded from personal reels and kept in full match replay, ensuring no parent ever receives a thumbnail with the wrong kid."*

### [2:30 - 4:15] Task 3: Interactive Prototype Walkthrough
> *(Screen Share: index.html running)*  
> *"Here is the working prototype of our 3 core screens:*  
>  
> *1. Screen 1: Coach Dashboard. Coach Dave opens the app after Saturday's match. 21 highlights are auto-verified. But right at the top is an amber action banner: '3 clips need review — jersey number unclear before auto-recap sends tonight at 6:30 PM.'*  
>  
> *2. Screen 2: Review Flow. Tapping the banner takes Coach Dave into the review queue. Here we see Clip 1: computer vision detected jersey '#4?' with 62% confidence due to a jersey fold. The system displays candidate A (#14 Mia Thompson, Forward) and candidate B (#4 Leo Vance, Defender). With a single tap on 'Confirm Mia Thompson (#14)', the tag is verified.*  
>  
> *3. Screen 3: Confirmation & Recap. The reel updates instantly. The hero thumbnail for Mia is locked in with the club watermark, and the weekly team recap is queued for 6:30 PM dinner delivery—guaranteeing high open rates and zero disappointed parents."*

### [4:15 - 5:30] Task 4 & Personal Close
> *"In Task 4, I used AI for rapid prototyping and synthetic data modeling, but I kept the strategic pushback human. The decision to hold firm against livestreaming and reject the Say/Do trap requires product conviction.*  
>  
> *A quick background on me: My name is Ayush Kabra. I'm a product manager passionate about building high-velocity, high-trust software that solves real user problems. What excites me about Ajaia is the blend of cutting-edge computer vision with everyday human moments—empowering youth sports communities and families.*  
>  
> *Regarding salary expectations, based on the market benchmark for this Product Manager role, my expectation is [Insert your range, e.g. $130,000 - $150,000 USD / or your target local equivalent]. Thank you for your time, and I look forward to the next steps!"*
