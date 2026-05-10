# Lumen — v0.2

A closed-eye stroboscopic flicker light stimulation app for the Meta Quest 2 browser. Two protocols, research-aligned music, configurable color and rhythmicity. Built around findings from Amaya et al. 2023 (PLOS ONE) and Montgomery et al. 2024 (Frontiers in Psychology).

## What it is, what it isn't

It is: a single HTML file that runs in any modern browser, including the Quest 2 browser. Closed-eye full-field flicker. No app store, no SDK, no immersive WebXR. Closed eyes diffuse spatial patterns, so we work with what actually transmits through eyelids: brightness, color, and timing.

It is not: a medical device, a therapy, or a substitute for one. The warning screen is not boilerplate.

## What you need

1. A Meta Quest 2 (or any device with a fullscreen-capable browser).
2. A GitHub account.
3. The music tracks listed below, as M4A, MP3, or WebM files. Acquire from Bandcamp, iTunes, or another legitimate source. Spotify Premium "downloads" are encrypted and won't work.

## Music shopping list

Just two tracks, both Greg Haines:

| File path | Track | Album | Duration |
|---|---|---|---|
| `tracks/azure.m4a` | Azure | *Azure* (EP, 2013) | 14:14 |
| `tracks/so-it-goes.m4a` | So It Goes | *Where We Were* (2013) | 7:17 |

Both are available on Bandcamp at [greg-haines.bandcamp.com](https://greg-haines.bandcamp.com), iTunes, and most other commercial platforms. Spotify Premium "downloads" are encrypted and won't work; you need actual audio files (M4A from iTunes or MP3 from Bandcamp both work).

Filenames matter: rename your downloads to exactly `azure.m4a` and `so-it-goes.m4a` and put them in a `tracks/` folder alongside `index.html`. If a file is missing, that segment plays silent and the flicker continues. The app handles missing files gracefully.

### How the music maps to each protocol

**Compact (20 min):** Azure plays from t=0 (start of session) through Settling, Onset, Peak, and into Plateau. So It Goes takes over at t=14:14 and carries the descent through color exploration, Valley, Re-entry, and final silence. The track transition coincides with the perceptual shift from peak to descent.

**Long-form (90 min):** Music anchors the two peaks; silence carries the integration. Specifically:

- 0:00 to 5:00: Settling (silent)
- 5:00 to 19:14: Azure plays through Onset and First Peak (10 Hz)
- 19:14 to 50:59: Silent flicker (Plateau, color phases, First Valley, Integration, Renewal). About 32 minutes of music-free flicker journey.
- 50:59 to 58:16: So It Goes plays through Second Peak (18 Hz) and into Tenderness
- 58:16 to 90:00: Silent flicker (descent, hold, approach silence, re-entry). About 32 more minutes.

Symmetric: roughly 32 minutes of silence on each side of each musical anchor. This is intentional and borrows from psychedelic-assisted therapy music protocol design, which treats silence during integration as a feature rather than dead space.

One caveat: at 18 Hz, So It Goes will probably feel slightly mismatched (a slow piece against fast strobe). The Montgomery 2024 participants flagged this kind of mismatch as a real perceptual issue. The track is shorter than Azure, so the mismatch window is briefer. If it feels wrong after a real session, we can swap which track plays at which peak.

## GitHub setup, step by step

### Is your GitHub integrated with this Claude session?

No. Your visible connectors here are Gmail, Google Calendar, Google Drive, Dropbox, and Microsoft 365. No GitHub. For a single HTML file plus a tracks folder, manual upload through the github.com web UI is genuinely fine and takes about two minutes per iteration. **Use Claude Code on desktop only when iteration heats up** (multiple files, many small commits, or you want to run the app locally before pushing). For now, web UI is the right call.

### One-time repo creation

1. Go to **https://github.com/new**.
2. Name it something like `lumen` (or anything you want; the URL slug ends up in the GitHub Pages address).
3. Make it **Public** (required for free GitHub Pages on personal accounts; if you want it private, you need GitHub Pro).
4. Check **"Add a README file"** so the repo isn't empty.
5. Click **Create repository**.

### Upload the files

1. In your new repo, click **"Add file" > "Upload files"**.
2. Drag `index.html` and `README.md` into the dropzone.
3. Drag the `tracks/` folder in too. (You can drop a whole folder; GitHub preserves the structure.)
4. Scroll down. Commit message: anything sensible like "Initial v0.2 upload."
5. Click **Commit changes**.

If the tracks total over 100 MB, you'll need to upload them in batches (GitHub's web UI has a per-commit limit). Ten or fifteen tracks at typical compression should fit fine.

### Turn on GitHub Pages

1. In the repo, click **Settings** (top right).
2. Left sidebar, click **Pages**.
3. Under "Build and deployment," **Source** = "Deploy from a branch."
4. **Branch** = `main`, folder = `/ (root)`. Click **Save**.
5. Wait one or two minutes. The page will show "Your site is live at https://YOURUSERNAME.github.io/lumen/" once deployment finishes.

