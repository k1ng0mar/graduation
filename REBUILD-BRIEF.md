# Sev's Site — Rebuild Brief (feed this to Nyx)

> **How to use this:** Paste this whole file to Nyx as the spec. Prepend one line:
> *"Build this exactly. This is a spec, not a starting point — every DO and DON'T is deliberate. Do not add features, sections, or copy that aren't named here. When unsure, do less."*
> Weaker models drift into slop when given freedom, so this brief deliberately removes freedom. Follow it literally.

---

## 0. Why the last build was slop (so you don't repeat it)

The previous version (`index.html`, now archived) failed in specific ways. **Each of these is now a hard rule below.** It:

1. Treated her quiz answers as a **checklist of symbols to literally depict** — plant a rose, pet a jaguar, match Monaco cards, catch autumn leaves. Literal = childish.
2. Was **six near-identical full-screen colored slides** with a "Continue" button between each — a slideshow, not an experience.
3. **Fractured the palette** — dawn purple, then pink, then dark maroon, then **teal/blue Monaco** (totally off-brief), then orange. Six unrelated color bands.
4. **Captioned every symbol with a paragraph** explaining its meaning ("A jaguar doesn't announce itself… Feisty doesn't mean loud. It means unstoppable."). Telling, not showing. Greeting-card prose.
5. Used **fortune-cookie quotes** with zero specificity ("You were made for blooming"). Could be for anyone.
6. Used **wedding-template fonts** (Dancing Script cursive + Playfair Display) and **bouncy/spin-in motion** (`cubic-bezier(…,1.56,…)`, `rotate(-180deg) scale(0)`).
7. **Lumpy hand-drawn SVGs** — the "jaguar" is a blob with dots; "Monaco" is a zigzag bar.
8. Signed off **"With love, your friend"** — a placeholder where the actual personal message should be. This is the single biggest miss.

---

## 1. The concept — ONE scene, not six

**Title: "Don't Stop 'Til Dawn."** (Her comfort song is *Don't Stop 'Til You Get Enough* — the whole site is one long sunrise she coaxes up. The song is the structure, never stated.)

There is **one continuous space**: a pre-dawn sky over a low horizon. Nothing ever "changes rooms." The entire experience is **one sky slowly warming from night to full sunrise**, driven by a single variable `--dawn` (0 → 1).

Everything is a function of `--dawn`:
- Sky gradient stops interpolate night → rose → peach → gold.
- The sun rises from below the horizon as `--dawn` increases.
- Stars fade out (`opacity: calc(1 - var(--dawn))`).
- Roses along the horizon bloom open.
- The warmth/saturation of the whole page lifts.

**Delayed gratification is built into the medium, not bolted on with counters:** the sun will not rise on its own. She has to *coax it* through a few slow, gentle interactions. Each one nudges `--dawn` up by a step, with a **long, slow tween (2.5–4s)** and a held pause before the next prompt appears. The payoff is earned light, and it lands once.

### The motifs become *atmosphere*, never stations:
| Motif | How it appears (subtle, woven in) | Never do this |
|---|---|---|
| Sunrise | The entire medium | — |
| Roses | A row of roses on the horizon that bloom as dawn rises (parametric curve, slow stroke-draw) | A "plant 3 roses" minigame with a counter |
| Jaguar + "feisty" | A faint **constellation** in the night sky shaped like a jaguar; only catches the eye if she lingers. A hidden spark. | A blobby jaguar SVG you "pet" |
| Autumn | The *color temperature* of the light — ambers, rust, warm gold in the dawn ramp | A separate orange "catch the leaves" screen |
| Monaco | At full sunrise, a faint **harbor silhouette** resolves on the horizon line in the warm haze | Cartier/casino-chip flashcards |
| MJ song | An optional, **soft** disco bassline that fades in *only* at full dawn, low volume | Auto-playing anything; a loud "Play Celebration" button mid-scene |
| Both sweet+savory / Monaco / "expensive taste" | Restraint and craft *is* the luxury. Quiet, not literal. | Listing luxury items |

---

## 2. Interactions (gentle, no scores, no counters)

Three steps total. No "0 of 3" text anywhere. Progress is shown **only** by how much the sky has warmed.

1. **Hold to let the light in.** A soft prompt: *"hold."* While she presses-and-holds (mouse/touch), `--dawn` rises smoothly; release and it eases to a hold-point. This makes patience tactile — it *is* delayed gratification. First press also unlocks audio context (so the groove can play later).
2. **Wake the roses.** As light grows, prompt: *"again."* A gentle tap/hold makes the horizon roses bloom open one by one (slow stroke-draw, staggered). When the last opens, the sky jumps toward full warmth.
3. **The sun crests.** Final hold: the sun clears the horizon, stars finish fading, the Monaco harbor silhouette resolves, the bassline fades in low, and **the message blooms** (see §6). This plays **once** and does not re-trigger.

