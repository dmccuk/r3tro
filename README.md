# r3tro.io

Simple, addictive arcade games you can play in seconds. Free, no sign-up. Every game is built with AI, in public.

See [SPEC.md](SPEC.md) for the full product plan.

## What's in this repo

```
r3tro/
├── index.html                  Homepage (arcade menu)
├── games/
│   └── shardfield/index.html   Game 1: vector rock shooter
├── quiz/
│   ├── index.html              Skill test engine (runs any question bank)
│   └── questions/linux.js      Linux command line questions (48)
├── CNAME                       Custom domain for GitHub Pages (r3tro.io)
├── .nojekyll                   Tells GitHub Pages to serve files as-is
├── README.md
└── SPEC.md
```

Every page is a single self-contained HTML file. There is no build step, no framework and nothing to install.

## Run it locally

Double-click `index.html` to open it in a browser. For a setup closer to the live site, run a tiny local server from the repo folder:

```
python3 -m http.server 8000
```

Then open http://localhost:8000.

## Put it online with GitHub Pages (free)

1. Create a new **public** repository on GitHub, for example `r3tro`.
2. Upload every file in this folder to the repo (drag and drop works on the GitHub website). Make sure `index.html` sits at the top level, not inside a subfolder.
3. In the repo, go to **Settings → Pages**. Under "Build and deployment", choose **Deploy from a branch**, pick `main` and `/ (root)`, then save.
4. After a minute or two, the site is live at `https://YOUR-USERNAME.github.io/r3tro/`.

## Connect r3tro.io

1. In **Settings → Pages → Custom domain**, enter `r3tro.io` and save. (The `CNAME` file in this repo already contains it.)
2. At your domain registrar, add these DNS records:

   | Type  | Name | Value                    |
   |-------|------|--------------------------|
   | A     | @    | 185.199.108.153          |
   | A     | @    | 185.199.109.153          |
   | A     | @    | 185.199.110.153          |
   | A     | @    | 185.199.111.153          |
   | CNAME | www  | YOUR-USERNAME.github.io  |

3. DNS can take up to a day to update. Once GitHub shows the domain as verified, tick **Enforce HTTPS**.

GitHub occasionally updates these addresses, so double-check them against GitHub's "Managing a custom domain for your GitHub Pages site" docs before you add them.

## Before you launch

- Replace the `#` placeholder links in `index.html` with your TikTok, Instagram, YouTube and tip jar links (search the file for `TODO`).
- Play Shardfield on your phone and a computer to make sure controls feel right.

## Adding a new game

1. Create a folder: `games/your-game-name/index.html`.
2. Make sure it meets the game checklist in SPEC.md section 4.
3. In the homepage `index.html`, copy the Shardfield `<li class="game">` block, then change the link, icon, title and description.
4. Commit. GitHub Pages redeploys automatically.

## Adding a skill test

The quiz engine in `quiz/index.html` runs any question bank. The URL picks the bank: `quiz/?t=linux` loads `quiz/questions/linux.js`.

1. Copy `quiz/questions/linux.js` to a new file, for example `quiz/questions/ansible.js`.
2. Change the last part of `window.R3TRO_BANKS.linux` to match the file name (`window.R3TRO_BANKS.ansible`), then update `title`, `short` and `blurb`.
3. Replace the questions. Each one needs `level` (`junior`, `mid` or `senior`), `q`, optional `code`, four `options`, `answer` (the index of the correct option, starting at 0) and `explain`. Options are shuffled when the test runs.
4. Aim for at least 15 questions per level. Each run picks 10 at random, so a bigger bank keeps repeat runs fresh.
5. Copy the Linux row in the homepage's "skill tests" list and change `?t=linux` to your new topic.

Test names may only use lowercase letters, numbers and hyphens.

This is a great place to accept contributions from viewers: they can open a pull request that adds questions to a bank.
