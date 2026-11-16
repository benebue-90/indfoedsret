# Indfødsret quiz

Quiz app for training the user's own mistakes from indfødsretstest.dk. It is a single `index.html` page and a `questions.js` data file, served on GitHub Pages (`benebue-90/indfoedsret`). The user opens it from their iPhone home screen. Progress and round history live in the phone's localStorage under key `indf-v1`, keyed by question `id`.

## Adding new screenshots (the recurring task)
1. New screenshots land in `screenshots/` (iPhone screenshots, gitignored, never pushed).
2. Read each one. A question can be cut off in one screenshot and complete in the next, so match them up.
3. For each question, look in `questions.js` for the same question text:
   - If it is already there, increment `misses`. Never change its `id`.
   - If it is new, add an entry with a new stable kebab-case `id`, the exact question text, the options in A/B/C order, `correct` (0-based index of the right answer), and `misses: 1`.
4. Move the processed images to `screenshots/done/`.
5. Commit and push. Report how many questions are new, how many were repeats, and any images that were unclear.

The weighting (Leitner boxes 0–4) lives in `index.html`. Every question keeps some weight, so questions the user has got right still come back now and then.
