# Glyph Atelier

Transcribing paintings into code. Upload a painting and the browser redraws it as letters, as halftone dots or as thousands of brush strokes, and can even play it as music.

**Live app:** _add your GitHub Pages link here_

## Why I built this
I'm a medical student learning to code. Medicine is full of images that are really data: X-rays, dermatoscopy photos, histology slides. Before training models on them, I wanted to understand at the pixel level what an image actually is to a computer. Transcribing paintings was the most enjoyable way to learn that.

## Three ways to transcribe a painting

| Style | Idea | Technique |
|---|---|---|
| **Glyphs** | Every patch of the painting becomes one character, heavier where it needs more ink. Your own text can be woven through it. | Downsampling, luminance, mapping values to a character ramp |
| **Halftone** | Like newspaper printing: a honeycomb of dots, bigger where it's darker. | Hexagonal grid, area-proportional radius (√) |
| **Strokes** | The painting is repainted with short strokes that follow its edges and forms. | Sobel edge filter, gradient direction rotated by 90°, layered rendering |

Plus:
- **Listen to the painting:** a playhead scans left to right. Height becomes pitch (pentatonic scale), brightness becomes volume, and warm colours open up the tone. Built with the Web Audio API.
- **Animate:** glyphs shimmer and ripple, dots pulse and strokes sway.
- **Hold to see original**, **Copy as text** (the glyph picture as plain text) and **Export image**.

## How it's built
Plain HTML, CSS and JavaScript on a `<canvas>`. No libraries, no build step.

```
index.html      page structure
style.css       design, named after pigments (Payne's grey, ultramarine, cadmium)
transcribe.js   the three styles: sample → map → draw
sound.js        sonification with the Web Audio API
sample.js       a painting generated with code, used until you upload your own
app.js          controls, animation loop, upload, export
```

Every style follows the same three steps:
1. **Sample:** shrink the image to a small grid so the browser averages each cell's colour.
2. **Map:** turn each cell's brightness into something: a letter, a dot size, a stroke direction.
3. **Draw:** paint the result onto the canvas.

## What I learned
- An image is a grid of numbers, and brightness is a weighted sum of red, green and blue (0.21 R + 0.72 G + 0.07 B).
- Edges are where those numbers change fast. The Sobel filter is the same idea that sits at the start of image-analysis pipelines in radiology.
- Seeded random numbers make "random" art reproducible.
- Animation means redrawing about 60 times a second from the same data.

## Run it locally
Open `index.html` in a browser. Your images never leave your computer.

## Next ideas
- Audio in → visuals out (draw a waveform or spectrogram live from the microphone)
- Export the animation as a video
- Apply the edge filter to a public medical image dataset

## Author
Joanna (Asiek) Farnicka, medical student and doctoral researcher, Charité – Universitätsmedizin Berlin.
