# Diffing Tool

A browser-based text and code comparison tool that visualizes differences
between two pieces of text using two hand-implemented diffing algorithms.
Paste any text or code, pick an algorithm, and see additions, deletions,
and unchanged lines highlighted in real time.

Built as a Design and Analysis of Algorithms (DAA) course project to
demonstrate practical applications of classic algorithmic techniques.

## Contributors

- [@talal](https://github.com/talal-11)
- [@ahmed](https://github.com/Ah65med)
- [@neha](https://github.com/nehalq)
- [@shayan](https://github.com/sfxdeve)

## Overview

The tool takes two text inputs — an original and a modified version — and
computes a line-by-line diff. Results are displayed either side-by-side
or in a unified view, with color-coded lines and optional line numbers.
Two example presets (plain text and a code snippet) are included to demo
the tool instantly without any typing.

## Algorithms

Two diffing algorithms are implemented from scratch and selectable at runtime:

**Longest Common Subsequence (LCS)**
The default algorithm. Builds a 2D DP matrix over the lines of both inputs,
then backtracks through it to classify each line as added, deleted, or
unchanged. Produces the optimal (minimal) diff but uses O(m × n) time and
space, where m and n are the line counts of each input.

**Two Pointers**
A simpler linear scan that walks both inputs simultaneously using two index
pointers. At each mismatch it peeks one step ahead to decide whether a line
was inserted or deleted before advancing. Faster and lighter than LCS on
inputs with mostly sequential changes, but less accurate on complex
rearrangements.

Both algorithms implement the same `DiffAlgorithm` interface, making them
drop-in swappable in the UI.

## Features

- Real-time diffing with 500ms debounce as you type, or manual trigger mode
- Side-by-side view (desktop) and unified view (mobile and toggle)
- Automatically switches to unified view on screens narrower than 768px
- Optional line number display
- Algorithm selector — swap between LCS and Two Pointers without reloading
- Two built-in example presets: plain text and a JavaScript code snippet
- Color-coded output: green for added lines, red for deleted, neutral for unchanged

## Tech Stack

- **Framework:** Next.js 15 (App Router) with Turbopack
- **Language:** TypeScript
- **UI:** React 19, shadcn/ui, Radix UI primitives, Tailwind CSS v4
- **Icons:** Lucide React
- **Linting / Formatting:** Biome
- **Package Manager:** pnpm

## Getting Started

### Prerequisites

- Node.js 18+
- pnpm (`npm install -g pnpm`)

### Install and run

```bash
git clone <repository-url>
cd diffing-main
pnpm install
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### Other commands

```bash
pnpm build          # Production build
pnpm start          # Serve the production build
pnpm biome:safe     # Lint and auto-fix (safe transforms)
pnpm biome:unsafe   # Lint and auto-fix (including unsafe transforms)
```

## Project Structure
src/

├── app/

│   ├── page.tsx          # Main UI — inputs, settings, and layout

│   ├── layout.tsx        # Root layout

│   └── globals.css       # Global styles

├── components/

│   ├── diffing/

│   │   ├── DiffViewer.tsx      # Orchestrates diff display

│   │   ├── SideBySideView.tsx  # Two-column diff layout

│   │   ├── UnifiedView.tsx     # Single-column diff layout

│   │   └── DiffLine.tsx        # Individual line renderer

│   └── ui/               # shadcn/ui components

├── hooks/

│   └── useDiff.ts        # React hook — runs the selected algorithm reactively

└── lib/

└── algorithms/

├── lcs.ts          # LCS algorithm implementation

├── twoPointers.ts  # Two Pointers algorithm implementation

├── types.ts        # DiffAlgorithm, DiffLine, DiffResult interfaces

└── index.ts        # Exports and algorithm registry

## Algorithm Complexity

| Algorithm     | Time       | Space      | Best for                        |
|---------------|------------|------------|---------------------------------|
| LCS           | O(m × n)   | O(m × n)   | Optimal diffs, complex changes  |
| Two Pointers  | O(m + n)   | O(m + n)   | Sequential changes, speed       |
