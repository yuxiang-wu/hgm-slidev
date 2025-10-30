# HGM Paper Presentation

Slidev presentation for the Huxley-Gödel Machine paper.

## Setup

Install dependencies:

```bash
npm install
```

## Running the Presentation

Start the dev server:

```bash
npm run dev
```

This will open the presentation in your browser at `http://localhost:3030`

## Navigation

- Use arrow keys (← →) or spacebar to navigate
- Press `f` for fullscreen
- Press `o` for overview mode
- Press `d` to toggle dark mode
- Press `g` to show slide numbers

## Building for Production

Build static HTML:

```bash
npm run build
```

The output will be in the `dist/` directory.

## Exporting to PDF

Export as PDF:

```bash
npm run export
```

This will create a `slides-export.pdf` file.

## Presentation Structure

1. Title & Introduction
2. Motivation & Problem Statement
3. Metaproductivity-Performance Mismatch
4. Background: Self-Improvement as Tree-Search
5. Gödel Machine Background
6. Key Concepts: GMP and CMP
7. Theorem 1
8. HGM Algorithm (3 policies)
9. Experimental Setup
10. Results (4 main result sections)
11. Interesting Discoveries
12. Key Contributions
13. Related Work
14. Limitations & Future Work
15. Key Takeaways

## Customization

Edit `slides.md` to modify the presentation content.

## Paper Reference

Wang, W., Piekos, P., Nanbo, L., Laakom, F., Chen, Y., Ostaszewski, M., Zhuge, M., & Schmidhuber, J. (2025).
Huxley-Gödel Machine: Human-Level Coding Agent Development by an Approximation of the Optimal Self-Improving Machine.
