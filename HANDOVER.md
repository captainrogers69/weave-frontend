# Handover: Weave site landing page

Written 2026-11-13 from the `notes-taker` (Weave app) session. Start here when working on this repo.

## The ask

Redesign the landing page (`index.html`). The current page is a dark screen with the centred yellow icon, "Weave", one line of text, and Privacy / Support links. The redesign must look designed, not generated ("AI slop" is the user's word for what to avoid), and carry the same creativity and style as the store preview images (below).

**Not done yet:** the new `index.html` was drafted but never written; the live page is unchanged. The direction, copy and pictures below are decided and ready to build.

## House rules from the user

- **Don't commit, push or deploy.** The user commits. Netlify deploys from this repo, so a push makes changes live.
- `/privacy/` is the privacy policy URL every store points at. Keep that path working, and keep its claims true to the app (see "Facts").
- Don't change the logo. The mark is locked: a yellow rounded square whose top-right corner lifts as a black quarter circle (`icon.svg`).
- Text the user reads: plain words, no jargon, concise.

## Brand

| Thing | Value |
|---|---|
| Yellow | `#F5C84C` (the icon) |
| Ink | `#141414` (the icon's corner) |
| App list colours (good as fields) | green `#CFE8D6`, blue `#D4E2FA`, purple `#E0D8FA`, pink `#F6D5E3` |
| Font | Geist, Medium (500) for headlines, Regular (400) for text. Files are in `fonts/` (from the app), with `OFL.txt` |
| Name | Store name "Weave - Tasks & To-Do List". On the page, just "Weave" |
| Lines already in use | "Remember less. Do more." (App Store subtitle), "Your whole day, on one thread.", "Your to-dos, finally sorted." |
| Tone | Friendly, a bit playful ("hi, laundry"), short sentences, no hype |

## The style of the store preview images (match this)

The images live in the app repo: `~/Downloads/notes-taker/docs/store/<platform>/`, drawn by `tool/store_art/styled.py` and `compose.py`. Open a few before designing; the user liked them.

What makes them work:

1. **Real app screens.** Every image shows the actual app, rendered from Flutter with believable sample data (tasks like "Send the Q4 report to Anna 11:00", "Post the parcel 17:30", "Water the plants 19:00", "Book the flights, Tomorrow 18:00"). No made-up UI.
2. **One short headline per image, with one word marked.** For example "Your whole day, on one *thread*.", "Lists that feel like *paper*.", "Reminders that ring *on time*.", "Easy on the eyes, *day or night*.", "Every list, every *device*.", "A list that *floats* over any app.", "Find *anything*, instantly." The marked word sits on a rounded highlighter block (white on yellow, yellow on the others), in ink. A short subline underneath in a softer colour.
3. **One colour theme per image**, rotating yellow, green, purple, ink (dark) and blue, so a row of images reads as a set.
4. **Lifted callouts.** A crop of the UI (the Today card, the reminder options, the top search results) is cut out, enlarged, slightly rotated (1.5–3°) and lifted off the device with a soft shadow, so the eye goes to the feature.
5. **Depth from overlap.** A phone in front of a laptop or window (sync), two phones tilted against each other (lists), one device split diagonally into light and dark with a yellow line on the cut.
6. **The brand row** (icon plus "Weave") on the first image only.

**What the user rejected:**
- A blurred navy-to-brown gradient behind the Microsoft Store poster ("looks AI slop").
- Yellow icon on a yellow background (it disappears).

**What they liked as the fix:** the Microsoft Store poster and box art (`docs/store/windows/logos/`). Flat yellow, the black lifted corner made huge in the top right, "Weave" in big ink type bottom left, and "Remember less. Do more." under it. Flat colour, big type, the mark as the composition.

For the web: the mesh gradients and soft shadows in the store images suit store screenshots. On the site, prefer flat fields of brand colour, big Geist type and real app screens. Don't use blurred gradients, glows or glass.

## Design plan (decided, using the design-taste-frontend skill)

Notes are in `.taste-skill/notes.md`, and the full direction sheet is in `.taste-skill/direction.json`. Reprint it with:

```sh
node ~/.claude/skills/design-taste-frontend/scripts/draw.mjs --show
```

**Direction:** "The sentence is the layout" (seed 1373249346). Brand palette and type kept.

**The idea:** the headline is the store line "Remember less. / Do [ ] more.". The gap inside it is a small white card (the app's real Today strip, `img/today-strip.webp`) whose top-right corner is Weave's black lifted corner. So the sentence holds the product, drawn as the logo.

**The one interactive thing:** "Type it the way you'd say it." A big input where you type a task with a time ("Dentist fri 10am", "Call mum tomorrow 6pm", "Stretch in 2 h"). It lands as a row in a small list with the time read out ("Fri 10:00", "Tomorrow 18:00"). You can tick rows off, and the list is saved in the browser so it survives a reload, like the app saving offline. This is honest: the app's own input says "Times work too: 6pm, tomorrow, in 2 h". Don't claim anything beyond day and time words (no "every Tuesday" parsing on the page).

**Sections, in order:**

1. **Hero, two fields.** Ink field on top with line 1 in yellow; yellow field below with line 2 in ink, the card in the slot, and the supporting sentence: "Weave is a to-do list that works offline, rings on time and syncs your phone, Mac and PC." The top bar has the mark and "Weave", the links (Try it, What it does, Screens, Privacy) and one button, "Join the beta".
2. **Try it.** The live input above, the list card at real app size, three example buttons.
3. **What Weave does: sentences with switches.** Full-width bands, each one sentence plus a working toggle. When on, the band fills with a list colour and a consequence line appears:
   - "Ring me right on the minute." → "Set 18:00 and hear it at 18:00, not five minutes late." (yellow, on)
   - "Keep working with no signal." → "Every change saves on the device first. Sync catches up when you're back online." (green, on)
   - "Sync my phone, Mac and PC." → "Sign in with your email, if you like. Edit on two devices at once and both changes stay." (blue)
   - "Float a list above every app." → "The mini bar on Mac and Windows: tick things off without switching windows." (purple)
   - "Repeat it, then forget it." → "Daily, weekly, monthly. Bins on Tuesday, rent on the 1st, laundry forever." (pink)
4. **On every screen: a run of frames on ink.** Heading on the left, a row of real screens on the right at one height, with one frame lifted. The frames are phone Up next, Mac Up next, the mini bar, phone dark mode, Windows search and a green list.
5. **Yours, and only yours.** A paragraph with the Weave mark as a drop cap three lines tall: local first, account optional, no ads, no tracking, delete anytime, and a link to the privacy policy. Three small facts on the left: Free; No account needed; Delete anytime.
6. **Get it: "Phone or / computer?"** A full-screen ink field with the question split top and bottom. In the middle, two buttons: "iPhone or Android" and "Mac or Windows". Both are `mailto:mobiledev.mayank@gmail.com` with a prefilled subject, because the apps are in beta with no public store links yet. Under them: "Weave is in beta. Email us and we'll reply with a test invite for that device."
7. **Footer.** A yellow field: "Remember less, starting today." plus the button; links to Privacy policy, Delete your account (`/privacy/#delete-account`) and Support; "© 2026 Mayank Mobile Dev"; then a huge "Weave" cropped by the bottom edge.

**Motion:**
- The top bar's colour follows the section under it (300ms).
- Each section's parts rise in, staggered about 80ms apart.
- The corner on the hero card lifts in on load, and the Today strip drifts slowly.
- Buttons and toggles respond to press and hover.
- Everything turns off under reduced motion.

**Phone layout:** the hero lines at about 11.6vw so "Remember less." fits on one line, the bands at least 132px tall, the frame run scrolling sideways, and the CTA buttons stacked.

**Rules from the skill to keep:**
- headlines at most two lines at every width;
- equal margins on both sides;
- no small labels above headings;
- no 01/02/03 numbering;
- no hairline dividers, gradients, shadows at rest, glass or emoji.

**Checks to run after building, from the repo root:**

```sh
S=~/.claude/skills/design-taste-frontend
node $S/scripts/lint.mjs index.html
node $S/scripts/inspect.mjs index.html      # aim for 0 FAIL at 1440 / 768 / 390, then look at every screenshot
```

## Files prepared in this repo (untracked)

| Path | What |
|---|---|
| `img/today-strip.webp` | The Today card header and timeline (for the hero card) |
| `img/phone-up-next.webp`, `phone-dark.webp`, `phone-list.webp` | iPhone screens (status bar cropped off) |
| `img/mac-up-next.webp`, `img/pc-search.webp` | Mac and Windows windows |
| `img/mini-bar.webp` | The mini bar, opened |
| `fonts/Geist-Regular.ttf`, `Geist-Medium.ttf`, `OFL.txt` | The brand font and its licence |
| `.taste-skill/` | Design notes and direction. Scratch: add it to `.gitignore`, don't ship it |

To make the screens again after an app UI change (in `~/Downloads/notes-taker`):

```sh
flutter test test/store/store_raw_test.dart test/store/mini_bar_raw_test.dart --dart-define=STORE_SHOTS=true
# raw PNGs land in build/store_raw/<platform>/; crop and export to webp (Pillow), as was done for img/
```

## Facts the page must stay true to

- **What it is:** offline-first lists and tasks, with the app saving on the device first.
- **Up next:** what's due today and later this week.
- **Reminders:** due dates, repeats and reminders that ring on the minute.
- **Lists:** colour-coded lists; Archive and Trash with undo; search.
- **Sync:** optional email sign-in syncs phone, Mac and PC. When two devices edit at once, both changes are kept.
- **Mini bar:** on Mac and Windows only, switched on in Settings → Mini bar.
- **Data:**
  - no ads, analytics, tracking or crash reporting;
  - Supabase stores only the email, the synced changes and the devices (name, platform, last seen);
  - not end-to-end encrypted;
  - the account is deleted from Settings → Delete account.
- **Release state:**
  - **iOS and macOS:** on TestFlight.
  - **Android:** going to Play testing.
  - **Windows:** release on hold. Say "PC" for sync, but don't promise a Windows download.
- **Contact:** `mobiledev.mayank@gmail.com`. Publisher: Mayank Mobile Dev.
- **Domain:** `weave-frontend.netlify.app`, later `weave.mobilemayank.com`.
