# "Our August" — 30-day advent calendar

## How it works
- `index.html` shows a real August calendar. Days grey out until their date arrives.
- Each day lives in its own file: `days/day-01.json` through `days/day-30.json`.
- Only days whose date has already passed even get downloaded by the browser — so there's nothing to find in the page source for future days, and no single view-source reveals every passcode or answer at once.
- Every day needs its own word. You send her that day's word each morning (text, or however you like) — the site doesn't display it anywhere.
- Once she enters the right word **on or after** that day's date, it unlocks permanently in her browser (via `localStorage`) — she can always scroll back and re-open any past day.
- Day 30 (Aug 30, her birthday) also triggers a **finale banner** at the top of the page with a bigger message and a tap-to-reveal for the real gift.

## 1. Fill in each day
Open any `days/day-XX.json` file — plain text editor is all you need. Example:

```json
{
  "day": 5,
  "passcode": "changeme-05",
  "message": "The message or caption for this day.",
  "media": ["assets/day05-photo.jpg"]
}
```

- `passcode` — change this to whatever word you'll text her that day. Keep it something only you two would land on (not literally "changeme").
- `message` — plain text (a note, a memory, a question). You can leave it as `""` if a day is media-only.
- `media` — a list of file paths. Leave it as `[]` for text-only days. Add one or more paths for photo/video/audio days:

```json
"media": ["assets/day12-video.mp4"]
```
```json
"media": ["assets/day18-a.jpg", "assets/day18-b.jpg"]
```

The site figures out image vs. video vs. audio automatically from the file extension (`.jpg/.png` → photo, `.mp4/.mov` → video, `.mp3/.m4a` → audio). You can mix a message with media on the same day — it just shows both.

Day 30 has one extra field:
```json
"finaleMessage": "The big message that appears in the special birthday banner."
```

## 2. Add your photos, videos, and audio
Drop the actual files into the `assets/` folder, named to match what you put in each day's `media` list.

**Compress before uploading** — this matters more here than the last version, since video/audio files are much bigger than photos:
- **Photos:** https://squoosh.app — export ~800px wide, JPG/WebP, quality 75–80%.
- **Videos:** keep clips short (10–30 sec) and compress them. If you're comfortable with the command line (which, as an IT guy, you probably are):
  ```
  ffmpeg -i input.mp4 -vf scale=720:-2 -crf 28 -preset veryfast -c:a aac -b:a 96k output.mp4
  ```
  This usually gets a phone video down to a few MB with no visible quality loss. If you'd rather use a GUI, HandBrake (free) does the same thing.
- **Audio (voice notes):** these are already small — no real compression needed, just export as `.m4a` or `.mp3`.

Keep an eye on total size — GitHub rejects individual files over 100MB, and Netlify's free tier has a 100MB per-file limit too. A month of short, compressed clips will stay well under that.

## 3. Set your name and the finale
In `index.html`:
- Replace `[Your Name]` in the footer.
- Fill in `[Write your big final message here...]` in the finale banner section — or just rely on day 30's `finaleMessage`, which overrides it automatically once unlocked.
- Fill in the `#gift-text` placeholder with whatever the real gift/plan reveal is.

## 4. Test it locally (important — this is different from a single-file site)
Because the site *fetches* each day's JSON file, opening `index.html` by double-clicking it won't work — browsers block that kind of local file access for security reasons. You need a tiny local server, which takes one command:

```
cd advent-site
python3 -m http.server 8000
```
Then open `http://localhost:8000` in your browser. (Any language's simple server works — Python's is just the one-liner.)

To test the date-gating without waiting for August, temporarily change `START_DATE` near the top of the `<script>` in `index.html` to an earlier date, refresh, then change it back before you go live.

## 5. Host it for free
Same two options as before, but note the file-size point above:

**Netlify** — go to https://app.netlify.com/drop and drag the whole `advent-site` folder in. Instant live link.

**GitHub Pages** — push the whole `advent-site` folder to a repo, then Settings → Pages → deploy from `main`. Live at `https://yourusername.github.io/advent-site/`.

Either way, once it's live, the `python3 -m http.server` step is no longer needed — the fetch requests just work normally over the internet.

## 6. Send it
Give her the link on August 1st. Each morning after that, text her that day's word. On August 30th, whatever word you set for day 30 also opens the finale.

---
**Honesty note on security:** like the passcode idea before, this is a soft gate, not real security — someone who really wanted to could open dev tools and find a day's word once that day's file has loaded, or nudge their system clock forward to make a future day "available" early. For a gift like this, that's a non-issue — the point is pacing and delight, not preventing determined snooping.
