# PageRank vs Personalized PageRank — an interactive explainer

One random walk, three teleport vectors. This is a single-file interactive website that teaches the difference between **PageRank**, **Personalized PageRank (PPR)**, and **Topic-Sensitive PageRank** by letting you *watch* it: a random surfer walks a live graph, and the only thing that ever changes between the algorithms is **where the surfer teleports when it gets bored**.

**Live demo:** [https://mehrshaad.github.io/pagerank-vs-personalized-pagerank/](https://mehrshaad.github.io/pagerank-vs-personalized-pagerank/)

## What's inside

- **Live random-surfer simulation** — solid hops follow links, dashed arcs are teleports. Node size, color, and glow show the exact rank for the active mode. Click any node to personalize on it.
- **Three modes** — Global (uniform restart), Personalized (restart at one node), and Topic-set (restart in a set — i.e. Topic-Sensitive PageRank), plus a damping-factor slider, speed control, and pause.
- **Exact vs empirical** — per-node rank bars computed by power iteration, with a live gold tick showing the surfer's visit-frequency estimate converging onto the exact value (the stationary-distribution fact, made visible).
- **The math** — the shared fixed-point equation with the one differing teleport term highlighted, the matrix closed form, and the linearity property that makes Topic-Sensitive PageRank precomputable.
- **Convergence chart** — live log-scale L1 error of power iteration against the geometric `d^t` reference line; recomputed as you drag `d`.
- **Three algorithms** — power iteration, Monte Carlo (what the on-screen surfer runs), and Andersen–Chung–Lang forward push, each with pseudocode and when-to-use notes.
- **The wider family** — Topic-Sensitive PR, Random Walk with Restart, HITS, SimRank, Heat-Kernel PageRank, and PPR inside GNNs (APPNP / PPRGo), with a comparison table.
- **Applications** — recommenders, local community detection, graph neural networks, and entity-anchored retrieval for knowledge graphs / RAG.

Everything is computed live in the browser — nothing is precomputed or faked. No frameworks, no build step, no dependencies (fonts load from Google Fonts; everything else is inline).

## Run locally

Open `index.html` in a browser. That's it.

## Deploy to GitHub Pages

1. Create a repository and push these files (keep the main file named `index.html`).
2. Repo **Settings → Pages → Build and deployment**: Source = *Deploy from a branch*, Branch = `main`, folder = `/ (root)`.
3. Your site goes live at `https://<your-username>.github.io/<repo-name>/` within a minute or two.

## The graph

Nine nodes in two loosely connected communities (`A–D` and `F–H`) joined through bridge nodes `E` and `I` — chosen so that personalizing inside one cluster visibly starves the other. The math core is delimited by `[math-core]` markers in `index.html` so it can be extracted and unit-tested in Node without a DOM.

## Verified

The implementation was validated against an exact linear solve of `(I − dPᵀ)π = (1−d)e`:

- power iteration matches the exact solution to ~1e-16 (L1),
- scores sum to 1 for all modes and damping values,
- the Monte Carlo surfer's visit frequencies converge to the exact distribution,
- linearity in the teleport vector (`π_{αu+βw} = απ_u + βπ_w`) holds to machine precision,
- per-iteration error contraction is bounded by `d`, as the convergence chart claims.

## References

Page et al. 1999 (the PageRank tech report) · Haveliwala 2002 (Topic-Sensitive PageRank) · Jeh & Widom 2002/2003 (SimRank; Scaling Personalized Web Search) · Kleinberg 1999 (HITS) · Andersen, Chung & Lang 2006 (forward push / local clustering) · Gasteiger et al. 2019 ([APPNP, arXiv:1810.05997](https://arxiv.org/abs/1810.05997)) · Gleich 2015 ([PageRank Beyond the Web, arXiv:1407.5107](https://arxiv.org/abs/1407.5107)).

## License

MIT — fork it, remix it, teach with it.
