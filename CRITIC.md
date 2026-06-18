# Sev Site — Critic Framework

I review every phase against this. Any score ≤3 → fix before shipping.

## The brief's anti-slop rules (from REBUILD-BRIEF.md §0)

Hard rules I must NOT violate (each one is a real failure of the previous build):
- [ ] NOT a checklist of symbols literally depicted (no "plant a rose" / "pet a jaguar" / "match cards" / "catch leaves" minigames)
- [ ] NOT six near-identical full-screen colored slides with Continue buttons
- [ ] NOT a fractured palette (dawn purple → pink → dark → teal → orange)
- [ ] NOT captioned symbols with paragraphs explaining their meaning
- [ ] NOT fortune-cookie quotes ("you were made for blooming")
- [ ] NOT wedding-template fonts (Dancing Script, Playfair, Great Vibes, Pacifico)
- [ ] NOT bouncy/spin-in motion (no `cubic-bezier(...,1.56,...)`, no `rotate(-180deg) scale(0)`)
- [ ] NOT lumpy hand-drawn SVGs (jaguar blob with dots, Monaco zigzag bar)
- [ ] NOT "With love, your friend" — placeholder where real message should be
- [ ] Personal message MUST be placeholder for Umar, NOT AI-written

## Brief §9 acceptance checklist

- [ ] One continuous scene, never a slideshow of colored panels
- [ ] No counters ("X of N"), no scores, no Continue buttons
- [ ] Every color from the §3 ramp — NO teal/blue, screenshot proves cohesion
- [ ] Fraunces + Inter only — NO script/cursive, NO Playfair
- [ ] No metaphor-captions, no fortune-cookie lines. On-screen text ≤ ~8 words + the message
- [ ] Motion slow + decelerating. NO bounce/spin-in. Durations vary
- [ ] Roses via real rose curve (rhodonea), NOT stacked ellipses; jaguar is constellation NOT blob
- [ ] Sunrise is earned (won't complete without her). Payoff plays once
- [ ] Personal message is placeholder for Umar, not AI-written
- [ ] Works on phone with touch; respects reduced-motion; keyboard-operable

## Impeccable / taste-skill cross-checks

- [ ] Color contrast: body text ≥4.5:1 against bg, large text ≥3:1
- [ ] No Inter as default sans (BANNED as default) — but brief explicitly names Inter, spec wins
- [ ] No Fraunces as default display (BANNED as default) — but brief explicitly names Fraunces, spec wins
- [ ] No hand-rolled decorative SVGs unless justified; brief's rose curve + constellation + harbor are justified
- [ ] Reveal animations enhance an already-visible default, NOT gate content visibility on class-triggered transition
- [ ] Reduced motion has a real alternative (crossfade or instant), not just "skip the animation"
- [ ] Real easing: `cubic-bezier(0.22, 1, 0.36, 1)` for reveals, `cubic-bezier(0.4, 0, 0.2, 1)` general. NO back/elastic/overshoot.
- [ ] Blur-in text (the premium move): `opacity: 0; filter: blur(14px); transform: translateY(18px)` → settled, 1.4s
- [ ] No emojis
- [ ] Body line length ≤ 65–75ch

## Self-grade per phase (1–5, any ≤3 = fix)

- cohesion: does it look like one designer made it?
- restraint: did I add anything the brief didn't ask for?
- motion-quality: is it slow + decelerating + varying?
- specificity-to-Sev: would she recognize this is for her, or could it be anyone?
- craft-of-SVG: real curves, not blobs?

## Phase review process

For every build phase:
1. **Self-grade** on the 5 axes above (be honest)
2. **Screenshot** the current state (Playwright) and inspect
3. **Checklist** the anti-slop rules above
4. **Apply finalizer polish**: focus-visible outlines, contrast, blur-in text, reduced motion alt
5. **Only ship** when the screenshot matches the brief's vision, not "good enough"
6. **Move on** if 3+ axes score ≤3 — rebuild, don't patch
