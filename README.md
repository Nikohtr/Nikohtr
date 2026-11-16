<picture>
  <source media="(prefers-color-scheme: dark)" srcset="assets/banner-dark.svg">
  <img src="assets/banner-light.svg" width="100%" alt="Niko Trouhtchev. Building an AI receptionist that answers in Bulgarian. 3,400+ tests behind one phone number. Snapping Mac windows with two fingers. Teaching a blank YOLOv8 to see, live. WireGuard in the menu bar, in ~2,900 lines of Rust. Shipping credit lines for SMEs at Monexo.">
</picture>

Full-stack engineer building AI products for the Bulgarian market. MSc in Artificial
Intelligence at Bocconi (2026–28); BSc Economics, Management and Computer Science, Bocconi.
Milan / Sofia.

<p>
  <a href="https://github.com/Nikohtr/sweep/releases/latest"><img src="https://img.shields.io/github/v/release/Nikohtr/sweep?label=Sweep&color=5E8576" alt="Sweep latest release"></a>
  <a href="https://github.com/Nikohtr/obadise-voice-agent"><img src="https://img.shields.io/badge/Obadi.se%20tests-3%2C400%2B-2da44e" alt="Obadi.se: 3,400+ tests"></a>
  <a href="https://github.com/Nikohtr/sweep"><img src="https://img.shields.io/badge/Sweep%20tests-480%2B-2da44e" alt="Sweep: 480+ tests"></a>
  <a href="https://github.com/Nikohtr/yolo-distillation"><img src="https://img.shields.io/badge/YOLOv8%20student-94.8%25%20of%20teacher%20boxes-d97706" alt="YOLOv8 student reproduces 94.8% of teacher boxes"></a>
  <a href="https://github.com/Nikohtr/wgbar"><img src="https://img.shields.io/github/stars/Nikohtr/wgbar?label=wgbar&logo=rust&color=CE422B" alt="wgbar stars"></a>
</p>

## Now

<details open>
<summary><b><a href="https://github.com/Nikohtr/obadise-voice-agent">Obadi.se</a></b> — founder · an AI phone receptionist that speaks Bulgarian</summary>

<br>

Answers a real Bulgarian phone number on a self-hosted stack, holds the conversation in
Bulgarian and files a structured lead. First deployment: after-hours lead capture for an SME
lender. Next: dental and medical clinics. A clock-free turn engine where **code owns the record
and the LLM owns the plan**.

```mermaid
flowchart LR
  C[Caller<br/>PSTN] -->|SIP| S[livekit-sip]
  S --> K[livekit-server<br/>SFU]
  K --> W
  subgraph W[Agent worker · Python · one host, EU]
    direction LR
    D[RNNoise<br/>denoise] --> V[Silero VAD] --> T[Soniox<br/>streaming STT]
    T --> L[Turn core<br/>clock-free state machine]
    L -->|forced tool call| M[LLM<br/>Anthropic wire]
    M --> L
    L --> P[Playout<br/>driver-owned] --> X[Soniox TTS]
  end
  X --> K --> S --> C
  L --> DB[(Postgres<br/>per-turn records)]
  L --> R[stereo .ogg<br/>caller L · agent R]
```

| ~0.65 s | 5.4 % | 75 / 525 | 2.8× |
|:--|:--|:--|:--|
| one-way line delay, measured with a click tone | truncation at the 0.8 s floor (242 live turns) | calls / turns per synthetic-caller campaign | more Anthropic tokens for the same Cyrillic text |

