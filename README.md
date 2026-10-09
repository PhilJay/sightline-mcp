# Sightline MCP server

Screenshots, OCR, scrolling capture, annotations and screen recording on macOS for AI agents like Claude Code, Claude Desktop and Codex CLI.

The server is part of [Sightline](https://apps.apple.com/app/id6812521593), the screenshot and recording app for Mac ([sightlinemac.com](https://sightlinemac.com/)). It runs locally over stdio and nothing leaves your Mac.

![Tell your AI agent what you need and Sightline captures the right window and marks it up](assets/agent-prompt.png)

## You stay in control

![You approve each agent, and every capture names the agent and plays a sound](assets/you-stay-in-control.png)

- Agent access is off until you turn it on in Settings > AI Agents.
- A new agent has to ask for permission first. Allowed agents are listed in Settings and can be removed at any time.
- Every agent capture plays the capture sound and names the agent.
- Agents can't change settings and only read and write inside your screenshot folder.

## Setup

1. Install [Sightline](https://apps.apple.com/app/id6812521593) from the Mac App Store (macOS 14 or later) and give it Screen Recording permission.
2. Open Settings > AI Agents, turn agent access on and click Connect for Claude Code, Claude Desktop or Codex CLI.

Or add it by hand. Claude Code:

```
claude mcp add --scope user sightline -- "/Applications/Sightline.app/Contents/MacOS/sightline-cli" mcp
```

Codex CLI, in `~/.codex/config.toml`:

```toml
[mcp_servers.sightline]
command = "/Applications/Sightline.app/Contents/MacOS/sightline-cli"
args = ["mcp"]
```

Any other client: run `/Applications/Sightline.app/Contents/MacOS/sightline-cli mcp` as a stdio server.

## Command line

The same tools work from the terminal and in scripts. Sightline has to be running with agent access on, and it asks you to allow `sightline-cli` the first time.

```
sightline-cli tools                                      # list the tools
sightline-cli capture_window --json '{"app": "Safari"}'  # call one, prints JSON
```

`sightline-cli` lives at `/Applications/Sightline.app/Contents/MacOS/sightline-cli`.

## Tools

- `capture_screen`, `capture_area`, `capture_window` capture a display, an area or a window, optionally with annotations.
- `list_windows` lists the on-screen windows with app name, title and window id.
- `list_displays` lists the connected displays, so a capture, recording or text read can pick one.
- `capture_text` reads text with on-device OCR and decodes QR codes and barcodes.
- `find_text` returns pixel boxes for text in a window, area or display.
- `pick_color` returns the hex and RGB color of one point on screen.
- `capture_scrolling` stitches a scrolling area or window into one tall image.
- `annotate` draws arrows, shapes, freehand lines, text, spotlights and blurs or pixelation onto an image or a video and crops images. On a recording it also cuts and reorders clips, plays them at 0.5x to 15x, sets the volume of stretches and adds smooth or instant zooms; blurs follow what they cover.
- `record_screen` records a window, area or display for up to a minute to MP4. It never records the microphone.
- `inspect_recording` reports when a recording is still or moving and reads text in chosen frames.
- `last_screenshot`, `last_recording` return the newest capture.
- `copy_to_clipboard` copies an image to the clipboard.
- `open_in_editor` opens an image or recording in the Sightline editor with editable annotations, clips, sound, zooms or a Beautify look, continues a capture the user saved as editable, or opens the picture on the user's clipboard.
- `beautify` puts a screenshot on a background with padding, rounded corners and a shadow, using a built-in look, one of the user's presets or their default look.
- `list_looks` lists the built-in looks, the user's presets and their default look; `save_look` saves a new preset.
- `save_replay` saves the last seconds of the screen when Replay is on (macOS 27).
