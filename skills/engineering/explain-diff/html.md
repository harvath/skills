# Output format: self-contained HTML

One long page with section headers and a table of contents. No top-level tabs — it's a single continuous scroll. Basic responsive styling so it reads on a phone.

## Constraints

- **Single self-contained file.** Inline CSS and JS.
- **No external fonts, CDNs, images, iframes, or packages.** This is not just about working offline: a `file://` page can still make outbound requests, so any external reference is a channel for shipping the source code you just embedded in the page to someone else's server. Everything is inline or it doesn't ship.
- **Code blocks use `<pre><code>…</code></pre>`,** and the CSS for `pre` must explicitly set `white-space: pre` or `pre-wrap`. Without it the browser collapses every newline into one line. This is the single most common way this skill produces a broken page — check every block before saving.
- **Escape all code-derived text** for both HTML and JavaScript contexts.
- Keep the JS small, namespaced, dependency-free. Event listeners over inline handlers. Handle repeated quiz cards without fragile global selectors.
- Visible focus states, sufficient contrast, and correctness never signaled by color alone.

## Diagrams

Build them from semantic HTML and CSS — divs, lists, tables, borders, flexbox. Not ASCII, not images.

## Quiz mechanics

Clicking an option immediately reveals whether it was correct and explains why. Keep the answers and explanations in the page's JS data or DOM so it works with no network.

Reveal feedback only after selection, and don't leak the answer through pre-selection styling, DOM order, `title` attributes, class names, or accessibility text. Accessibility labels describe the option, not its correctness.

A deterministic per-page shuffle of the options is a good way to satisfy the position-balance rules in `SKILL.md`.

## Saving

Write to `/tmp/YYYY-MM-DD-explanation-<slug>.html` using today's date. The date prefix keeps files time-sorted; `/tmp` keeps the deliverable out of version control. Don't write it into the repo unless the user asks.

## Validate before handing off

- the file exists and is a complete HTML document
- no external asset references
- every code block's CSS preserves whitespace
- the quiz interactions work and the answer positions are balanced

Then return the absolute path as a clickable local-file link, plus a sentence on what you inspected and any assumptions or gaps.
