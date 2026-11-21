---
name: capture-and-inspect
description: Capture a Mac window, screen area or display with Sightline and inspect it - read text and QR codes or barcodes, find where text is, pick a color, list windows. Use when the user wants a screenshot of a window or area, to read text or a code on screen, or to locate UI text.
---

# Capture and inspect the screen

1. **Find a real target first.** Call `list_windows` for app name, title and window id, and `list_displays` for display indexes. Coordinates are points, origin at the top left of the main display.
2. **Capture.**
   - `capture_window` for an app window, by `app`, `title` or `id` (preferred).
   - `capture_area` for a region: x, y, width, height in points.
   - `capture_screen` for a whole display.
   - `capture_scrolling` only if it is actually listed among the tools. The Mac App Store version of Sightline does not offer it.
3. **Inspect as asked.**
   - `capture_text` reads text with on-device OCR and decodes QR codes and barcodes, from a window, area, display or a saved image path.
   - `find_text` returns pixel boxes for text.
   - `pick_color` returns the hex and RGB color of one point, in the same points as `list_windows`.
4. **Follow up.** To add marks, a style or open the result, pass the returned path (it is in the Agent folder) to `annotate`, `beautify` or `open_in_editor`. If the user means a screenshot they have open ("this screenshot"), call `list_editors` first and pass its id as `editor`.

Read the live tool schema or https://sightlinemac.com/docs/mcp/ for other parameters. Do not invent fields.
