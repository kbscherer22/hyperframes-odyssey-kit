Build Well — Visual Identity
Ground truth extracted from assets/buildwell_logo.png (podcast cover art) and buildwellcollective.com. Every composition in this project MUST trace its palette, typography, and motion choices back to this file.
Style Prompt
Build Well is an intelligent, editorial, human brand — "a beautifully art-directed magazine feature, in motion." Compositions should feel like turning the pages of a considered publication: deep sage-green canvases, warm blush accents, generous whitespace, serif headlines that breathe, and calm, confident motion. Not corporate. Not hype-driven. Not clinical. The mood is warmth, credibility, and quiet authority — women who build serious healthcare products and talk about it honestly.
Colors
Token
Hex
Role
--bw-green
#366560
Primary background (deep sage green — from logo)
--bw-green-deep
#294f4b
Cards, panels, shadows on green scenes
--bw-green-soft
#51716d
Borders, dividers, hairlines on green
--bw-blush
#edb8b6
Primary accent — highlights, underlines, CTAs (from logo)
--bw-blush-deep
#d99a97
Accent variant — pressed states, small text where contrast matters
--bw-ivory
#f7f1ea
Light background (editorial scenes) + primary text on green
--bw-ink
#22302e
Primary text on ivory (green-tinted near-black)
--bw-text-dim
#b9cdc9
Secondary/meta text on green
--bw-ink-dim
#5f6f6c
Secondary/meta text on ivory


Two-canvas system: green scenes (brand moments, openers, quote cards, end cards) and ivory scenes (editorial content, lists, frameworks). Alternate them; never mix a third background color.
Typography
Fraunces (SemiBold 600 / Light 300) — warm editorial serif. Use for: headlines, pull quotes, guest names, big numbers. SemiBold for impact, Light for large elegant statements.
Montserrat (Medium 500 / SemiBold 600) — geometric sans, echoes the "WELL" and tagline in the logo. Use for: labels, kickers, captions, lower-thirds, CTAs, meta text. Uppercase with letter-spacing: 0.12em for kickers and labels (matches the "WOMEN SHAPING HEALTH TECHNOLOGY" treatment).

Pair them — never use only one. Montserrat uppercase kicker above a Fraunces headline is the house pattern.

The script "Build" lettering lives in the logo only. Never typeset it as live text; never substitute a lookalike script font in compositions.
Logo
Primary file: assets/buildwell_logo_transparentbackground.svg — blush script "Build" + bold "WELL" wordmark with underline flourish and tagline, transparent background. Use this in compositions (vector, scales to any render size).
Raster fallback: assets/buildwell_logo_transparentbackground_large.png (1563px, true alpha).
Cover-art version: assets/buildwell_logo.svg — same wordmark on --bw-green; for end cards and podcast-platform contexts.
Clearspace: half a logo-height of margin on all sides.
Never recolor. Never stretch. No glows, shadows, or effects — the brand is matte, not luminous.
Motion Rules
Entrance only (per Hyperframes skill rule): every element animates in via gsap.from(). Transitions between scenes handle exits.
Easing palette: power2.out, sine.out, power3.out for entrances; sine.inOut for ambient drifts; power2.in for hand-offs into transitions. No back.out or elastic — bounce reads as playful, not editorial.
Use at least 2 different eases per scene, but keep the family calm.
Duration bands: text entrances 0.6–0.9s, accent elements (underlines, rules) 0.5–0.7s, ambient drifts 3–6s. Slower than social-media default — confidence, not urgency.
Offset first animation 0.2–0.4s from scene start. Let scenes breathe.
Text stagger: 0.10–0.16s per word for headlines (word-level, not per-character — per-character reads as techy).
Signature move: blush underline strokes draw in left-to-right under key phrases (scaleX from 0, transform-origin: left), echoing the logo's underline flourish.
Numbers: count-up with {innerText: N, snap: {innerText: 1}} + font-variant-numeric: tabular-nums, in Fraunces.
Transitions
All CSS (not shader) so scenes stay simple.

Scene change
Transition
Duration
Ease
Opener → content
Blur crossfade
0.6s
sine.inOut
Content → content
Soft push slide left
0.5s
power2.inOut
Green ↔ ivory scene
Straight crossfade
0.6s
sine.inOut
Final → end card
Blur crossfade
0.7s
sine.inOut


Primary = crossfades (70%). Push slides only between same-canvas content scenes. No zoom-through, no whip pans, no glitches.
Buttons / CTAs
Rounded pill, solid --bw-blush fill, --bw-green-deep text, Montserrat SemiBold uppercase, letter-spacing: 0.1em, 15–17px, 14–16px vertical + 30–38px horizontal padding.

Example: [ JOIN THE COMMUNITY → ]

Secondary style: transparent fill, 1.5px --bw-blush border, --bw-ivory text.
Lower-Thirds (podcast clips)
Guest name: Fraunces SemiBold, --bw-ivory
Title • Company: Montserrat Medium uppercase, --bw-text-dim, 0.1em tracking
Blush underline rule (2–3px) between name and title, drawn in on entrance
Anchor bottom-left with generous margin; never boxed in a filled container
Iconography
Thin stroke, 1.5–2px weight, --bw-blush on green / --bw-green on ivory, no fills. Simple line motifs: underline flourishes, asterisks, arrows (→), serif-style quotation marks for pull quotes. No emoji in rendered video.
What NOT to Do
No full-screen linear gradients — H.264 banding. Use solid --bw-green + a very subtle localized radial lift behind focal elements if needed.
No neon, no cyan/electric blue, no saturated tech palettes. The palette is green + blush + ivory + ink. That's it.
No terminal/command-center aesthetics — no monospace tickers, no glitch effects, no HUD frames. Build Well is editorial, not a control room.
No hype-style karaoke captions (per-word color pops, emoji, screen shake). Captions are Montserrat Medium, sentence case, --bw-ivory on a soft rgba(41,79,75,0.85) pill.
No fonts outside Fraunces + Montserrat. No Arial, Helvetica, Inter, or system fonts. The logo script is an image, never a font.
No pure black (#000) or pure white (#fff). Use --bw-ink and --bw-ivory.
Contrast guardrails: --bw-blush on --bw-green is for large text (24px+) and graphic accents only; body-size text on green must be --bw-ivory or --bw-text-dim.
No transparent keyword in gradients — shader-compatible CSS rule. Use rgba(54,101,96,0).
No Math.random() or Date.now() — render determinism. Use seeded PRNG if needed.
No exit animations on any scene except the final one — transitions handle exits.
No stretching or recoloring the logo. Keep aspect ratio. Respect clearspace.
File References
assets/buildwell_logo_transparentbackground.svg — primary wordmark (transparent, vector)
assets/buildwell_logo_transparentbackground_large.png — raster fallback (1563px, alpha)
assets/buildwell_logo.svg — cover-art version on brand green
assets/brand-tokens.css — the CSS :root vars imported by every composition
Fonts via Google Fonts: https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,300;9..144,600&family=Montserrat:wght@500;600&display=swap

