# Project: "Our August" — 30-Day Birthday Countdown Site

## Purpose

A personalized, self-built birthday gift for my girlfriend, replacing a single store-bought present with a month-long experience she opens a piece of every day.

Starting **August 1** and running through her birthday on **August 30**, she gets one new passcode-protected page each day containing a photo, video, voice note, or message — something no off-the-shelf gift could replicate. On her birthday, a final page unlocks with a bigger closing message and the reveal of the real, physical gift, while every previous day's page stays visible so the whole month can be looked back on as one keepsake.

## Why this format

- **Daily anticipation, not a one-time reveal** — spreads the gift out over the entire lead-up to her birthday instead of a single moment.
- **Personal effort as the gift itself** — built from scratch rather than bought, using my own skills (IT/dev background) as the thing that makes it meaningful.
- **Mixed media** — not limited to just photos; each day can be whatever fits best (a memory, a video, a voice note, a note).
- **A keepsake afterward** — because past days stay unlocked and viewable, the finished site becomes a full archive of the month, not something that disappears after each day.

## How it works (mechanics)

- A real August calendar grid on the page — days are greyed out until their actual date arrives.
- Each day requires a unique passcode, sent to her separately (e.g. by text) each morning — the site never reveals it.
- A day only opens once **both** conditions are met: its date has arrived, and the correct word is entered.
- Once opened, a day stays unlocked permanently in her browser, so she can revisit any previous day at any time.
- Day 30 (her birthday) additionally triggers a **finale section** — a distinct part of the page with a longer closing message and a tap-to-reveal for the actual physical gift.

## What was built

| File/Folder | Purpose |
|---|---|
| `index.html` | The site itself — calendar UI, passcode gate, content viewer, finale logic |
| `days/day-01.json` … `day-30.json` | One file per day: passcode, message, and media references — kept separate so no day's content or password is visible before its date |
| `assets/` | Folder for the actual photos, videos, and audio clips |
| `README.md` | Step-by-step setup guide: filling in content, compressing media, testing locally, and hosting for free (Netlify / GitHub Pages) |

## Status

Structure and logic are built and working. Remaining work is content: writing each day's message, choosing/compressing the media for each day, picking the 30 passcodes, and writing the finale message and real-gift reveal — then hosting it and sending the link on August 1st.
