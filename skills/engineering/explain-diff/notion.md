# Output format: Notion page

Use the Notion MCP tools to create a new page. If those tools aren't available, stop and offer the HTML format instead.

Ask where it should live if the parent page is ambiguous and you can't infer it from the workspace.

## Constraints

- Native Notion blocks throughout — headings, toggles, callouts, tables, code blocks. Not a wall of markdown pasted into one block.
- Notion renders a table of contents from your headings; use a `table_of_contents` block rather than hand-rolling a link list.
- Use callout blocks for definitions, invariants, and edge cases.
- Code goes in real code blocks with the language set, so it stays monospaced and keeps its newlines.

## Diagrams

Notion can't do custom CSS, so lean on what it has: tables for mappings and before/after comparisons, nested lists for flows and hierarchies, callouts for the boxes in a system diagram, columns for side-by-side panels. Keep the diagram families consistent across the page.

Still no ASCII diagrams, and still always include example data.

## Quiz mechanics

Toggle blocks stand in for interactivity — the reader picks an answer mentally, then opens the toggle to see if they were right. Structure each question as a numbered item with one toggle per option:

```markdown
1. Question
   ▶ Option 1
     ❌ Why this is wrong, and the misconception behind it
   ▶ Option 2
     ❌ Why this is wrong, and the misconception behind it
   ▶ Option 3
     ✅ Why this is right
   ▶ Option 4
     ❌ Why this is wrong, and the misconception behind it
```

The toggle title is the option text alone. Don't put ✅/❌ or any hint in the title — it's visible before the toggle is opened, which gives the answer away.

## Handing off

Return the URL of the new page, plus a sentence on what you inspected and any assumptions or gaps.
