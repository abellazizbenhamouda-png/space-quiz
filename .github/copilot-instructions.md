# Copilot instructions

## Project shape

Orbit Quest is a dependency-free static quiz implemented entirely in `index.html`. The document contains the semantic page structure, inline CSS, the question bank, and the browser-side quiz logic; there is no separate build pipeline or application runtime. Open the file directly in a browser to run it.

The script owns quiz state (`questionIndex`, `score`, and `answered`) and renders each question into the existing page. Selecting an answer locks the options, updates feedback, score, and progress, then enables the next action. Completing the last question replaces the quiz with a score-based results view; replay resets the state and restores the first question.

## Commands and checks

There are no package manifest, build, lint, or automated test commands in this repository. For a change, open `index.html` directly in a browser and exercise the affected interaction; the integrated browser can load the local file without a server.

## Code conventions

- Keep the app self-contained in `index.html`; there are currently no dependencies or module boundaries.
- Add quiz content to the `questions` array. Each entry has a `category`, `question`, `options` array, zero-based `answer` index, and explanatory `fact`. Keep answer indexes aligned with their options.
- Preserve the existing flow through `renderQuestion`, `selectAnswer`, `showResults`, and `restartQuiz`. `answered` prevents duplicate scoring; progress represents answered questions and advances only after a choice.
- Theme colors are CSS custom properties in `:root`, with their dark-theme counterparts in `@media (prefers-color-scheme: dark)`. Use these tokens for new UI states so both themes remain consistent.
- Retain the current accessibility patterns when changing interactions: native buttons, visible keyboard focus, focus movement between question/actions, an `aria-live` feedback/results region, and progressbar value updates. Hide decorative symbols from assistive technology and respect `prefers-reduced-motion`.
- Keep responsive adjustments in the existing narrow-screen media query and motion alternatives in the reduced-motion media query.
