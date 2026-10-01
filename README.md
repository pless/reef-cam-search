# Roatán reef cam search

Text search over viewer-captioned snapshots from two fixed underwater cameras at Utopia Village, Roatán (the explore.org coral cam and dock cam), answered three ways: a frozen SigLIP2 model, two linear maps fitted to each camera's captions, and the same two maps applied over sets of query phrases and image patches. Everything runs in the browser.

Page: https://pless.github.io/reef-cam-search/

## What is here
- `index.html`: the page.
- `data/<cam>/`: per camera, `meta.json` (for each snapshot: explore.org thumbnail and snapshot URLs, the viewer's caption, local time, and whether the frame was in the training split), int8 image embeddings for the three models, int8 patch embeddings for the set model, and the text-side maps.
- `model/`: the SigLIP2 base/16-256 text tower (Google, Apache 2.0) repackaged for browsers: int8 token table, float16 weights, float32 arithmetic.

No images are stored here. Thumbnails load from explore.org and each result links to the original snapshot. Snapshots and captions belong to explore.org and the viewers who wrote them, and are used here with explore.org's permission; viewer names are not included. Contact robert.pless@gmail.com to have anything removed.

## Numbers (held-out test frames, caption as the query, R@10 / R@50)
| camera | frozen | two maps | two maps over sets |
|---|---|---|---|
| coral cam (983 frames) | 0.06 / 0.18 | 0.23 / 0.49 | 0.24 / 0.53 |
| dock cam (954 frames) | 0.05 / 0.19 | 0.26 / 0.59 | 0.29 / 0.60 |

These are the full-precision models. Measured inside the browser on the dock cam, the page gives 0.06 / 0.20, 0.26 / 0.59 and 0.29 / 0.60.
