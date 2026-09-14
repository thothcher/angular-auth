# Auth, Authorization & Session Lifecycle — ლექცია 51

A 20-slide, single-file HTML lecture (in Georgian) about authentication in Angular apps. It covers JWT, access and refresh tokens, silent refresh, auth state with Signals, route guards and RBAC. Animated diagrams explain how things work step by step, and several slides have live demos you can click through with the audience.

![Deck tour](docs/deck-tour.gif)

---

## Quick start

1. Open [lecture-51-auth.html](lecture-51-auth.html) in a modern browser (Chrome, Edge, Firefox or Safari).
2. Press **F** for fullscreen and **→** to begin.

There is no build step. Tailwind v4 and the fonts load from CDNs, so the machine needs internet the first time. After that the browser cache is usually enough.

> Tip: the slide number is stored in the URL (`…/lecture-51-auth.html#11`), so you can reload or share a link to any slide.

## Keyboard

| Key | Action |
|---|---|
| `→` `Space` `PageDown` | next slide |
| `←` `PageUp` | previous slide |
| `Home` / `End` | first / last slide |
| `O` | overview of all slides |
| `N` | speaker notes for the current slide |
| `X` | x-ray: hover to read an element's Tailwind classes |
| `F` | fullscreen |
| `?` | help panel |
| `Esc` | close overlays |

## What's on each slide

| # | Topic | Animation / interaction |
|---|---|---|
| 01 | Title | the lock opens and snaps shut; token "chips" float around |
| 02 | Agenda | six links of one chain light up in turn |
| 03 | HTTP has no memory | two requests: the server recognises the first (token), not the second |
| 04 | Authn vs Authz | ID card scan ✓ · a keycard opens one door and is refused at the other · flip card quiz |
| 05 | JWT anatomy | header → payload → signature highlight in turn (click a part to pin it) |
| 06 | Access vs Refresh | timeline: access renews every 15 min ↻, refresh expires → logout |
| 07 | Token lifecycle | sequence diagram in sync with the six steps (click any step) |
| 08 | Where to store tokens | an XSS bug raids all four storages; httpOnly cookie shields |
| 09 | HTTP interceptor | a plain request goes in, comes out stamped with `Authorization: Bearer` |
| 10 | Idle session | **live demo**: a 15 s countdown, warning phase and lock-out overlay |
| 11 | Silent refresh | **toggle**: 4 × `/refresh` race with no lock vs one refresh with `isRefreshing` + `Subject` |
| 12 | Auth state | `setUser()` → signal → computed values → template, then `logout()` |
| 13 | Route guards | the guard sends a guest to `/login?returnUrl=…`, then lets them into `/admin` |
| 14 | RBAC matrix | permission cells cascade in |
| 15 | Permission engine | **live demo**: switch roles; the buttons pop or shake as permissions change |
| 16 | `*appHasPermission` | the button is hidden, but `curl` still reaches the API → the server answers 403 |
| 17 | Big picture | a request lights up every stage of the chain |
| 18 | Common mistakes | the mistake cards appear one after another |
| 19 | Summary | gradient key phrases |
| 20 | Thank you / Q&A | solid dark slide with drifting chips |

## Animated explainers

**Authn vs Authz** (slide 4): the ID card is verified, and the keycard opens one door but not the other.

![Authn vs Authz](docs/authn-vs-authz.gif)

| | |
|---|---|
| **HTTP is stateless** (slide 3)<br>![](docs/http-stateless.gif) | **Token lifetimes** (slide 6)<br>![](docs/token-timeline.gif) |
| **XSS vs storage** (slide 8)<br>![](docs/xss-storage.gif) | **Signals propagation** (slide 12)<br>![](docs/signals.gif) |
| **Silent refresh race** (slide 11)<br>![](docs/silent-refresh.gif) | **Route guard** (slide 13)<br>![](docs/route-guard.gif) |
| **Interceptor** (slide 9)<br>![](docs/interceptor.gif) | **Hiding ≠ security** (slide 16)<br>![](docs/hidden-button-curl.gif) |

**Token lifecycle, step by step** (slide 7): the sequence diagram and the list advance together.

![Lifecycle sequence](docs/lifecycle-sequence.gif)

## How it's built

- **One file.** All markup, CSS and JS live in `lecture-51-auth.html`. The diagrams are inline SVG animated with CSS `@keyframes`, so they stay sharp on any projector and need no image files.
- **Palette.** The colour tokens are at the top of the file, in the `@theme` block (`--color-live`, `--color-box-p`, and so on). Change them there and every slide follows.
- **Background.** One solid colour, set on `body` in the hand-written `<style>` block. There are no gradients or patterns behind the slides.
- **Diagrams.** Each diagram's CSS sits in the `/* ── ანიმირებული დიაგრამები ── */` block, labelled with its slide number (`/* 08 · XSS … */`).
- **Players.** Animations that should run only while their slide is visible register in `players` with `play()` and `stop()`. Examples are the step-by-step sequence diagram, the silent-refresh toggle, the JWT highlight cycle and the idle-session countdown.
- **Accessibility.** Slide transitions and all loops turn off when the OS asks for reduced motion (`prefers-reduced-motion`).

## Regenerating the GIFs

The GIFs in [docs/](docs/) are recorded from the real deck in headless Chrome:

```bash
cd tools
npm install puppeteer-core gifenc pngjs
node record-gifs.js            # every GIF + deck tour + cover.png
node record-gifs.js signals    # just one
```

If Chrome is installed somewhere else, set `CHROME=/path/to/chrome`.

## Files

```
auth/
├── lecture-51-auth.html   the whole presentation
├── README.md
├── docs/                  GIFs and the cover image used above
└── tools/record-gifs.js   records docs/*.gif from the deck
```
