# College Lost and Found

A simple website where college students can post items they have lost and items they have found, so belongings get back to their owners.

The whole site is one file: `college-lost-and-found.html`. There is nothing to install or build.

## Features

- **Post a lost item** or **post a found item** using a short form (item name, category, date, place, details, your name, and a phone number or email).
- **Browse all posts** as tag-style cards, with lost items in coral and found items in green.
- **Filter** by All, Lost or Found, and by category.
- **Search** across item names, places, categories and details.
- **Show contact** on a card to reveal the poster's phone or email. Click it again to copy it.
- **Mark as found or returned** to fade a card and move it to the bottom of the list. Click **Reopen** to undo.
- **Delete** a post you no longer need.
- Works on phones and desktops, supports keyboard navigation, and respects reduced-motion settings.

## How to run

1. Download `college-lost-and-found.html`.
2. Double-click it to open it in any modern browser (Chrome, Edge, Firefox, Safari).

That is all. An internet connection is only needed to load the Google Font. If it is offline, the site falls back to the system font and still works.

## How data is stored

Posts are saved in your browser's `localStorage`. This means:

- Posts stay after you close or refresh the page.
- Posts are visible **only in the same browser on the same device**. Other students will not see them.
- Clearing browser data removes all posts.

This is fine for a demo or a single shared computer, such as a notice-board kiosk. For a real campus-wide board, connect the site to a shared backend (see below).

## Customizing

All settings are in the same HTML file.

| What to change | Where |
| --- | --- |
| Item categories | The `CATS` array at the top of the `<script>` |
| Colors | The CSS variables in `:root` (`--blue`, `--lost`, `--found`, `--sun`) |
| Site name and headline | The `<header>` section and the `<title>` tag |
| Sample posts | The default list assigned to `items` in the script (delete them to start empty) |
| Storage key | The `KEY` constant, if you want to reset all saved data |

## Making it shared across students

To let every student see the same posts, replace the `load()` and `save()` functions with calls to a hosted database. Common free options:

- **Firebase** (Firestore)
- **Supabase** (Postgres with a ready-made API)

Posts would then be read from and written to the database instead of `localStorage`. The rest of the page can stay the same.

## Safety tips for users

- Meet in a public place on campus, such as the library or the main office, when handing over an item.
- Ask the owner to describe unique details of the item before returning it.
- Avoid posting sensitive details, such as full ID numbers, in the description.

## Project structure

```
college-lost-and-found.html   The complete website (HTML, CSS and JavaScript)
README.md                     This file
```

## Tech

Plain HTML, CSS and JavaScript. No frameworks or libraries. Font: Bricolage Grotesque (Google Fonts).
