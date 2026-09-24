# Economics Flashcards

A responsive flashcards website for GitHub Pages, with Decks and Study navigation, answer reveal, shuffle, keyboard shortcuts, and another round for missed cards. Includes six decks and 24 original sample Economics cards. There is no Notes section.

Progress lasts for the current page session and resets on refresh. Cards are edited in the repository; there is no sign-in or online card editor.

## Publish on GitHub Pages

1. Extract this ZIP on your computer.
2. Create a GitHub repository, for example `economics-flashcards`. A public repository works with GitHub Free. For a website at your account's root address, name the repository `YOUR-USERNAME.github.io` instead.
3. Upload the **contents** of the extracted folder into the repository root. `mkdocs.yml`, `README.md`, `docs/`, `theme/`, and `.github/` must be directly inside the repository, not inside an extra enclosing folder. Commit to `main`.
4. Confirm `.github/workflows/pages.yml` appears in the repository. If your file picker hid `.github`, use **Add file → Create new file**, enter `.github/workflows/pages.yml`, and paste the supplied file's contents.
5. Open **Settings → Pages → Build and deployment → Source**, then select **GitHub Actions**. The workflow is already supplied; you do not need to add a suggested template.
6. Open **Actions → Publish Economics Flashcards → Run workflow**, choose `main`, and run it. If an earlier run failed before Pages was enabled, rerun it now.
7. Once both jobs succeed, open the website link in **Settings → Pages** or the deployment run. For a repository called `economics-flashcards`, it is normally `https://YOUR-USERNAME.github.io/economics-flashcards/`.

Later commits to the default branch (`main` or `master`) automatically rebuild and publish your cards. If your default branch has another name, update the `branches` list in `.github/workflows/pages.yml`.

The workflow supplies the correct website URL during the build, supporting both account sites and repository subfolder sites.

## Edit cards

Edit `docs/assets/flashcards.json`. Each card has a unique `id`, an existing topic ID, a question, and an answer:

```json
{
  "id": "price-005",
  "topic": "price-mechanism",
  "question": "What is a shortage?",
  "answer": "A shortage occurs when quantity demanded exceeds quantity supplied at the current price.\nThis creates upward pressure on price."
}
```

The file is an array: keep the surrounding square brackets and put commas between card objects, but no comma after the last one. Questions and answers are plain text; use `\n` for line breaks and `\"` for quotation marks inside text. Markdown and HTML are not rendered in card text.

Commit the changes. GitHub Actions validates the file, rebuilds the page, and publishes the update. Duplicate card IDs, unknown topics, and missing card fields fail the build with a message in the Actions log.

## Add or rename decks

Edit `extra.topics` in `mkdocs.yml`:

```yaml
- id: international-trade
  title: International trade
  group: Macroeconomics
  description: Trade, exchange rates, and economic integration.
```

Add cards whose `topic` is `international-trade`. Decks and counts are generated automatically. Keep topic IDs unique. To rename a deck, change its `title`; changing its `id` also requires updating all corresponding card topics.

## Study controls

- Choose a deck from **Decks** or the desktop sidebar.
- Select **Reveal answer**, then **Review again** or **I knew it**.
- At the end, review remaining cards or start again.
- Turn on **Shuffle** to reorder remaining cards.
- Keyboard: **Space** reveals an answer, **1** marks it for review, **2** marks it remembered.

## Build locally (optional)

GitHub builds the site for you; Python is only needed if you want to preview edits locally.

```bash
python -m pip install -r requirements.txt
python -m mkdocs serve
```

Open the local address printed by MkDocs. To generate the static website:

```bash
python -m mkdocs build --strict
```

The output is in `site/`. An optional Vite preview is available with `npm ci` then `npm run dev`, after building with MkDocs. Node is not required for GitHub deployment.

## Files

- `theme/flashcards-app.html`: interface, styling, and interactions.
- `theme/main.html`: HTML document and metadata.
- `docs/assets/flashcards.json`: questions and answers.
- `mkdocs.yml`: deck metadata and build configuration.
- `hooks.py`: card validation and template data.
- `.github/workflows/pages.yml`: automatic GitHub Pages publishing.

## If publishing fails

- **Pages not configured:** select GitHub Actions as the Pages source, then rerun the workflow.
- **Workflow missing:** check that `.github/workflows/pages.yml` was uploaded, rather than just the ZIP file.
- **Cannot find requirements or config:** move the extracted files into the repository root.
- **Card validation failed:** fix the indicated JSON syntax, duplicate ID, missing field, or unknown topic, then commit again.

The package was built locally with strict validation. It has not been deployed to a GitHub account yet.

Official setup references: [publishing source](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site) and [custom Pages workflows](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages).
