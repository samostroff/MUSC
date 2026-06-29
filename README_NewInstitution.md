# Sensory Room: Sonic Interventions — Site Template

A lightweight, single-file web app that presents grouped audio players (setup, nature
soundscapes, soothing music, rhythm activities) for use on a tablet in a sensory room.
It optionally logs anonymous listening analytics (which tracks were started, progress,
and completion) to your own Google Analytics 4 property.

This is a shareable template. It contains **no analytics ID and no personal contact
info** — you fill those in. The audio player works out of the box even if you never
enable analytics.

## What's in the repo

```
index.html        the whole app (HTML + CSS + JS in one file)
audio/            your .mp3 files (filenames must match those listed in index.html)
images/           header_image.jpg, naturesounds.png, soothingmusic.png, rhythmactivities.png
```

## Quick start

1. Put your audio files in an `audio/` folder and your images in an `images/` folder.
   The template expects relative paths like `audio/Nature9.mp3` — either name your files
   to match the list inside `index.html`, or edit the `players` array near the bottom of
   `index.html` to match your filenames and titles.
2. Host the folder anywhere that serves static files (GitHub Pages, Netlify, an internal
   web server, etc.). On GitHub Pages, putting these files in a repo and enabling Pages
   is enough.
3. Open the page on your tablet. Done — analytics is optional (see below).

## Enabling your own Google Analytics (optional but recommended for research)

Each institution should use its **own** GA4 property so the data stays under your control
(consent, IRB, privacy). Do not reuse anyone else's Measurement ID, and don't share yours.

1. Go to https://analytics.google.com → Admin → **Create property**. Give it a name
   (e.g., "Sensory Room Audio").
2. Under the new property, create a **Web data stream** pointing at the URL where you'll
   host the site. Copy its **Measurement ID** — it looks like `G-XXXXXXXXXX`.
3. Open `index.html`, find the commented-out **GOOGLE ANALYTICS (OPTIONAL)** block near
   the top, uncomment it, and paste your Measurement ID in **both** spots (the script
   `src` URL and the `gtag('config', ...)` line).
4. Save, deploy, load the page, and play a track. In GA go to **Reports → Realtime** and
   confirm a `track_start` event appears within a minute or two.

### Custom events the page sends

Once analytics is enabled, these fire automatically — no extra setup:

| Event | When it fires |
|-------|---------------|
| `track_start` | a track begins playing |
| `track_progress` | at 25%, 50%, 75% of a track |
| `track_progress_detail` | every ~5 seconds and on pause/end (listened seconds + percent) |
| `track_complete` | a track reaches ~90% or finishes |

Each event includes `track_id`, `track_name`, `player_id`, and `player_title`, so you can
break results down by section and individual track in GA's Events report or in Explore.

## What to customize before sharing/deploying

- **Contact line** at the bottom of `index.html`: replace `[YOUR NAME]` and
  `your-email@example.com`.
- **Intro and per-section text**: the `<p>` blocks marked with comments.
- **Google Form embeds** (optional): each player has a commented-out `<iframe>`. Replace
  `YOUR_FORM_ID` with your own form's embed ID and uncomment to collect survey responses.
- **Track list**: edit the `players` array to match your audio files.

## Notes

- The page reorders the three rotating sections once per calendar week to reduce ordering
  bias. You can remove the `rotateSectionsByWeek` script if you don't want this.
- **Audio licensing:** make sure you have the rights to host and distribute whatever audio
  you place in `audio/`. The original study's tracks were custom-composed and are not
  included in this template.
