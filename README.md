# Festa Fiesta! — 부산 바다축제

A complete 3D festival-management / crowd-simulation game in **one HTML file**.
No build step, no dependencies, no external assets — open `index.html` and play.

> 플레이어는 축제 공간·시설·시간·자원을 설계하고, 자율적으로 움직이는 군중의 반응을
> 관찰한 뒤, 개입을 통해 축제를 개선한다.

---

## Play

Open `index.html` in any WebGL2 browser (Chrome / Edge / Firefox / Safari 15+).

Or serve it locally:

```bash
python -m http.server 5173
```

Then visit `http://localhost:5173`.

---

## What's in it

**Loop** — `Setup → Promotion → [ Morning Check → Live ×4 → Closing → Report ] ×3 → Finale → Final Report`

| System | Detail |
|---|---|
| Renderer | Bespoke WebGL2 — instanced meshes, cascaded-free directional shadow map with PCF, Gerstner-ish water with shore foam, procedural sky with sun/moon/stars/clouds, HDR bloom, ACES tonemap, ground-projected heat-map overlay |
| Geometry | 100% procedural at load — terrain, ocean, 25 facility types, characters, props. Zero binary assets |
| Crowd | Up to 600 agents. Utility AI over taste / need / distance / queue / density / buzz, A* on a 1.5 m nav grid with congestion-weighted costs, steering + separation, FIFO queue system with slot assignment and abandonment |
| Economy | Full double-entry ledger. Every gold and metric change carries a `CauseId` surfaced in the daily report |
| Incidents | 12 event types with staff dispatch — staff physically walk from the Ops HQ and work the site. Mitigating facilities reduce resolve time |
| Programs | Paid program cards slotted into program-capable facilities, with pre-purchase forecasts |
| Modes | Overview (RTS camera) and Ground (first-person, pointer-lock) — **Ground is strictly optional and carries no penalty** |
| Minigame | 다대포 서핑 — 52 s wave run with a steering-vs-balance tension |
| Finale | 5 purchase tiers driving a 96 s cinematic with up to 140 procedural fireworks shells |
| Audio | Entirely synthesised via WebAudio — an upbeat festival score that shifts by scene, plus sea, crowd and SFX |
| Accessibility | Colour-blind palettes, pattern overlays on all heat maps, high-contrast UI, reduced-motion, UI scaling, full KO/EN localisation |

---

## Controls

| Key | Action |
|---|---|
| `W A S D` | Pan camera / walk (Ground) |
| `Q` `E` / right-drag | Rotate |
| Wheel | Zoom |
| `Tab` | Overview ↔ Ground |
| `R` | Rotate placement |
| `X` | Demolish mode |
| `1` `2` `3` | Speed ×1 / ×2 / ×4 |
| `Space` | Pause |
| `C` / `0` | Cycle / clear heat-map overlay |
| `E` / `F` | Interact / photo mode (Ground) |
| `L` `H` `Esc` | Language / help / cancel–settings |

---

## Design-document conformance

Built against *Festa Fiesta! — 통합 기획서* (2026-07-31). Notable contracts honoured:

- **Time policy** — the simulation never pauses for incident UI, staff dispatch, Ground mode or the minigame. Only Morning Check and ESC stop the clock.
- **Speed lock** — ×2/×4 are disabled from 10 minutes before the 19:40 main show until it ends, guaranteeing minimum viewing time.
- **No mid-run game over** — a bankrupt festival enters an emergency-relief-loan state and still plays all three days.
- **Finale fallback** — a minimum finale always runs, even with no purchase (AT-007).
- **World-change contract** — validate → reserve → apply → post-validate → charge exactly once, with rollback and a typed reason code on failure (AT-003 / AT-004).
- **CauseId** — every satisfaction, safety, buzz and gold delta is attributed and shown in the report (AT-005).
- **Emergency lanes** — the blue corridors can never be built on.
- **Accessibility** — risk is never encoded in colour alone (AT-011).

Balance figures follow the document's *밸런스 시드 v0* (10,000 gold, 6 staff, 1,500/day rent,
150/staff wages, 600 hire, 300/700/1,200 cleanup, 2,000/4,000/6,000/8,000 finale tiers with
FinaleBonus +5/+12/+20/+30), tuned against instrumented full-run playtests.

---

## Deploy on Render

`render.yaml` is a Render Blueprint for a static site.

1. Push this repo to GitHub.
2. Render Dashboard → **New → Blueprint** → select the repo → **Apply**.

Or without the blueprint: **New → Static Site**, connect the repo, leave *Build Command* empty
and set *Publish Directory* to `.`.

---

## Credits

Every mesh, texture, sound effect, the music and the globe are generated procedurally at
runtime. There is not a single external asset file — no images, no audio, no fonts, no CDN.

---

MIT licensed. Fonts fall back to system stacks.
