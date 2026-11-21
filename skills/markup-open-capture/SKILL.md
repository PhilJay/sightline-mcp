---
name: markup-open-capture
description: Annotate or edit the screenshot or recording the user has open in Sightline, or the agent's own last capture, with arrows, boxes, numbers, text, highlights, blur and other marks. Use when the user wants marks on the current or last screenshot.
---

# Mark up an open capture

1. **Find the right picture.** If the user means a capture they are looking at ("this screenshot", "my last screenshot"), call `list_editors` first and use the editor's `id` as `editor`. `last_screenshot` is only this agent's own last capture, not the user's. To find an older capture of the user, use `search_captures`; other tools only take files in the Agent folder, so copy a file found there into the Agent folder before marking it up.
2. **Draw.** Call `annotate` with `editor` or `path`. The change shows up live in an open editor as one undo step. Use `open_in_editor` instead when the user wants to adjust the marks by hand.
   - Annotation types: arrow, line, freehand, rectangle, ellipse, highlight, blur, spotlight, magnify, text, number.
   - Coordinates are pixels of the image, origin top left, not screen points. For an editor, use the width and height `list_editors` reports.
3. **Everything else** (colors, crop, rotate, resize, export, recording options, camera): follow the live tool schema or https://sightlinemac.com/docs/mcp/. Do not invent keys.
