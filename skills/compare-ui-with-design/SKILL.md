---
name: compare-ui-with-design
description: Compare a running Mac or iOS Simulator UI with a design image using Sightline's compare_with_design (the agent version of Show Differences on a pin), then fix the differences and check again until none remain. Use when the user wants to check a UI against a design, run Show Differences, or find visual regressions.
---

# Compare a UI with a design

Agents have no pin tool. `compare_with_design` runs the same check as Show Differences on a Sightline pin.

1. **Put the design in the Agent folder.** The design must be a PNG, JPEG or WebP inside the Sightline Agent folder, the folder that paths returned by capture tools are in. If the design is somewhere else, such as a Figma export or a file in the repository, copy it into that folder first (for example with `cp` next to a path a capture tool returned) and pass the copied path as `design`.
2. **Find the target.** Call `list_windows` (and `list_displays` if needed). Prefer `window` with `app`, `title` or `id` for an app or the iOS Simulator. Use `area` (x, y, width, height in points) or `display` only when the user asked for a region or a whole display. With none of them, Sightline captures the display under the pointer.
3. **Compare.** Call `compare_with_design` with `design` and the target. `align` (default true) lines the design up by up to 8 pixels first.
4. **Read the result.** It returns a marked capture (path, width, height, scale), the overall `shift` (dx, dy) and up to 20 `differences`, each with a `number`, a pixel box and a `hint`:
   - `shifted`: that part sits dx, dy away from where the design has it.
   - `only_in_design`: missing on screen.
   - `only_on_screen`: on screen but not in the design.
   - `looks_different`: present in both, but different.
   When copy or labels may differ, also run `capture_text` on the design and on the window.
5. **Fix and check again.** Change the app or code, wait for the UI to reload, then call `compare_with_design` again with the same target. Later passes can use `include_image: false`. Repeat until `differences` is empty.

Do not say the UI matches while differences remain. If some are left, report each one by number and say why it is left (for example, intended, or data that differs from the design).

Full parameter reference: https://sightlinemac.com/docs/mcp/
