# Open Issues: College Lost and Found

Welcome, contributors! This file lists tasks you can pick up. Each issue has a label, a difficulty level, what to do, and how we will know it is done.

The whole site lives in one file, `college-lost-and-found.html` (HTML, CSS and JavaScript). No build tools are needed. Open the file in a browser to test.

## How to pick up an issue

1. Comment on the issue (or tell your mentor) that you are taking it, so two people don't do the same work.
2. Fork the repository and create a branch named `issue-<number>-short-name`, for example `issue-1-local-date`.
3. Make the change. Keep it small and focused on one issue.
4. Test it manually in at least two browsers and on a phone-sized screen.
5. Open a pull request. Mention the issue number, describe what changed, and add a screenshot for visual changes.

**Difficulty levels:** 🟢 Beginner · 🟡 Intermediate · 🔴 Advanced

---

## 🟢 Beginner issues (good first issue)

### #1 Default date is wrong in some time zones
**Labels:** `bug`, `good first issue`

**Problem:** The `day()` helper uses `toISOString()`, which returns the UTC date. In India (UTC+5:30), between midnight and about 5:30 AM, the form's default date and the date picker's maximum show yesterday. Students cannot select today.

**What to do:** Change `day()` so it builds the date from the user's local time (`getFullYear()`, `getMonth()`, `getDate()`) and formats it as `YYYY-MM-DD`.

**Done when:**
- The default date and the `max` date in the form match the local date at any time of day.
- Sample posts still show correct "days ago" dates.

---

### #2 Whitespace-only text passes validation
**Labels:** `bug`, `good first issue`

**Problem:** Fields marked `required` accept a string of spaces. After submit the values are trimmed, so a post can be created with an empty name, place or contact.

**What to do:** Before saving, check the trimmed values. If a required field is empty, stop the submit and show a short message under that field (do not use `alert`).

**Done when:**
- Typing only spaces in Item name, Place, Your name or Contact blocks the post and shows a clear message.
- Valid posts still save normally.

---

### #3 Copy contact fails silently
**Labels:** `bug`, `good first issue`

**Problem:** After clicking "Show contact" and clicking again, the code calls `navigator.clipboard.writeText`. If the browser blocks it (common when the file is opened from disk), nothing happens and the user gets no feedback.

**What to do:** Show a toast such as "Couldn't copy. Please copy it manually." when the copy fails. Optionally select the text so the user can copy it by hand.

**Done when:**
- A success toast appears when copying works.
- A failure toast appears when copying is blocked.

---

### #4 Fix the sample post text
**Labels:** `content`, `good first issue`

**Problem:** The "Student ID card" sample post has the description "Name starts with S. Handed over to the front desk? No, I have it." This is a drafting slip and reads oddly.

**What to do:** Reword it to something clear, such as "Name starts with S. I am holding it and can hand it over."

**Done when:** All four sample posts read naturally and have no leftover drafting text.

---

### #5 New post can be hidden by active filters
**Labels:** `bug`, `good first issue`

**Problem:** After a student posts an item, the site switches to the matching Lost or Found tab but keeps any search text or category filter. The new post may not appear, which looks like the post failed.

**What to do:** In the submit handler, clear the search box and reset the category filter to "All categories" before calling `render()`.

**Done when:** A newly posted item is always visible right after posting.

---

### #6 Improve badge text contrast
**Labels:** `accessibility`, `good first issue`

**Problem:** White text on the coral (`--lost`) and green (`--found`) badges is below the WCAG AA contrast ratio (4.5:1) for small text.

**What to do:** Darken the badge background colors or switch the text color so each badge reaches at least 4.5:1. Check with a tool such as the WebAIM contrast checker.

**Done when:** All badge, button and tab text combinations pass WCAG AA. Include the contrast values in your pull request.

---

### #7 Tag overlaps the headline on tablets
**Labels:** `bug`, `ui`, `good first issue`

**Problem:** The yellow hero tag is hidden below 700px width but may overlap the headline between roughly 700px and 900px.

**What to do:** Test at 700, 768, 820 and 900px. Adjust the breakpoint, the tag's size, or its position so it never covers text.

**Done when:** No overlap at any width from 320px to 1920px. Add before and after screenshots.

---

### #8 Add a footer link and "How it works" section
**Labels:** `enhancement`, `content`, `good first issue`

**What to do:** Add a short three-line section under the header that explains the flow: post it, check the board, meet safely. Keep the existing design style. Use plain language and no numbered markers unless the content is a real sequence.

**Done when:** The section is responsive and readable on a phone, and it does not push the item list too far down the page.

---

## 🟡 Intermediate issues

### #9 Dialog closes and loses typed text on outside click
**Labels:** `bug`, `ux`

**Problem:** Clicking the backdrop closes the form and discards everything typed. This can happen by accident, for example when a text selection ends outside the dialog.

