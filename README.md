# Everyone's a 4.8

An interactive drop about trust signals in hiring. AI now writes the resumes and AI reads them, so hiring leans harder on who will vouch for you. The rating systems people have built for that job tend to drift toward the top of their scales, where they tell fewer and fewer people apart. The drop measures that drift, explains the forces behind it, and lets you run a simulated company of 80 coworkers to see which rules keep a vouch worth something.

By [Brian Grover](https://www.linkedin.com/in/briantgrover) ([@briantgrover](https://x.com/briantgrover)), October 2026. It makes the case for Vouched, a concept that replaces the resume with two kinds of proof: challenges, where the work itself is scored, and blind vouches from people you actually worked with, counted by each voucher's track record. Vouched is shown here as a concept.

## What's on the page

Six full-screen scenes under a fixed frame: the title and the page's own rating at the top, a counter with dots at the bottom. One scroll, swipe or arrow key moves one scene, and each scene's line hands off to the next.

1. **Everyone's a 4.8.** We rate everything now, and approval that costs nothing turns into a commodity that can't tell anyone apart.
2. **It's the same everywhere.** Harvard grades, eBay sellers, LinkedIn endorsements, GitHub stars and Airbnb listings, each a grid of 100 stars that fills as the scene arrives, all crowded at the top; hotels, rated as businesses, are the exception.
3. **One example up close.** Drag the star to guess the typical Airbnb rating in San Francisco and New York. The big number counts to the answer from our own measurement of this year's data, 4.84, as every listing rises from the slider's track.
4. **The comparison.** The same 80 simulated coworkers rate each other under two sets of rules at once, on two charts that share one axis: one-click likes above, praise tied to real work below. Each chart counts how many of the 10 most skilled it finds and how many people end up rated 4.8 or higher, and one sentence states both when the run ends. A "How this works" strip gives the model in three plain steps; on a phone it starts folded.
5. **Which rules find the best people?** In our simulation, one bar for each set of rules, best first: Vouched-style rules (about 8 of the 10 most skilled), tied to real work (about 6), hidden reviews, written reviews and saying how you know someone (about 5), one-click likes (about 5) and LinkedIn-style endorsements (about 2), each averaged over 12 simulated companies, with a line where guessing lands. A tap on a bar reruns the lower chart under those rules, with one plain line on what they find and what they cost, and a line under the bars says the numbers are simulated, not measured.
6. **What this means for Vouched.** Most ratings count every vote the same; people don't. Weighing approval by who gave it and how much care went into it keeps it from turning into a commodity. Vouched is a concept built on two kinds of proof: challenges, where the work itself is scored, and blind vouches from people you actually worked with.

Scenes 2, 4 and 6 each have a "Why?" that opens a few sentences of evidence, with sources, in a frosted card over the scene's text. The page's rating climbs from 3.0 to 5.0 as you go, and the last scene says so. `methods.html` holds the rest behind a short summary, in four parts that open on request: the data, the lab's rules, the research, and the sources.

## Data and sources

- `research/airbnb_measure.py` downloads Inside Airbnb's detailed listings for San Francisco and New York City (snapshot of 14 June 2026) and writes the rating distribution to `data/airbnb.json`. Inside Airbnb data is licensed [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/); credit to [Inside Airbnb](https://insideairbnb.com/).
- `research/sources.md` lists every number the page uses, the primary source it came from, and the ones that were cut.
- `data/figures.json` holds the numbers drawn in the charts, each traceable to the ledger. Its `rules` block is scene 5's bars; `node tools/lab-check.mjs` fails if any of them drifts from the model.

## How it was built

Built with [Claude Code](https://claude.com/claude-code). Research agents traced every number to its primary source, other agents built the lab and the charts, six specialist agents reviewed the design, motion, scrolling, accessibility, layout and loading, and a fresh reviewer checked the finished page against the sources. The full conversation is in `TRANSCRIPT.md`.

The page is static HTML, CSS and JavaScript with no framework, no build step, no cookies and no tracking.

- `index.html`: the six scenes and all their copy; `methods.html`: the notes, research and methods
- `css/style.css`: the design system (paper, ink and gold, the two type roles, the one motion curve, the grain); `css/stage.css` for the scenes and the frame; `css/charts.css` and `css/lab.css` for the interactive parts; `css/methods.css` for the notes page
- `js/stage.js`: the scenes, the frame, the "Why?" cards and the inputs that move between scenes
- `js/motion.js`: the page's one easing curve and timings, for scripts
- `js/charts.js`: the guess, the drift grids, and the two charts on the notes page
- `js/lab-model.js`: the trust lab's model, with no DOM code, so it runs in Node too; `js/lab.js` draws it, and `node tools/lab-check.mjs` checks the claims the page makes about it
- `js/methods.js`: the blind-reveal cards on the notes page
- `js/stars.js`: the star used everywhere
- `tools/`: the share card and icon templates, the script that renders them, and the lab check

## Run it locally

```sh
python3 -m http.server 8800
```

Then open http://localhost:8800. The page needs a server (not a `file://` URL) because it loads JSON and JavaScript modules.

To re-measure the Airbnb data:

```sh
python3 research/airbnb_measure.py
```

## Credits

Airbnb data is from Inside Airbnb under CC BY 4.0. Fonts are Newsreader (Production Type) and IBM Plex Mono (IBM), both under the SIL Open Font License.
