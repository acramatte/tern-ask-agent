# Tern: Ask an agent

A macOS and Linux desktop plugin for [Tern](https://stencil.so/tern) that sends highlighted terminal output to an agent for explanation—useful for warnings, errors, and running logs.

## Install

Requires Tern with `cx.agents:start` support (tested on 0.8.2) and a configured agent such as `omp`. macOS uses the built-in `/usr/bin/pbpaste`; Linux requires `wl-paste` on Wayland or `xclip` on X11.

```sh
tern plugin link /path/to/tern-ask-agent
tern plugin reload
```

On your Mac, copy the updated plugin folder, then run the same link/reload commands with its local path. No Homebrew clipboard package is needed.

## Use

Highlight text and press **⌘⌥A** (Command+Option+A) on Mac or **F8** on Linux. Alternatively, choose **Ask an agent about selected text** in the command palette (**Ctrl+Shift+P** on the default Linux keymap).

The plugin opens an agent split beside the logs, using Tern's **Settings → Agents** command. It includes the selection, source directory, and current or most recent shell command. The original process keeps running. The prompt requests an explanation and diagnostic steps without edits or remediation; agent permissions remain unchanged.

## Limitations

- Uses the clipboard because Tern's public plugin API has no terminal-selection getter or context-menu hook; no right-click entry.
- Overwrites clipboard contents; invoking without a selection clears them. Avoid copying other text during the handoff, and check logs for secrets before sending.
- Sends at most the last 32 KB of a selection; the prompt tells the agent when text was cut.
- Verified end-to-end with omp on X11. Native macOS and hardware-triggered Wayland use are unverified; clipboard-access failures abort with a toast.
- macOS and Linux desktop only. Change the shortcut in `window.luau` or bind `plugin.ask-agent.ask-selection` in Tern's keyboard settings.

To uninstall: `tern plugin unlink ask-agent`.
