# Replacing 3D models — assets/models/

This folder holds custom `.glb` 3D model files that any page on this
site can load instead of its built-in placeholder model — including
the homepage's hero model and lab cards, and every topic page.

## Where the swappable slots are

**Homepage (`index.html`)** — near the top of the big `<script>` block
at the bottom of the file, look for `MODEL_FILES`:

```js
const MODEL_FILES = {
  hero:     null, // e.g. "assets/models/hero.glb"      (front-screen atom)
  atom:     null, // e.g. "assets/models/atom.glb"       (Atom Explorer lab card)
  molecule: null, // e.g. "assets/models/molecule.glb"   (Molecule Builder lab card)
  dna:      null, // e.g. "assets/models/dna.glb"        (DNA Double Helix lab card)
};
```

Set any of these to a path in this folder and that model (including the
main front-screen hero model) loads your file instead of the built-in one.

**Topic pages** (built from `topic-template.html`) — near the top of the
page's `<script>` section:

```js
const MODEL_FILE = null; // e.g. "assets/models/electrostatics.glb"
```

## How it works everywhere

- If a `MODEL_FILE`/`MODEL_FILES` entry is `null`, that spot uses its
  built-in placeholder model (plain Three.js code written directly in
  the page).
- If it points to a `.glb` file in this folder, the page loads that
  file instead — no other code changes needed.
- If the file is missing or fails to load, it automatically falls back
  to the placeholder model, so a bad file never breaks the page.
- On the homepage, when a custom model replaces the Atom Explorer or
  Molecule Builder lab card, that card's element/molecule switcher
  buttons are automatically hidden, since they only apply to the
  built-in models. The DNA speed buttons keep working regardless, since
  they just control rotation speed.

## Replacing a model yourself

1. Get a `.glb` file. You can:
   - Download one from a site like Sketchfab (look for CC0 / free-to-use models)
   - Export one from Blender (`File → Export → glTF 2.0 → .glb`)
   - Have someone build one for you — `.glb` is the standard format for this
2. Name it clearly, e.g. `hero.glb`, `electrostatics.glb`, `benzene-ring.glb`
3. Drop it into this folder
4. Open the relevant page's HTML file, find the matching config line
   above, and point it at `"assets/models/your-file-name.glb"`
5. Re-upload/redeploy the site

To update a model later, just replace the file with a new one of the
same name — you don't need to touch any code.

## Keeping file sizes reasonable

Aim for under 5–10MB per model so it loads quickly on school devices.
Tools like [gltf-transform](https://gltf-transform.dev) or Blender's
export compression options can shrink files significantly.

