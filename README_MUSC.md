# MUSC Sensory Room: Sonic Interventions

Production site for the MUSC sensory-room audio study. A single-page web app that presents
grouped audio players (setup, natural soundscapes, soothing music, rhythm activities) on an
iPad in the therapy room, and logs anonymous listening analytics to Google Analytics 4.

- **Live site:** https://samostroff.github.io/MUSC/
- **Hosting:** GitHub Pages (serves `index.html` from the `main` branch)
- **Contact:** Sam Ostroff — samueljostroff@gmail.com

## Repository contents

```
index.html            the live app (HTML + CSS + JS in one file) — this is what GitHub Pages serves
original_index.html   backup of an earlier version (unlinked; safe to delete — preserved in git history)
userID.html           alternate variant (user-ID capture); not part of the main participant flow
audio/                the .mp3 tracks referenced in index.html
images/               header_image.jpg, naturesounds.png, soothingmusic.png, rhythmactivities.png
```

Only `index.html` is served to participants. `original_index.html` and `userID.html` are
not linked from it.

## Google Analytics

- **Property:** "MUSC Audio Player" (property ID `a386335443p526837613`)
- **Data stream:** "MUSC Sensory Space"
- **Measurement ID:** `G-SR0VG72M7B` (hardcoded in the `<head>` of `index.html`, in both
  the gtag `src` URL and the `gtag('config', ...)` call)

### Custom events

These fire automatically as participants use the players:

| Event | When it fires |
|-------|---------------|
| `track_start` | a track begins playing |
| `track_progress` | at 25%, 50%, 75% of a track |
| `track_progress_detail` | every ~5 seconds and on pause/end (listened seconds + percent) |
| `track_complete` | a track reaches ~90% or finishes |

Each event carries `track_id`, `track_name`, `player_id`, and `player_title`, so results
can be broken down by section and by individual track in GA's Events report or in Explore.

### Monthly data-health check

To confirm collection hasn't silently stopped (broken iPad, removed tag, site down):

1. Open GA → **MUSC Audio Player** → **Reports → Realtime** (or **Admin → Events**).
2. Play a track on the live site and watch for `track_start` to appear, or check that the
   `track_*` events show non-zero counts over the last 7–28 days.
3. If `track_start` reads 0 for ~2–4 weeks or the stream shows "No stream data detected,"
   confirm the live site still loads, still contains the GA tag `G-SR0VG72M7B`, and that
   the therapy-room iPad is online.

## How the page works

- **Four players.** Player 1 is a one-track setup/volume check. Players 2–4 each hold a
  short playlist; tracks auto-advance to the next in the list when one ends, and starting a
  track pauses any other player.
- **Weekly section rotation.** Sections 2–4 are reordered once per calendar week (and the
  "jump to a section" links follow the same order) to reduce ordering bias across
  participants. Logic lives in the `rotateSectionsByWeek` script.
- **Spacebar** toggles play/pause on the focused (or first) audio element.
- **Analytics helper.** `sendGAEvent()` wraps `gtag` and no-ops if GA isn't present, so the
  player keeps working even if the analytics block is ever removed.

## Editing

- **Track list:** edit the `players` array near the bottom of `index.html` (each entry has
  an `id`, `title`, and `url`). Audio URLs currently point at
  `https://samostroff.github.io/MUSC/audio/...`.
- **Section text / intro:** the `<p>` blocks marked with HTML comments.
- **Optional surveys:** each of players 2–4 has a commented-out Google Form `<iframe>`.

## Related

A genericized, shareable version of this site (no analytics ID, relative audio paths, no
personal info) is maintained separately for other research institutions that may want to
run their own copy with their own GA property.