Each step: **held 600ms pause → slow transition → next prompt blur-fades in.** Never show all prompts at once. One word at a time ("hold." → "again." → nothing, just the dawn).

---

## 3. Palette — ONE sunrise ramp (no other colors exist)

Paste this. Every color on the page comes from here. **No teal, no blue, no green except the rose stems. Nothing outside this ramp.**

```css
:root{
  /* night → dawn ramp, dark to light */
  --c-night:   #241024;  /* plum-black */
  --c-dusk:    #3d1a3a;  /* deep mulberry */
  --c-mulberry:#5e2347;
  --c-rose-dp: #9b2d4e;  /* deep rose — the ONE accent for the most important word */
  --c-rose:    #b5546e;
  --c-coral:   #e08a7d;  /* coral-rose */
  --c-peach:   #f2b48a;
  --c-gold:    #f7d49b;  /* warm autumn gold */
  --c-cream:   #fdf2ec;  /* lightest */
  --ink:       #3a1c2a;  /* text on light */
  --warm-white:#fff6f0;  /* text on dark */
  --stem:      #6e7d54;  /* muted olive, the ONLY non-warm color, tiny use */
}
@property --dawn { syntax:'<number>'; inherits:true; initial-value:0; }
```

Use `--dawn` to interpolate. Example sky (layer 2–3 `radial-gradient`s for a soft mesh, not one flat `linear-gradient`):
```css
body{
  background:
    radial-gradient(120% 80% at 50% 110%, var(--c-gold), transparent 60%),
    radial-gradient(100% 70% at 50% 100%, var(--c-coral), transparent 55%),
    linear-gradient(180deg, var(--c-night), var(--c-dusk) 40%, var(--c-mulberry) 75%, var(--c-rose));
  /* fade the warm layers up via --dawn on the radial layers' opacity using mask or a warming overlay */
}
```
The cleanest way: keep a fixed night gradient, and **one warm overlay div** whose `opacity: var(--dawn)` carries the sunrise. Animate `--dawn`, not 30 separate properties.

---

## 4. Typography — drop the wedding fonts

```html
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,300..600;1,9..144,300..500&family=Inter:wght@300;400;500&display=swap" rel="stylesheet">
```
- **Display / her name / the few words on screen:** `Fraunces` (a soft, optical serif with real character — feminine but not cutesy). Use light weights (300–400), large optical size, generous line-height. Her name "Sev" in **Fraunces italic**, large — classier than any cursive.
- **Body / the message:** `Inter` 300–400, comfortable measure (~38ch), line-height 1.7.
- **BANNED:** Dancing Script, any cursive/script, Playfair Display, Great Vibes, Pacifico. They read as template-elegant.
- Letter-spacing: tiny positive tracking on small uppercase labels only (`0.18em`). Never on headlines.

---

## 5. Motion — elegant means slow and decelerating

- **Easing:** reveals use `cubic-bezier(0.22, 1, 0.36, 1)` (expo-out). General `cubic-bezier(0.4, 0, 0.2, 1)`.
  **BANNED:** any back/overshoot/elastic (`cubic-bezier(…, 1.56, …)`, `back.out`, `elastic`), and spin-in (`rotate(-180deg) scale(0)`).
