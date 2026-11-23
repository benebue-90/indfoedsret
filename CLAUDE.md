# Indfødsret quiz

Quiz app for training the user's own mistakes from indfødsretstest.dk. It is a single `index.html` page and a `questions.js` data file, served on GitHub Pages (`benebue-90/indfoedsret`). The user opens it from their iPhone home screen. Progress and round history live in the phone's localStorage under key `indf-v1`, keyed by question `id`. Optional sync: each device stores a GitHub token (gist scope only) in localStorage key `indf-sync`, and the app merges its progress with a private gist file `indfoedsret-progress.json` when it opens and after each round. Runs are merged by timestamp, and for each question the most recent answer wins.

## Adding new screenshots (the recurring task)
1. The user saves iPhone screenshots in dated subfolders such as `screenshots/Nov 16 2026/`. These folders are the user's own backup, so never move, rename or delete them. `screenshots/` is gitignored and never pushed.
2. `screenshots/processed.txt` lists the filenames that are already done. Process only the files that are not in that list. The user may re-upload the same image (possibly under a new name or into a new folder), so also compare md5 hashes against already-processed files and skip exact duplicates. Deduplicate at question level too: if a question's text is already in `questions.js` from the same results page, don't count it again.
3. Make small copies in the scratchpad before reading them (`sips --resampleWidth 560`). Some screenshots have nothing to do with the quiz (for example ads), so skip those. A question can be cut off in one screenshot and complete in the next. Several screenshots from the same result page count as one miss, not several.
4. For each question, look in `questions.js` for the same question text:
   - If it is already there, increment `misses`. Never change its `id`.
   - If it is new, add an entry with a new stable kebab-case `id`, the exact question text, the options in A/B/C order, `correct` (0-based index of the right answer), `misses: 1`, and `explain` (the site's explanation text).
5. Validate the data with node (ids unique, `correct` in range). Append the new filenames to `processed.txt`, then commit and push.
6. Report how many questions are new, how many were repeats, and which images were skipped or unclear.

The weighting (Leitner boxes 0–4) lives in `index.html`. Svag (box 0–1) and På vej (box 2–3) are strongly prioritised; Sikker (box 4) and "Lært" (`streak >= 5`) questions are not asked at all (user's request, 2026-11-21 and 2026-11-23); they only fill in if fewer than 10 other questions remain; a wrong answer elsewhere isn't possible then, so it stays retired unless progress is reset.
