# Timesheet

A single-page PWA for clocking in and out and splitting the day across projects.
No backend, no build step, no accounts — everything lives in your browser.

<!-- screenshot.png goes here -->

## What it does

- Clock in and out with one tap; a running day counts up live.
- Fix the times by hand when you forget, and set a lunch deduction.
- Split the day across projects by dragging a bar or typing percentages.
- See the week at a glance, with per-project totals in decimal hours.
- Export and import your data as JSON.

## Running it

Open `index.html` over HTTP — service workers need a secure origin, so `file://`
won't do:

```
python3 -m http.server 8000
```

Every path is relative, so it also works from a GitHub Pages project page
(`user.github.io/timesheet/`), a user page, or a custom domain.

## Installing on iPhone

Open the URL in **Safari** (Chrome on iOS can't install PWAs), tap Share →
*Add to Home Screen*. It then launches full screen with no browser chrome.
On desktop Chrome or Edge, use the install icon in the address bar.

## Shipping an update

Change the files, bump `CACHE` in `sw.js` (`timesheet-v12` → `v13`), push.
Installed copies pick up the new version the next time they're opened online.
Without the bump, phones may keep serving the cached build.

## Your data

Stored under the `timesheet.v1` key in localStorage, on each device separately —
a phone and a laptop don't share hours. iOS can evict the storage of a site you
haven't opened in a few weeks, though installing to the home screen makes that
much less likely. Use **Export JSON** now and then; **Import JSON** replaces
everything, so it restores a backup rather than merging two devices.
