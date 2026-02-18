# automator-autotype

A macOS Automator Quick Action that types clipboard contents character-by-character — useful for paste-restricted fields (VDI, Citrix, locked web forms).

## Why use this?

Many remote desktop and virtual environments block `Cmd+V` paste. Tools like [Mac-AutoType](https://github.com/user/mac-autotype) solve this, but require installing a third-party application.

**automator-autotype** is different:

- **Zero install** — uses only built-in macOS Automator and AppleScript
- **No third-party apps** — nothing to download, notarize, or trust
- **MDM-friendly** — easily deployed and allowlisted via configuration profile (PPPC)

## How it works

The workflow contains a single "Run AppleScript" action that:

1. Reads the current clipboard contents
2. Iterates over each character
3. Sends each character as a keystroke via `System Events`
4. Handles newlines by simulating the Return key
5. Adds a tiny delay (`0.01s`) between keystrokes for reliability

## Installation

1. **Clone or download** this repository
2. **Copy the workflow** to your Services folder:
   ```bash
   cp -R autotype.workflow ~/Library/Services/
   ```
3. **Grant Accessibility permission** — the first time you run it, macOS will prompt you to allow Automator (or the host app) in **System Settings → Privacy & Security → Accessibility**. Click "Allow".

### Corporate / MDM deployment

For managed Macs, IT can pre-approve the Accessibility permission via a PPPC (Privacy Preferences Policy Control) configuration profile targeting `com.apple.automator.runner` (or the relevant bundle ID of the calling application).

## Setting up a keyboard shortcut

1. Open **System Settings → Keyboard → Keyboard Shortcuts → Services** (on Ventura+: **System Settings → Keyboard → Keyboard Shortcuts → App Shortcuts** may also work)
2. Find **autotype** under **General**
3. Assign your preferred shortcut (e.g. `Ctrl+Cmd+V`)

## Usage

1. Copy text to the clipboard as usual (`Cmd+C`)
2. Click into the paste-restricted field
3. Trigger the shortcut — the text will be typed out character-by-character

## License

[MIT](LICENSE)
