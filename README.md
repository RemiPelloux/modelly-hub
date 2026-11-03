# Modelly hub

The index of published [Modelly](https://github.com/RemiPelloux/Modelly) models:
`index.json`, served at <https://remipelloux.github.io/modelly-hub/index.json> and read by
`modelly hub`.

```bash
modelly hub search epidemic
modelly hub info within_host
modelly hub install within_host my_outbreak/
```

Every entry carries its model card (intended use, out-of-scope use, data, validation, known
limits, ethical considerations), the Modelly versions it supports, where its code is with its
sha256, and, for a published package, its Zenodo DOI and optionally a Sigstore signature. The
guide is [The model hub](https://remipelloux.github.io/Modelly/dev/hub.html).

## Adding a model

1. Give your project a `[tool.modelly.hub]` table (`target`, `field`), a model card stamped on
   its current source (`modelly card stamp card.toml`) and a wheel (`python -m build`).
2. `modelly hub publish . --zenodo --no-dry-run` archives it on Zenodo for a DOI (with
   `ZENODO_TOKEN` set) and writes `hub-entry.json`.
3. Open a pull request adding that entry to the `models` list of `index.json`.

The pull request is merged when `modelly hub check index.json` passes (run on every pull
request) and the entry follows these rules:

- the model runs on a supported Modelly and its validation tests pass on the source the card
  was stamped on;
- the card says honestly what the model is for and what it is not for;
- the name is unused, lower case, with digits and underscores only;
- every file the entry points to is archived (Zenodo) and its sha256 recorded.

The zoo models (`"kind": "zoo"`) are part of Modelly; their entries are regenerated with
`modelly hub zoo-index` at each release.
