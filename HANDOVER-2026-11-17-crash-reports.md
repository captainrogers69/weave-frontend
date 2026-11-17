# Handover: crash reports (Sentry) — privacy page and landing page

Written 2026-11-17 from the `notes-taker` (Weave app) session. The app now sends crash reports to Sentry. Two pages on this site say things that become untrue, or leave it out. Both must be updated and live **before** the first app release with crash reports reaches users.

House rules from `HANDOVER.md` still apply: don't commit, push or deploy (the user does; a push to this repo deploys), keep `/privacy/` at that path, plain words, short sentences.

## What changed in the app (the facts to write from)

- When Weave hits an error or crashes, it sends a **crash report** to **Sentry** (Functional Software, Inc.), stored in the **United States**.
- A report holds: the type of error and where in Weave's code it happened; app version and build; operating system and version; device model (for example "iPhone 15", "Mac14,2"); which part of the app was involved (for example sync, reminders); a **random id made on the device**, not linked to the account or email.
- Timing data (how long start-up and screens take) for about **1 in 10** sessions.
- **Never** sent: task or list text, email, account id, the device's name, screenshots, IP address (Sentry is set to store none).
- Sent **with or without an account**. That is the big change: until now, without an account nothing left the device.
- Users can turn it off: **Settings → Crash reports → Send crash reports**. On by default.
- Reports are kept for **up to 90 days**, then deleted. They aren't linked to the account, so deleting the account doesn't remove them; they expire. (Confirm the 90 days with the user: it depends on the Sentry plan.)
- Still true: no ads, no analytics, no tracking, nothing sold.

## 1. Privacy page (`privacy/index.html`)

Change **Effective 13 November 2026** to the date the page goes live.

| Where | Now | Change to |
|---|---|---|
| In short, bullet 1 | "Without an account, everything stays on your device. We receive nothing." | "Without an account, your lists and tasks stay on your device. If the app runs into an error, it sends us a crash report (never your tasks, lists or email); you can turn this off in Settings." |
| In short, "No ads, no analytics, no tracking…" | — | Keep as is. Still true. |
| Using Weave without an account, last sentence | "Nothing is sent to us." | "Your lists and tasks are never sent to us. The only thing that can leave your device is a crash report (see Crash reports below)." |
| What we don't collect | "No crash reporting services." | "No screenshots, screen recordings or text from your lists in crash reports." |

**New section** after "Using Weave with an account":

> **Crash reports**
>
> When Weave runs into an error or crashes, it sends a crash report so we can find and fix the problem. A crash report contains:
>
> - the type of error and where in Weave's code it happened,
> - the app version, your operating system and version, and your device model (for example "iPhone 15" or "Windows PC"),
> - which part of the app was involved (for example sync or reminders),
> - a random identifier created on your device, so we can tell how many devices an error affects. It is not linked to your account or email.
>
> Weave also sends timing information for a small share of sessions (for example how long the app takes to start), to find slow parts of the app.
>
> Crash reports never include the text of your tasks or lists, your email address, your account, your device's name, screenshots or your IP address.
>
> Crash reports are sent whether or not you have an account. You can turn them off at any time: Settings → Crash reports → Send crash reports. Reports already sent are kept for up to 90 days and then deleted.
>
> We process crash reports because we have a legitimate interest in keeping Weave working and fixing errors; you can object at any time by turning them off.

**Service providers**, new bullet after Supabase:

> Sentry (Functional Software, Inc.) receives crash reports and stores them on our behalf in the United States. See the Sentry privacy policy (https://sentry.io/privacy/). Sentry protects transfers from the EEA and UK with Standard Contractual Clauses.

**Keeping and deleting your data**, new bullet:

> Crash reports are kept for up to 90 days. They aren't linked to your account, so deleting your account doesn't find them; they expire on their own.

## 2. Landing page (`index.html`) — checked 2026-11-17

Every privacy claim on the page, checked against the app:

| Line | Where | Verdict |
|---|---|---|
| "Yours, and only yours." | `#yours` heading, ~line 478 | OK |
| "Free / while in beta", "No account needed / sign in only to sync", "Delete anytime / in Settings" | facts list, ~480–482 | OK (account data is still deleted in Settings) |
| "Weave keeps your lists on your device first, and works without an account. Sign in with your email only if you want sync. There are no ads, no analytics and no tracking." | first `.statement`, ~485 | OK. Crash reports aren't analytics or tracking, and the lists do stay on the device. |
| "To sync, we store your email, your changes and the names of your devices. It isn't end-to-end encrypted, and you can delete it all from Settings. The privacy policy has the details." | second `.statement`, ~486 | **Incomplete**: says what is stored for sync but not that crash reports are sent, with or without an account. Add one sentence (below). |
| Meta description, `og:description`, hero line ("works offline, rings on time and syncs…") | `<head>`, hero | OK |
| Demo note "Your list stays in this browser after a reload…" | demo | OK (about the web demo) |

**Proposed change** to the second statement, before "The privacy policy has the details.":

> "If the app runs into an error, it sends us a crash report so we can fix it: never your tasks, lists or email, and you can turn it off in Settings."

Keep it one sentence, same tone. If it makes the block too long on phones, it can replace "It isn't end-to-end encrypted," only with the user's OK; that line is a deliberate honesty point.

## 3. One more thing to check: Netlify's injected script

The **live** page has a script the local `index.html` doesn't:

```html
<script async src="/.netlify/scripts/hud?variant=public" … data-account-tier="free"></script>
```

plus a Netlify comment with a `utm_` link at the top. Netlify adds these at deploy. Find out what the script does and whether it can be turned off in the Netlify site settings. The page says "no analytics and no tracking" about the app, but a reader will take it for the site too; the site shouldn't load anything that tracks visitors. Report to the user before changing settings.

## Checklist

- [ ] Privacy page edited as in section 1, new effective date.
- [ ] Landing page sentence added (section 2).
- [ ] Netlify script checked (section 3), result told to the user.
- [ ] Retention "up to 90 days" confirmed with the user.
- [ ] Pages reviewed by the user, then committed and deployed by the user before the app release.
- [ ] Tell the app side when it's live (the app session keeps a note of what the policy says).

Source of these facts in the app repo: `~/Downloads/notes-taker/docs/privacy/crash-reporting.md` (also has the App Store and Play form answers, which the user fills in; not this team's job).
