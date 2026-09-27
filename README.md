# Dutch Journey - Obsidian vault

Obsidian vault for learning Dutch, published as a website with [Quartz](https://quartz.jzhao.xyz) on GitHub Pages.
Site: `https://<username>.github.io/dutch-journey/`

## Structure

| Folder | Contents | Template |
| --- | --- | --- |
| `00 Inbox` | Quick capture; sort later | - |
| `01 Daily` | One note per study day | Daily |
| `02 Vocabulary` | One note per word (title = word, no article) | Word |
| `03 Verbs` | One note per verb (infinitive) | Verb |
| `04 Grammar` | One note per grammar topic | Grammar |
| `05 Phrases` | Expressions and sentences | Phrase |
| `06 Lessons` | Course / lesson notes | Lesson |
| `07 Practice` | Writing and speaking exercises | Writing |
| `08 Resources` | Apps, books, podcasts, videos | Resource |
| `99 Meta` | Templates and attachments (not published) | - |

Insert a template: command palette → **Templates: Insert template**. Daily note: **Daily notes: Open today's daily note**.

## Plugins

Core plugins (already enabled in `.obsidian/`): Templates, Daily notes, Backlinks, Graph view, Properties, Bookmarks, Outline.

Community plugins (Settings → Community plugins → Browse):

| Plugin | Why |
| --- | --- |
| **Git** (Vinzent03) | Auto commit + push every N minutes, so the website updates without a terminal. Also works on mobile. |
| **Spaced Repetition** | Review flashcards. Every Word/Verb/Phrase note has a `word::meaning` line under a `#flashcards` heading. |
| **LanguageTool** | Dutch spelling and grammar check while writing practice texts. |
| **Dataview** | Tables inside Obsidian, e.g. all `het` words or all irregular verbs. Queries show as code blocks on the website. |
| **Calendar** | Click through daily notes by date. |

Example Dataview query (all `het` words):

````
```dataview
TABLE plural, level FROM "02 Vocabulary" WHERE article = "het" SORT file.name
```
````

Optional later: Templater (if you want prompts or scripted templates).

## Publishing

The workflow in `.github/workflows/deploy.yml` builds the site on every push to `main`. It clones Quartz v4.5.2, copies the vault into Quartz `content/`, applies `.quartz/quartz.config.ts`, and deploys to GitHub Pages. Excluded from the site: `99 Meta`, `.obsidian`, this README, any folder named `private`, and notes with `draft: true` in their properties.

**The website is public.** Put anything personal in a `private` folder or set `draft: true`.

One-time setup:
1. Create an empty public repo named `dutch-journey` on github.com (no README).
2. Push this vault:
   ```bash
   git remote add origin https://github.com/<username>/dutch-journey.git
   git push -u origin main
   ```
3. Repo → Settings → Pages → Build and deployment → Source: **GitHub Actions**.
4. Repo → Actions → re-run the workflow if the first run failed before step 3.

Preview locally (optional, needs Node 22+):
```bash
git clone --depth 1 --branch v4.5.2 https://github.com/jackyzha0/quartz.git ../quartz
cd ../quartz && npm ci
cp -r ../Dutch/. content/ && cp ../Dutch/.quartz/quartz.config.ts .
npx quartz build --serve
```