- **Durations:** dawn warming between steps **2.5–4s**; text reveals **1.2–1.6s**; micro-interactions **0.3–0.4s**. Never the same duration on everything.
- **The one premium move — blur-in text:** reveal text from `opacity:0; filter:blur(14px); transform:translateY(18px)` → settled, `1.4s`, stagger `0.08s` per line. The blur is what reads as expensive; a plain fade reads as template.
- **Roses bloom** via SVG `stroke-dasharray`/`stroke-dashoffset` draw-on + slow petal scale, staggered. Build the rose shape from a **rhodonea/rose curve** `r = a·cos(kθ)` (k=4 → 8 petals), not stacked ellipses.
- **Particles:** ≤ 36 soft pollen/petal motes, sine-wave horizontal drift, gentle rise, low opacity. Subtle. Not confetti.
- **Page load choreography (sequence, don't dump):** night sky settles → faint stars appear → "Sev" blurs in → the single prompt "hold." fades in. One timeline, explicit offsets.
- `prefers-reduced-motion`: skip particles and auto-motion; let her advance with taps; jump `--dawn` instantly between steps.

---

## 6. Copy — say almost nothing, mean everything

**The whole site has maybe 8 words of UI text plus the final message.** Show, don't caption.

- On-screen words, total: her name (`Sev`), the prompts (`hold.` / `again.`), and the final message. That's it. **No instruction sentences, no atmospheric filler, no metaphor explanations.**
- **BANNED:** any sentence that explains a symbol ("a jaguar doesn't announce itself…"), any fortune-cookie line ("you were made for blooming"), "Enter the Garden," "Continue," "Congratulations, graduate," exclamation-mark hype.

### The final message — ⚠️ DO NOT WRITE THIS. Umar writes it.
This is the soul of the gift and the one thing an AI must not generate. Leave this exact placeholder in the code and **stop**:

```html
<!-- UMAR: replace this entire block with your real words to Sev.
     One specific shared memory beats ten metaphors. Keep it short.
     Do NOT let any model fill this in. -->
<p class="message" id="umar-message">[ YOUR MESSAGE GOES HERE ]</p>
```
Guidance for Umar (not for the AI): one real moment only she'd recognize, in your actual voice, ~3–5 sentences. Sign it as yourself, not "your friend."

---

## 7. Technical spec

- **Single `index.html`**, vanilla JS, no framework. GSAP optional via CDN; vanilla is fine.
- One scene: fixed full-viewport. Layered: `sky` (gradients) → `stars` (incl. jaguar constellation) → `sun` → `horizon` (roses + harbor silhouette) → `particles` → `text`.
- Drive **one** custom property `--dawn` (0→1) via JS `requestAnimationFrame` tweens; let CSS derive everything from it.
- **Reuse from the old file (it's the good part):** the WebAudio `playGroove()` disco bassline — but: start it **muted/low**, fade in only at full dawn, and gate behind her first interaction. **Fix the bug:** in the old `catchLeaf`, `msgIdx` was used before declaration (NaN). The leaf game is gone, but audit for the same "use before declare" pattern.
- **Accessibility:** keyboard-operable (Space/Enter to "hold"); visible `:focus-visible`; `aria-live` for the final message; respects `prefers-reduced-motion`; an unobtrusive "skip" that jumps to full dawn.
- **Mobile-first:** touch press-and-hold must work; test portrait; tap targets ≥ 44px; no horizontal scroll.
- No external assets, no photos (none exist — don't request any). Google Fonts only.
- Deploy: static file → existing GitHub Pages repo (`k1ng0mar/sev-graduation`) or Vercel. Same as before.

---

## 8. Build order (do NOT build all at once)

1. **The light system first.** One scene, `--dawn` 0→1 on a debug slider. Get the sky, sun, and star-fade beautiful before anything else. If this isn't gorgeous on its own, stop and fix it.
2. Horizon roses (rhodonea curve, stroke-draw bloom).
3. The three hold-interactions + slow pacing + blur-in prompts.
4. Jaguar constellation + Monaco harbor silhouette (faint, tasteful).
5. Final dawn: message bloom + soft bassline fade-in. Insert Umar's message placeholder — do not generate it.
6. Reduced-motion + keyboard + mobile pass.

---

## 9. Acceptance checklist (Nyx self-reviews before declaring done)

- [ ] It is **one continuous scene**, never a slideshow of colored panels.
- [ ] **No counters** ("X of N"), no scores, no "Continue" buttons.
- [ ] **Every color** is from the §3 ramp. No teal/blue. Screenshot proves cohesion.
- [ ] **Fraunces + Inter** only. No script/cursive, no Playfair.
- [ ] **No metaphor-captions, no fortune-cookie lines.** On-screen text ≤ ~8 words + the message.
- [ ] Motion is **slow + decelerating**; no bounce/spin-in; durations vary.
- [ ] Roses use a **real rose curve**, not stacked ellipses; jaguar is a **constellation**, not a blob.
- [ ] The sunrise is **earned** (won't complete without her); payoff plays **once**.
- [ ] The personal message is a **placeholder for Umar**, not AI-written.
- [ ] Works on a phone with touch; respects reduced-motion; keyboard-operable.
- [ ] Honest self-grade 1–5 on: cohesion, restraint, motion-quality, specificity-to-Sev, craft-of-SVG. **Any score ≤3 → fix before shipping.**

> North star: when in doubt, **do less and slow it down.** Elegance here is restraint plus one perfect sunrise — not more features.
</content>
</invoke>
