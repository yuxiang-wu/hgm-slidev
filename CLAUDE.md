# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Slidev presentation** for the Huxley-Gödel Machine (HGM) paper from KAUST, 2025. Slidev is a presentation framework that uses markdown to create slides with interactive features, code highlighting, and animations.

## Key Commands

### Development
```bash
# Install dependencies
npm install

# Start development server (opens at http://localhost:3030)
npm run dev

# Build for production (output to dist/)
npm run build

# Export to PDF
npm run export
```

## Project Structure

- **slides.md** - Main presentation content. All slide content is defined here using markdown with frontmatter configuration
- **HGM.md** - The actual research paper markdown file (reference material, not part of presentation)
- **public/images/** - Static assets including title-figure.jpg and figure1-main-results.jpg
- **package.json** - Uses @slidev/cli and @slidev/theme-default
- **README.md** - Project documentation with presentation structure outline

## Slidev-Specific Architecture

### Slide Format
- Slides are separated by `---` in slides.md
- Frontmatter at the top defines theme, transitions, and metadata
- Supports Vue components, Mermaid diagrams, and v-click animations
- Uses Tailwind CSS for styling (utility classes like `grid`, `flex`, `text-center`)

### Layout System
The presentation uses built-in Slidev layouts:
- `default` - Standard content layout
- `center` - Centered content (used for main results figure)
- Custom layouts with grid systems for multi-column content

### Special Features Used
- **v-click** - Progressive content reveal animations
- **Mermaid diagrams** - Flowcharts showing agent trees and evolution
- **Grid layouts** - `grid grid-cols-2` and `grid grid-cols-3` for structured content
- **Gradient backgrounds** - Color-coded sections (blue, green, purple, yellow themes)
- **Image embedding** - Local images from `/images/` directory

## Content Themes

The presentation follows a color coding scheme:
- **Red/Orange** - Problems and challenges
- **Blue** - Gödel Machine and theoretical concepts
- **Green** - Solutions, results, and improvements
- **Purple** - Advanced concepts (CMP, self-improvement)
- **Yellow** - Key insights and takeaways

## Development Notes

- The presentation is currently configured for `auto` color schema (supports both light and dark modes)
- Default theme is used; customization happens through Tailwind utility classes
- Images are stored locally in public/images/ and referenced with `/images/` paths
- The presentation includes mathematical formulas (would need KaTeX support if editing)
