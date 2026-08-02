# Build Well Video Workspace — Guide

HTML-native video workspace built on [Hyperframes](https://hyperframes.heygen.com), adapted from Nate Herk's Hyperframes Editor kit. Not a Remotion project — this is the other pipeline.

**This workspace hosts multiple video projects, one folder each, all under `video-projects/`.** The workspace root holds shared tooling (`node_modules/`, `package.json`, `.claude/`, this `CLAUDE.md`, `DESIGN.buildwell.md`, `MOTION_PHILOSOPHY.md`) — never put `index.html`, `assets/`, `compositions/`, or `renders/` directly at the root. Always work from inside a project subfolder.

## About Build Well (READ FIRST — this is the brand)

Build Well ([buildwellcollective.com](https://www.buildwellcollective.com/)) is a media platform and professional community: **"Build Well: Women Shaping Health Technology."** Podcast, newsletter, and social content at the intersection of product management, AI, and healthcare, hosted by Kelly Scherer, Alex Tong, and Kristi Lui.

- **Audience:** mid-career women in digital health product roles (PMs, designers, clinical/ops leads), plus founders and engineers entering healthcare.
- **Brand tone:** intelligent, editorial, human, credible. NOT hype-driven, NOT generic tech-bro podcast aesthetics, NOT clinical/corporate.
- **Content types produced here:**
  1. **Episode clips** — 9:16 vertical (1080×1920) guest-quote and insight clips from podcast episodes, with lower-thirds and captions. Primary output.
  2. **Episode trailers / teasers** — 16:9 and 9:16.
  3. **Audiograms / quote cards** — 1:1 (1080×1080) and 4:5 (1080×1350) for LinkedIn (primary social channel).
  4. **Brand films / promos** — community, Office Hours, newsletter CTAs.
- **Distribution:** LinkedIn first, then Instagram/TikTok clips, YouTube for full episodes.
- **CTAs rotate between:** Listen to the episode, Join the Community, Subscribe to the newsletter.

**`DESIGN.buildwell.md` (workspace root) is the visual source of truth** — palette (deep sage green `#366560` + blush `#edb8b6` + ivory), typography (Fraunces + Montserrat), motion rules, caption style, lower-third spec, and the What-NOT-to-Do list. Read it before any composition work. Brand assets live in root `assets/` (`buildwell_logo_transparentbackground.svg` is the primary wordmark; `brand-tokens.css` has the `--bw-*` vars).

## MOTION_PHILOSOPHY.md — discipline yes, aesthetic no

`MOTION_PHILOSOPHY.md` (workspace root) is the deconstructed playbook of the Infinite Payments spot — it came with this kit. **For Build Well, apply its discipline, not its look:**

- **Keep:** one idea per beat, motion lives in transitions, breathing outros (hold 4–6s), callbacks, the pre-flight checklist habit, scene-level pacing rigor.
- **Ignore/override:** black canvas, perspective grids, crosshairs, chrome-gradient text, halo glows, whip transitions, ~1.5s scene lengths. Build Well scenes run calmer and longer (see `DESIGN.buildwell.md` motion rules — 0.6–0.9s entrances, crossfade-led transitions, no zoom/glitch).

**On any conflict between `MOTION_PHILOSOPHY.md` and `DESIGN.buildwell.md`, the Build Well spec wins.**

## Skills — USE THESE FIRST

**Always invoke the matching skill before writing or modifying compositions.** Skills encode framework-specific patterns (`window.__timelines` registration, `data-*` attribute semantics, shader-compatible CSS, relative-timing syntax) that are NOT in generic web docs. Skipping them produces broken compositions.

| Skill                    | Command                    | When to use                                                                               |
| ------------------------ | -------------------------- | ----------------------------------------------------------------------------------------- |
| `hyperframes`            | `/hyperframes`             | Authoring/editing compositions, captions, TTS, audio-reactive animation, transitions      |
| `hyperframes-cli`        | `/hyperframes-cli`         | CLI commands: `init`, `add`, `lint`, `preview`, `render`, `transcribe`, `tts`, `doctor`   |
| `gsap`                   | `/gsap`                    | GSAP animation — timelines, easing, stagger, plugins, performance                         |
| `hyperframes-registry`   | `/hyperframes-registry`    | Installing catalog blocks/components via `npx hyperframes add <name>`                     |
| `short-form-video`       | `/short-form-video`        | 9:16 talking-head + motion-graphics clips (adapt caption style to Build Well spec)        |

Not present? `npx skills add heygen-com/hyperframes --yes` then reopen this directory.

## Commands

```bash
# Authoring loop
npx hyperframes preview                          # Studio opens in browser with hot reload (port 3002)
npx hyperframes lint                             # static HTML check — always run before rendering
npx hyperframes compositions                     # list comp IDs + resolved durations
npx hyperframes render --quality draft --output renders/draft.mp4    # fast iteration render
npx hyperframes render --quality standard --output renders/final.mp4 # visually lossless 1080p

# Catalog & install
npx hyperframes catalog --type block             # browse blocks
npx hyperframes add <name>                       # install a catalog item into compositions/

# Media pipeline (baked into CLI — no Whisper CLI needed)
npx hyperframes transcribe <file> --model small.en --json          # word-level timestamps
npx hyperframes tts "text" --voice af_bella --output narration.wav # on-device TTS (rarely used — Build Well is real-voice first)

# Diagnostics
npx hyperframes doctor                           # env check (Node, FFmpeg, Chrome, Docker)
npx hyperframes docs <topic>                     # inline docs: data-attributes, gsap, rendering, examples, troubleshooting, compositions
```

### Render flags worth knowing

- `--quality draft|standard|high` — CRF 28 / 18 / 15 (standard is visually lossless at 1080p)
- `--fps 24|30|60` (default 30 — Build Well default is 30)
- `--format mp4|mov|webm` — `mov` = ProRes 4444 with alpha, `webm` = VP9 alpha (Chromium only)
- `--workers <n>` / `--gpu` / `--docker` / `--crf <n>`

## Build Well output specs

| Deliverable | Dimensions | FPS | Notes |
|---|---|---|---|
| Episode clip (Reels/TikTok/Shorts) | 1080×1920 (9:16) | 30 | Captions mandatory; lower-third on first appearance of speaker; end card with logo + CTA, hold 4–6s |
| LinkedIn clip / audiogram | 1080×1350 (4:5) | 30 | Assume sound-off viewing — captions carry the content |
| Quote card (animated) | 1080×1080 (1:1) | 30 | Fraunces pull quote + blush underline + attribution |
| Trailer / YouTube | 1920×1080 (16:9) | 30 | |

Safe margins on 9:16: keep text inside the center ~1080×1420 — platform UI eats the top ~250px and bottom ~250px.

## Workspace Layout

```
build-well-video/
├── CLAUDE.md, AGENTS.md, DESIGN.buildwell.md   ← workspace docs (brand spec = DESIGN.buildwell.md)
├── MOTION_PHILOSOPHY.md                         ← pacing discipline reference (aesthetic overridden by DESIGN.buildwell.md)
├── package.json, node_modules/                  ← workspace tooling
├── .claude/                                     ← skills + plugin config
├── assets/                                      ← shared brand assets (Build Well logos, brand-tokens.css, music)
└── video-projects/                              ← one folder per video
    ├── episode-clip-template/
    ├── may-shorts-19/                           ← reference template (AIS-era, structure only)
    └── ...
```

Each project under `video-projects/<name>/` is a self-contained Hyperframes project:

- `index.html` — root composition entry point
- `compositions/` — sub-compositions loaded via `data-composition-src`
- `assets/` — media files for this project. Brand assets are duplicated per-project, not symlinked — keeps each project portable. Copy from root: `cp ../../assets/brand-tokens.css ../../assets/buildwell_logo_transparentbackground.svg assets/`
- `renders/` — render outputs (gitignored)
- `hyperframes.json` — CLI config (paths relative to the project folder)
- `meta.json` — project metadata (id, name, dimensions, fps)

### Always run the CLI from inside the project folder

```bash
cd video-projects/<project>
npx hyperframes lint
npx hyperframes preview
npx hyperframes render --quality standard --output renders/final.mp4
```

The CLI reads `hyperframes.json`/`meta.json` from the current directory. Running it from the workspace root will fail or scan the wrong files.

### Adding a new video project

1. `mkdir video-projects/<slug>` (kebab-case, e.g. `ep07-maddie-clips`)
2. `cd video-projects/<slug>` then `npx hyperframes init`, or copy `hyperframes.json` + `meta.json` from a sibling and edit `meta.json`
3. Copy brand assets in from root `assets/`
4. Build the composition; lint + preview + render from inside this folder

Naming convention for episode work: `ep<NN>-<guest-or-topic>-<type>`, e.g. `ep07-maddie-clips`, `ep08-solo-trailer`.

## Render Contract (the must-dos and must-not-dos)

1. Root `<div>` needs `id`, `data-composition-id`, `data-start="0"`, `data-width`, `data-height`.
2. Timed visible elements need `class="clip"` — **except** `<video>` and `<audio>` (adding `class="clip"` to `<video>` breaks it).
3. Every timed element needs `data-start`, `data-duration`, `data-track-index`.
4. `data-start` can reference another clip's id: `data-start="intro"`, `data-start="intro + 2"`. Same-track clips cannot overlap — use different `data-track-index` values.
5. `<video>` must be `muted`; audio belongs in sibling `<audio>` elements for the mixer. `data-has-audio="true"` only when the video's own audio should feed the mix.
6. Every composition registers exactly one GSAP timeline, paused, on `window.__timelines["<data-composition-id>"]`. Key must match `data-composition-id` exactly.
7. Composition duration = `tl.duration()`. Pad with `tl.set({}, {}, <seconds>)` to extend.
8. Never call `.play()`, `.pause()`, or set `.currentTime` on media. The framework owns playback.
9. Never animate `width`/`height`/`top`/`left` directly on a `<video>` — wrap in a `<div>` and animate the wrapper.
10. Sub-compositions use `<template>` + `data-composition-src`. Their timelines auto-link to the parent — never do `masterTL.add(child)`.
11. Determinism: no `Date.now()`, no unseeded `Math.random()`, no render-time network fetches. Use seeded PRNGs.

## Authoring Loop

1. **Read `DESIGN.buildwell.md`** if you haven't this session — it sets palette, type, captions, and motion.
2. Pick the skill → invoke `/hyperframes` (or sibling) before editing.
3. Edit HTML in `index.html` or `compositions/<name>.html`.
4. `npx hyperframes lint` — fix errors, triage warnings.
5. **Localhost Studio preview** — before **any** render, start `npx hyperframes preview` in the background and hand Kelly the URL. She eyeballs the edit live and iterates; no render cycle until she's seen it.
6. Only after Kelly signs off on the live preview: `render --quality draft`.
7. **Visual verification** (REQUIRED) — see below.
8. Second preview pass on the draft MP4 (serve `renders/` via `npx serve . -p 8080 -n` — NOT Python's http.server, which breaks scrubbing) — wait for explicit sign-off before the final render.
9. Final: `render --quality standard`; report the output path.

Silence is not approval — wait for an explicit "looks good / render it / ship it."

## Visual Verification (MANDATORY before delivery)

Lint passing ≠ design working. Never report a render as done without actually looking at frames.

1. Render a draft: `npx hyperframes render --quality draft --output renders/<name>-draft.mp4`
2. Pull one frame per scene at its hero moment plus any risky transition, covering the full timeline:
   ```bash
   mkdir -p renders/frames
   for t in <scene1-t> <scene2-t> ...; do
     ffmpeg -y -ss $t -i renders/<name>-draft.mp4 -frames:v 1 -q:v 2 "renders/frames/t${t}.png"
   done
   ```
3. Call `Read` on every PNG so the image actually loads into context. Verify:
   - Speaker's face is not cropped; framing correct for each scene
   - Scene transitions land on the intended word
   - Captions are on-brand (Montserrat Medium, sentence case, ivory on the green caption pill — see `DESIGN.buildwell.md` §What NOT to Do #4) and inside safe margins
   - Lower-thirds match the spec (Fraunces name / Montserrat title / blush underline)
   - Colors trace to `--bw-*` tokens — flag any stray AIS-era cyan `#37bdf8` or orange `#f09025` as a bug
   - No text overflow, no unintentional overlap, no blank frames
4. If anything is wrong — fix, re-render, re-verify. Only then run the `standard` render.

## Asset Prep

Re-encode raw recordings to H.264 MP4 before referencing as `<video src>`:

```bash
ffmpeg -i raw.mov -c:v libx264 -preset medium -crf 20 -c:a aac -b:a 192k -movflags +faststart assets/clip.mp4
```

Podcast audio loudness target: **-16 LUFS** for clips (`ffmpeg -i in.wav -af loudnorm=I=-16:TP=-1.5:LRA=11 out.wav`). Use `npx hyperframes doctor` if a render fails partway.

## Prompting Shorthand (what the `/hyperframes` skill understands)

- **Motion easing:** default to smooth / dreamy for Build Well. Avoid bouncy/springy.
- **Caption energy:** storytelling or tutorial. Never hype.
- **Transition energy:** calm (blur/crossfade) or medium (push). Never high (zoom, glitch).
- **Audio reactivity:** use sparingly — subtle background amplitude only (≤10%); no text reactivity on brand content.

## Registry (available via `npx hyperframes add <name>`)

Useful for Build Well: `logo-outro`, `yt-lower-third` (restyle to spec), `spotify-card`, `data-chart`, `transitions-blur`, `transitions-push`, `grain-overlay` (very subtle, if at all).
Avoid: `glitch`, `whip-pan`, `flash-through-white`, `cinematic-zoom`, and other high-energy shader transitions — off-brand.
Browse: `npx hyperframes catalog --type block --json`

## Documentation — fetch when the skills don't cover enough

- **Agent index:** https://hyperframes.heygen.com/llms.txt — complete sitemap
- **Catalog blocks:** `https://hyperframes.heygen.com/catalog/blocks/<slug>` — full props + examples
- **Reference:** `https://hyperframes.heygen.com/reference/html-schema` — authoritative data-attribute + timeline spec
- **Inline docs:** `npx hyperframes docs <topic>` — `data-attributes`, `gsap`, `rendering`, `examples`, `troubleshooting`, `compositions`
- **Source repo:** https://github.com/heygen-com/hyperframes

Don't guess at a block's props — fetch the page.
