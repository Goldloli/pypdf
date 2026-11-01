# Benchmark page

The page at <https://py-pdf.github.io/pypdf/dev/bench/> shows how fast pypdf is
after every commit to `main`.

## How it works

1. On every push to `main`,
   [benchmark.yaml](../../.github/workflows/benchmark.yaml) runs
   [tests/bench.py](../../tests/bench.py) with pytest-benchmark, once on
   CPython and once on PyPy.
2. [github-action-benchmark](https://github.com/benchmark-action/github-action-benchmark)
   appends the results to `gh-pages:dev/bench/data.js`.
3. After both runs, the `publish` job copies [index.html](index.html) to
   `gh-pages:dev/bench/index.html`, and commits and pushes it if it changed.
4. GitHub Pages serves the `gh-pages` branch. The page loads `data.js` and
   draws the charts in the browser with Chart.js.

## Changing the page

Edit [index.html](index.html) on `main` and open a PR as usual. Do not edit
`dev/bench/index.html` on `gh-pages` directly: the next benchmark run
overwrites it.

To try the page locally, download `data.js` next to it and serve the folder:

```bash
cd docs/benchmark-page
curl -O https://py-pdf.github.io/pypdf/dev/bench/data.js
python -m http.server
```

Then open <http://localhost:8000/>. Do not commit `data.js`.
