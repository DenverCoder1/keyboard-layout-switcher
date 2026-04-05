# Contributing to Keyboard Layout Switcher

## Getting Started

### Prerequisites

- Google Chrome or Chromium-based browser
- Basic knowledge of JavaScript, HTML, and CSS

### Setup

1. Fork and clone the repository:

    ```bash
    git clone https://github.com/YOUR_USERNAME/keyboard-switch-shortcut.git
    cd keyboard-switch-shortcut
    ```

2. Load the extension in Chrome:
    - Go to `chrome://extensions/`
    - Enable "Developer mode"
    - Click "Load unpacked" and select the project directory

3. After making changes, reload the extension from `chrome://extensions/`. For content script changes, also reload the webpage.

## Adding a New Keyboard Layout

All layout configuration lives in `layouts.js`. **No other files need to be changed.**

Add an entry to the `KEYBOARD_LAYOUTS` object:

```javascript
"french-english": {
    defaultShortcut: { ctrl: false, shift: true, alt: true, key: "F", direction: "auto" },
    layouts: {
        french: {
            chars: "character_mapping_in_qwerty_order",
            name: "French",
        },
        english: {
            chars: "qwertyuiop[]asdfghjkl;'zxcvbnm,./",
            name: "English",
        },
    },
},
```

### Fields

- **`name`** — display name shown in the settings UI, using the ↔ symbol
- **`defaultShortcut`** — the shortcut pre-filled in settings for new installs (`ctrl`, `shift`, `alt` booleans + `key` string + `direction`: `"auto"`, `"forward"`, or `"reverse"`)
- **`layouts`** — exactly two entries; each has a `name` and a `chars` string in QWERTY order

### Character Mapping Format

List characters in the order they appear on a standard QWERTY keyboard:

```
q w e r t y u i o p [ ]
a s d f g h j k l ; '
z x c v b n m , . /
```

Both `chars` strings must be the same length (33 characters for a full mapping). A mismatch will log a warning and only map up to the shorter length.

**Hebrew example:**

```javascript
chars: "/'קראטוןםפ][שדגכעיחלךף,זסבהנמצתץ.";
```

### Checklist

- [ ] Layout ID is unique, kebab-case (e.g. `french-english`)
- [ ] Both `chars` strings are the same length
- [ ] Characters are in the correct order (match QWERTY layout)
- [ ] `defaultShortcut.key` doesn't conflict with existing default layouts (e.g. `Alt+Shift+H`, `Alt+Shift+R`, `Alt+Shift+E`, `Alt+Shift+A` are taken)
- [ ] Tested in both directions
- [ ] `README.md` updated to list the new layout and its default shortcut

## Reporting Bugs

Include: a description, steps to reproduce, expected vs actual behaviour, browser version, and OS.

## Pull Request Process

1. Create a branch: `git checkout -b feature/your-feature-name`
2. Make and test your changes
3. Push and open a pull request against `main`

## Code Style

- Format with Prettier
- Meaningful variable and function names
- Comments for non-obvious logic
- ES6+ JavaScript
