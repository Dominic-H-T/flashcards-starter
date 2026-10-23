# Flashcards

A tiny flashcard app for studying. Built live in class as a Claude Code demo.

## Tech conventions
- Everything lives in ONE file: `index.html`, with inline `<style>` and `<script>`.
- Plain JavaScript only. No frameworks, no libraries, no CDN links, no build step.
- Persist data in `localStorage` under the key `flashcards.v1`.
- A card is a plain object: `{ id, front, back }`. Add fields only when a feature needs them.
- Keep functions small and name them for what they do (`renderCard`, `markMissed`).

## How to run
- Open `index.html` directly in a browser. There is nothing to install.

## Working agreements
- Before changing code, give me a short plan (3-5 bullets).
- After a change, tell me exactly how to check it in the browser.
- Don't add features I didn't ask for. Suggest them instead.
