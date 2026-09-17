# BotWithUs Launcher Guide

The user-facing guide for the BotWithUs Launcher, published with GitHub Pages:
**https://botwithus.github.io/launcher-guide/**

Five hand-written pages — no build step, no `node_modules`, no generator. What is in
the repo is what is served.

| File | Page |
|---|---|
| `index.html` | Get started — install, sign in, a tour of the sidebar |
| `accounts.html` | Adding accounts, launching a character, the emailed-code option |
| `scripting.html` | Opening the scripting framework |
| `arguments.html` | Editing a framework's arguments (advanced) |
| `cli.html` | `bwu_cli` commands (advanced) |
| `assets/site.css` | The whole stylesheet |
| `assets/img/` | Screenshots go here |

## Editing

Open a page in an editor and change the HTML. To preview, serve the folder — opening the
files directly with `file://` works too, but serving matches what Pages does:

```bash
python -m http.server 8080
# then http://localhost:8080/
```

The header, sidebar and footer are copied into each page rather than templated. Five pages
did not justify a build step — but it does mean **a change to the nav has to be made in all
five files**.

## Theme

Bootstrap 5 dark and bootstrap-icons from jsDelivr (the same CDN botwithus.com uses), with
`assets/site.css` on top. The `:root` block in that file is copied from the website's own
stylesheet so the guide matches botwithus.com. If the website's palette changes, update
that block.

## Deploying

Push to `main`. `.github/workflows/pages.yml` uploads the checkout and publishes it.

One-time setup on a new clone of this repo: **Settings → Pages → Source → GitHub Actions**.
Without it the workflow runs and publishes nothing.

## What must not go on this site

The audience is players and script writers. Nothing here should make the launcher easier to
attack or reverse-engineer. Specifically, do not add:

- Internals of how the launcher reaches the game — components, load order, process names,
  hardware IDs, the licensing service or how the launcher talks to it.
- The bundled Java entry's actual argument string, or any module, class or internal property
  name from it. The pages teach the *fields* and what is safe to add; a user can read their
  own entry in their own UI.
- How Script Market content is delivered, verified or loaded.
- The auto-code listener's port or endpoint — point at `bwu_cli jagex mail-setup`, which
  prints it locally and cannot go stale.
- Development-only commands and flags, or anything gated behind a debug build.
- Internal repository names, source paths, or build details.

When in doubt: describe the button and what happens, not the machinery behind it.
