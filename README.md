# Team event — one-pager invite

A single static web page. Colleagues open one URL, see the event details, and can
add it to their calendar (or RSVP). No build step, no framework, no backend.

- **Project folder:** `/Applications/Claude Project /Claude Projects/team-event/`
- **The whole page is driven by one `CONFIG` block** near the bottom of
  [`index.html`](index.html). Edit that block, save, done.

---

## Status / open decisions

| Decision | Choice |
| --- | --- |
| Hosting | ✅ GitHub Pages |
| Repo visibility | ✅ Public (required for free GitHub Pages — nothing sensitive on an invite page) |
| Language | ✅ English |
| Visual style | ✅ Modern, playful, minimal — light/dark aware, one accent color (`--accent` in `index.html`, currently a placeholder violet — swap for your brand color any time), drifting background shapes |
| RSVP method | ✅ Slack — page says "reply in `#team-day`". Add a real link in `CONFIG.slackUrl` (in `index.html`) to turn on the "Open Slack" button; until then it just shows the text. |
| Maps | Auto-generated Google Maps search links per agenda stop, from the venue name only. Add a city/address to `CONFIG.agenda[].map` in `index.html` for a more precise pin. |
| Photos | Placeholder tiles for now (no images available to me). Drop real files into `photos/` and list them in `CONFIG.photos` in `index.html` to swap them in. |
| Event content | ✅ Filled in — see interview notes below |

---

## Preview it locally

**Option A — just double-click** `index.html` in Finder. It opens in your browser.

**Option B — local web server** (closer to how it'll behave when hosted):

```bash
cd "/Applications/Claude Project /Claude Projects/team-event"
python3 -m http.server 8000
```

Then open <http://localhost:8000> . Stop the server with `Ctrl+C`.

---

## One-time machine setup (needed only for the GitHub step)

1. **Install git** (this Mac doesn't have it yet). Run:

   ```bash
   xcode-select --install
   ```

   A macOS dialog pops up — click **Install**, wait a few minutes, done.

2. **GitHub account** — you have one. Have your username handy for the next step.

3. _(Optional, nicer)_ **GitHub CLI** for one-command repo creation:

   ```bash
   brew install gh    # if you have Homebrew; otherwise skip — the web flow below works fine
   ```

---

## Publish to GitHub + get a shareable URL

Replace `YOURNAME` with your GitHub username.

```bash
cd "/Applications/Claude Project /Claude Projects/team-event"

git init
git add .
git commit -m "Team event invite page"
git branch -M main
```

**Create the empty repo on GitHub** — either:

- Web: <https://github.com/new> → name it `team-event` → **Public** → *don't* add a README → Create. Then:

  ```bash
  git remote add origin https://github.com/YOURNAME/team-event.git
  git push -u origin main
  ```

- Or with `gh`:

  ```bash
  gh repo create team-event --public --source=. --remote=origin --push
  ```

**Turn on GitHub Pages:** repo → **Settings** → **Pages** → Source: `Deploy from a branch` → Branch: `main` / `/ (root)` → **Save**.

After ~1 minute your page is live at:

```
https://YOURNAME.github.io/team-event/
```

That's the URL you send to colleagues.

### Updating the page later

```bash
cd "/Applications/Claude Project /Claude Projects/team-event"
git add .
git commit -m "Update event details"
git push
```

Pages redeploys automatically in about a minute.

---

## Editing the content

Open [`index.html`](index.html), find the `const CONFIG = { ... }` block, edit the
values, save. It controls the title, tagline, date/time, location, host,
description, the RSVP button, and it auto-generates the "Add to calendar"
links and the downloadable `.ics` file.

Date format is 24-hour local time: `"YYYY-MM-DD HH:MM"`.

---

## Planning interview notes

- **What is the event?** "Team Day" — a full in-person day for a remote-first team.
- **Purpose / vibe:** A bit of everything — fun, some vibe coding, shared laughs, design/coding-related games, mainly a chance to see each other in person.
- **Date & time:** Thursday... actually **Friday, October 1, 2026**, 10:00 – open end.
- **Agenda:**
  - 10:00–11:00 Breakfast — Auszeit
  - 11:00–11:45 Walk or public transit to Palavara Studio (30 min walk / 24 min transit)
  - 12:00–14:30 Pottery workshop — Palavara Pottery Studio
  - 14:30–17:30 Break / activities — Office
  - 17:30–open end Dinner — Candyman
- **Who's invited:** the team (assumed — confirm if it's everyone or a subset)
- **Host / organizer:** Anna
- **RSVP:** placeholder is email to Anna by Fri Sept 25 — _confirm actual method/deadline_
- **Company:** Inverse Studio (a design company — page should feel fun/playful/modern over corporate; explicitly does *not* need to match the studio's actual brand)
- **Prep note for pottery:** wear clothes that can get messy (or bring a change), leave jewelry/rings somewhere safe
- **Still open:** exact addresses for Auszeit / Palavara / Candyman (nice-to-have, map links currently just search the venue name)
