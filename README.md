# Inspired Art Dataset

Ground-truth data for **region-level attribution**: which part of a generated
image was inspired by which public-domain artwork.

10 images were generated with FLUX.1-dev from prompts that each reference
several artworks. For every artwork that visibly appears in a scene, human
annotators recorded the rectangle where it appears (`scene_x/y/w/h`) and the
rectangle of the source artwork that was reused (`source_x/y/w/h`).

## Layout

| Path | Contents |
|---|---|
| `scenes.csv` | One row per generated scene: prompt, source artworks, model, seed, request id, cost |
| `scenes/sceneNNNN.png` | Generated images (1024x1024) |
| `sources.csv` | One row per source artwork: title, artist, era, source URL |
| `sources/artNNNN_*.jpg` | Source artwork images (public domain, from Wikimedia Commons) |
| `attribution.csv` | One row per (scene, source artwork) pair: presence + both rectangles |
| `attribution/sceneNNNN.png` | Same generated image with the attribution rectangles drawn and labeled |

## Coordinates

- All boxes are `[x, y, w, h]` in pixels.
- `scene_*` boxes are in the 1024x1024 generated image.
- `source_*` boxes are in the source artwork's own pixel space.
- `present` is `true` when the artwork actually appears in the scene; only
  those rows carry `scene_*` coordinates.
- `source_id` (`artNNNN`) is a stable global identifier; the same artwork gets
  the same id across scenes.

## Provenance

Images were generated with `black-forest-labs/flux-1-dev` (RunPod), seeds
1000–1009. Source artworks are public-domain works retrieved from Wikimedia
Commons; the exact URL for each is in `sources.csv`.