Registered acceptance gates, synthetic-caller campaigns, 3,400+ tests.
*[Architecture write-up](https://github.com/Nikohtr/obadise-voice-agent); the code is private.*

</details>

<details>
<summary><b><a href="https://monexo.bg">Monexo</a></b> — full-stack engineer at a Bulgarian fintech (fast SME credit lines)</summary>

<br>

SvelteKit / Svelte 5, Drizzle, PostgreSQL: payment allocation, balance-chain integrity, document
generation, admin tooling. Also run its Meta and Google Ads.

</details>

## Open source

<table>
<tr>
<td width="50%" valign="top">

<a href="https://github.com/Nikohtr/sweep"><img src="assets/sweep-demo.gif" width="100%" alt="Sweep demo: four overlapping windows snap to the left half and the right quarters, and one closes with a pinch"></a>

<img src="assets/sweep-icon.png" width="20" height="20" alt=""> **[Sweep](https://github.com/Nikohtr/sweep)** · Swift · GPL-3.0 · free<br>
Tidy your Mac with two fingers. Swipe, pinch or tap on a titlebar to snap, move, minimize
and close windows.<br>
<sub>macOS 14+ · universal · 480+ tests</sub>

<details>
<summary>How it works</summary>

Also works on Dock icons, the menu bar, tabs and Mission Control. A pure-logic core (gesture
state machine, snap geometry) with 480+ tests driven by synthetic touch frames;
Accessibility-API window control; signed in-app updates.

</details>
</td>
<td width="50%" valign="top">

<a href="https://github.com/Nikohtr/yolo-distillation"><img src="assets/yolo-distillation.gif" width="100%" alt="Teacher and student side by side: at step 0 the student detects nothing; its boxes converge on the teacher's as online distillation runs"></a>

**[yolo-distillation](https://github.com/Nikohtr/yolo-distillation)** · Python · PyTorch · AGPL-3.0<br>
Watch a blank YOLOv8 learn from a trained one, live, side by side.<br>
<sub>94.8 % of teacher boxes in 30 min · 5.65 steps/s at 320 px on Apple silicon</sub>

<details>
<summary>How it works</summary>

Response-based distillation on the decoded pre-NMS head (soft-target BCE + confidence-masked
L1), with a replay buffer, webcam/slideshow sources and time-lapse recording, plus a patch that
exposes full per-box class probabilities through Ultralytics `Results`. Honest result: the
student memorises the photos it trains on; on held-out photos it stays at 0 %.

</details>
</td>
</tr>
<tr>
<td width="50%" valign="top">

<a href="https://github.com/Nikohtr/axiom-review"><img src="assets/axiom-review.jpg" width="100%" alt="Axiom Review landing page: paste a URL to get a UX review"></a>

<img src="assets/axiom-icon.png" width="20" height="20" alt=""> **[axiom-review](https://github.com/Nikohtr/axiom-review)** · TypeScript · Next.js 16 · MIT<br>
Paste a URL, get a grounded UX and accessibility review.<br>
<sub>every finding pinned to a CSS selector and a screenshot of that element</sub>

<details>
<summary>How it works</summary>

Playwright loads the page at desktop and mobile size and audits the live DOM. Claude must cite
a CSS selector for every finding; each selector is re-screenshotted in the open browser, and
selectors that do not resolve are dropped.

</details>
</td>
<td width="50%" valign="top">

<a href="https://github.com/Nikohtr/wgbar"><img src="assets/wgbar-menu.png" width="100%" alt="WGBar right-click menu: office connected, tunnel picker, connect on demand, launch at login"></a>

**[wgbar](https://github.com/Nikohtr/wgbar)** · Rust · objc2 · MIT<br>
A tiny macOS menu bar toggle for `wg-quick` WireGuard tunnels.<br>
<sub>~2,900 lines of Rust · macOS 13+</sub>

<details>
<summary>How it works</summary>

Connect-on-demand via an "armed" interface so the first connection never fails, automatic DNS
repair on launch, wake and network change, and a least-privilege root helper.

</details>
</td>
</tr>
</table>

<details>
<summary><b>Before</b> — thesis, InsiderWallets, Postbank</summary>

<br>

- Bachelor's thesis: online learning for call-centre staffing under demand uncertainty —
  UCB1 / LinUCB / bandits-with-knapsacks against Prophet-based forecasts.
- Founded InsiderWallets, a crypto wallet-analytics product (150+ users; wound down).
- Customer Intelligence & AI intern at Postbank Bulgaria (demand forecasting, ~5 % MAPE).

</details>

<p align="center"><sub>Bulgarian · English · Italian</sub></p>
