# Ahwa Baladi — CSS 3D clickable flip cards

Task 1 of the Lime Light internship programme. A small landing page advertising a fictional
Egyptian coffee brand, built around three clickable 3D flip cards.

**Live site:** https://<your-github-username>.github.io/ahwa-flip-cards/

## The idea

Egyptian coffee is ordered by sweetness rather than by size, so the three tins are the three
standard orders — *sada* (no sugar), *mazbout* (one spoon), *ziyada* (two or three). The front of
each tin is the shelf label; clicking it turns the tin around to the tasting notes, specs and the
order button on the back.

## How the flip works

No JavaScript. Each card holds a visually hidden checkbox followed by the card body:

- `.tin` sets `perspective`, which creates the 3D space the rotation happens in.
- `.tin__body` gets `transform-style: preserve-3d` so its two children keep their own positions
  on the Z axis while the parent rotates.
- Both faces are absolutely positioned on top of each other with
  `backface-visibility: hidden`; the back face is pre-rotated `180deg` so it reads correctly once
  the card turns.
- The `<label>` inside each face points at the checkbox, so clicking anywhere on the button toggles
  it, and `.tin__switch:checked ~ .tin__body { transform: rotateY(180deg); }` does the flip.
- Only the face currently pointing at the reader keeps `pointer-events`, so the hidden face can
  never swallow a click.

Because the state lives in a real checkbox, the cards can also be flipped with the keyboard
(<kbd>Tab</kbd> to the card, <kbd>Space</kbd> to turn it), and `prefers-reduced-motion` shortens
the animation for anyone who asks the browser for less movement.

## SCSS

`scss/style.scss` is the source. It uses:

- a token block for the palette and timing,
- a `$blends` map holding the accent and seal colour of each tin,
- an `@each` loop that generates `.tin--sada`, `.tin--mazbout` and `.tin--ziyada` from that map,
- `@mixin face`, `@mixin foil-band` and `@mixin ring` for the repeated pieces,
- BEM-style nesting with `&`.

Build it with:

```bash
npm install -g sass
sass scss/style.scss css/style.css --no-source-map --style=expanded
```

The compiled `css/style.css` is committed so GitHub Pages can serve the site as-is.

## Structure

```
index.html
css/style.css     compiled output, linked by index.html
scss/style.scss   source
```