### Iteration workflow

When I send you a new version of `index.html`:

1. Go to your repo on github.com.
2. Click on the existing `index.html` file.
3. Click the pencil icon ("Edit this file") at the top right.
4. Select all (Ctrl/Cmd-A), paste the new contents.
5. Scroll down, commit message, click Commit.
6. GitHub Pages redeploys in 30 to 90 seconds.

That's the loop. You don't need git CLI, you don't need Claude Code, you don't need anything installed. When this loop becomes annoying (probably around v0.4 or v0.5), we switch to Claude Code on your desktop.

## Testing on Quest 2

### First-time setup

1. Put on the Quest 2. Open the **Browser** app.
2. Type your URL: `https://YOURUSERNAME.github.io/lumen/`
3. Bookmark it.

### Running a session

1. Read the safety screen, tap **I Understand**.
2. Pick a protocol on the home screen. Tap **Continue**.
3. Wait for the audio status to show how many tracks were found (this is a pre-flight HEAD check on every track URL).
4. Adjust master brightness if you want. Choose music or silent.
5. Tap **Begin**. The browser should request fullscreen; accept.
6. Close your eyes. The Quest's pancake lenses already block most ambient light; the browser's full-bright white is the photic source through your eyelids.
7. To end early: tap anywhere on the screen, or press space if you have a keyboard paired.

### What to watch for on the first run

- Audio playback. The Quest browser sometimes blocks autoplay until user gesture; tapping **Begin** counts as the gesture. If music doesn't start, that's the most likely cause and we'll adjust.
- Phase transitions. The "Settling" phase at the start is intentionally dark and silent for 90 seconds (5 minutes on long-form). Don't think the app is broken.
- Wake lock. The screen shouldn't dim mid-session. If it does, the wake lock API is unsupported in your Quest browser version and we'll work around it.

## Dev mode (for testing without sitting through 20 minutes)

URL parameters let you fast-forward and inspect the protocol without waiting.

| URL | Effect |
|---|---|
| `https://...lumen/` | Normal session. |
| `https://...lumen/?dev=1` | Shows a debug overlay during the session: current time, phase, frequency, rhythmicity, brightness, scheduled flash count. |
| `https://...lumen/?speed=10` | Runs the timeline 10x faster. The 20-min compact protocol completes in 2 minutes. |
| `https://...lumen/?dev=1&speed=20` | Both. Useful for verifying the long-form arc in 4-5 minutes. |

Speed range: 0.1x to 60x. Audio also fast-forwards (it seeks to the right offset when each track triggers), so don't use ?speed for anything you want to actually listen to.

## Protocol structure (for the curious)

Each protocol is a list of phases. Each phase has:
- Frequency in Hz (10 = canonical Amaya peak, 0 = no flicker)
- Rhythmicity (rhythmic, arrhythmic-norm with normally-distributed inter-flash intervals, or arrhythmic-pairs with paired flashes per Amaya 2023)
- Duty cycle (0.30 throughout, the research-standard "ON" fraction)
- Color (hex), the "ON" color
- Brightness ramp from start to end of phase (0 to 1)

The **Compact** arc: 90s settling → 8 minutes climbing 6 to 10 Hz at white → 2.3 minutes peak at 10 Hz white → ~5 minutes color exploration (amber, then cool blue, then back to white) → 1.7 minutes arrhythmic valley at 6 Hz → 25 seconds re-entry → 6 seconds silence.

The **Long-form** arc: 5 minutes settling → 9 minutes onset → 5 minutes first peak → 4 minutes plateau → ~4 minutes color exploration → 5.5 minutes arrhythmic first valley → 14 minutes deep integration at 4 Hz → 4 minutes renewal → 5.4 minutes 18 Hz second peak (the experimental segment, brighter and more intense) → 3.4 minutes amber tenderness → cooldown → 8.3 minutes long arrhythmic descent → 6 minutes hold space → 8 minutes approach silence → 5.2 minutes re-entry.

## Known limits and what comes next

- The session can't be paused mid-flow, only ended. By design for now. We can add pause if you want it after a few sessions.
- Color is rendered through CSS background swaps on a single div, not WebGL. This is fine at 18 Hz. If we go higher or want spatial variation, we move to a canvas.
- No EMDR mode yet. That's v0.4.
- No open-eye kaleidoscope mode yet. That's v0.3.

## Citations

Amaya IA, Behrens N, Schwartzman DJ, Hewitt T, Schmidt TT (2023). Effect of frequency and rhythmicity on flicker light-induced hallucinatory phenomena. PLoS ONE 18(4): e0284271. https://pmc.ncbi.nlm.nih.gov/articles/PMC10089352/

Montgomery C, Amaya IA, Schmidt TT (2024). Flicker light stimulation enhances the emotional response to music: A study comparing light- and sound-induced emotions. Frontiers in Psychology 15:1325499. https://pmc.ncbi.nlm.nih.gov/articles/PMC10901288/