**What to do:** Only close on backdrop click if the form is empty, or ask for confirmation when it has content. Make sure pressing Escape follows the same rule.

**Done when:** Users never lose a filled-in form without a confirmation.

---

### #10 Add a fallback for browsers without `<dialog>`
**Labels:** `compatibility`

**Problem:** Safari earlier than 15.4 and other old browsers do not support `<dialog>`, so the Post buttons do nothing.

**What to do:** Detect `typeof dlg.showModal !== "function"` and use a simple fallback, such as showing the dialog as a fixed overlay with a class toggle.

**Done when:** The form opens, submits and closes in a browser without `<dialog>` support (test with the dialog polyfill disabled or an old browser).

---

### #11 Edit an existing post
**Labels:** `enhancement`

**What to do:** Add an "Edit" button to each card. Reuse the existing form, pre-filled with the post's values. Saving updates the post instead of creating a new one.

**Done when:**
- Edit opens the form with the current values.
- Saving updates the card without changing its id or type.
- Cancel leaves the post unchanged.

---

### #12 Sort options and "Resolved" filter
**Labels:** `enhancement`

**What to do:** Add a sort control (Newest first, Oldest first) and a toggle to hide or show resolved posts. Remember the choice for the session.

**Done when:** Sorting and the toggle work together with the existing tabs, search and category filter.

---

### #13 Dark mode
**Labels:** `enhancement`, `ui`

**What to do:** Add a dark theme using CSS variables and `prefers-color-scheme: dark`, plus a manual toggle that saves the choice.

**Done when:** Every element is readable in both themes and passes contrast checks.

---

### #14 Export and import posts as a JSON file
**Labels:** `enhancement`

**Why:** Posts live only in one browser. Export and import lets a volunteer move the board to another computer or keep a backup.

**What to do:** Add "Export" (downloads `lost-and-found.json`) and "Import" (reads a JSON file, validates it, and merges posts without duplicates).

**Done when:** An exported file imports cleanly into a fresh browser, and invalid files show a clear error without breaking existing data.

---

### #15 Automated "possible match" hints
**Labels:** `enhancement`

**What to do:** When viewing a lost item, show a small "Possible match" note if a found item has the same category and shares keywords in its name or description (and the reverse). Keep the scoring simple and explain it in code comments.

**Done when:** Matches appear on both the lost and found cards, and unrelated items are not flagged in the sample data.

---

## 🔴 Advanced issues

### #16 Shared backend so all students see the same posts
**Labels:** `enhancement`, `backend`, `help wanted`

**Problem:** Data is stored in `localStorage`, so other students never see a post. This is the biggest limitation of the project.

**What to do:** Replace `load()` and `save()` with calls to a hosted database such as Firebase Firestore or Supabase. Keep the UI the same. Document setup steps in the README, and never commit secret keys.

**Done when:**
- A post created on one device appears on another device.
- The site still shows a friendly message if the backend is unreachable.

---

### #17 Student login and post ownership
**Labels:** `enhancement`, `security`, depends on #16

**Problem:** Anyone can delete any post.

**What to do:** Add sign-in (for example, college email only). Only the post's author can edit, delete, or mark it resolved. Enforce this with database rules, not only in the UI.

**Done when:** A user cannot change another user's post, even by calling the database directly.

---

### #18 Photo upload for items
**Labels:** `enhancement`, depends on #16

**What to do:** Allow one optional photo per post. Resize it in the browser before upload (for example, max 800px), accept only images, and limit the file size.

**Done when:** Photos show on cards, load lazily, and have alt text based on the item name.

---

### #19 Moderation: report a post and auto-expire old posts
**Labels:** `enhancement`, `safety`, depends on #16

**What to do:** Add a "Report" button that flags a post for an admin. Archive posts older than 60 days automatically.

**Done when:** Reported posts are hidden after a set number of reports, and admins can review them.

---

### #20 Automated tests and CI
**Labels:** `testing`, `tooling`

**What to do:** Move the pure logic (filtering, sorting, date helper, matching) into testable functions. Add tests with a simple framework (Vitest or Jest) and a GitHub Actions workflow that runs them on every pull request.

**Done when:** The workflow passes on the main branch and fails when a test breaks.

---

## Labels reference

| Label | Meaning |
| --- | --- |
| `good first issue` | Small, clear task for newcomers |
| `bug` | Something is not working as expected |
| `enhancement` | New feature or improvement |
| `accessibility` | Helps users with disabilities |
| `ui` / `ux` | Visual design or user experience |
| `compatibility` | Browser or device support |
| `backend` / `security` | Needs server-side or access-control work |
| `help wanted` | Maintainers would especially like help |

## Code of conduct

Be kind and patient. Ask questions early. Review each other's work with helpful comments. Everyone here is learning.
