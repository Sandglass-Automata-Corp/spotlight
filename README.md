# G Code (Macro B) Syntax Highlighting for VS Code

VS Code extension that adds Fanuc-style G Code Macro B syntax highlighting and registers `.nc` files as language `G Code` (`gcode`).

## What this extension highlights

- Comments: `; ...` and `( ... )` (including nested parentheses comments)
- G codes: `G0`, `G1`, `G65`, etc.
- M codes: `M3`, `M30`, `M98`, etc.
- N sequence numbers: `N10`, `N20`, etc. (separate from G/M)
- Sub programs: `O1234` and `M98 P1234`
- Sub macros: `O9xxx` and `G65/G66/G66.1 Pxxxx`
- Variables: `#1`, `#500`, `#<name>`, `#[expr]`
- Conditionals/control flow: `IF`, `THEN`, `WHILE`, `DO`, `END`, `GOTO`
- Brackets and parentheses
- Unclosed `(` comment groups are marked as invalid

## Developer prerequisites

- VS Code
- Node.js + npm
- Optional: VS Code CLI in PATH (`code`) if you want terminal install commands

## Install for development

### Option A: Extension Development Host

1. Open this folder in VS Code.
2. Run:

```bash
npm install
```

3. Press `F5` to launch the Extension Development Host.
4. Open `/Users/chris/devel/spotlight/macro-b-test.nc`.
5. Confirm language mode is `G Code`.

### Option B: Build and install VSIX (recommended if `F5` is unreliable)

1. Build:

```bash
cd /Users/chris/devel/spotlight
npx @vscode/vsce package
```

2. Install/reinstall:

```bash
code --install-extension /Users/chris/devel/spotlight/g-code-macro-b-0.0.1.vsix --force
```

3. Reload VS Code.

## After install

1. Set the bundled theme for guaranteed distinct token colors:
   - `Preferences: Color Theme` -> `G Code Tokyo Night Pro`
2. If another extension takes over `.nc`, force association in `settings.json`:

```json
{
  "files.associations": {
    "*.nc": "gcode"
  }
}
```

## Iterating on changes

When you change grammar/theme/manifest files, rebuild and reinstall the VSIX:

```bash
cd /Users/chris/devel/spotlight
npx @vscode/vsce package
code --install-extension /Users/chris/devel/spotlight/g-code-macro-b-0.0.1.vsix --force
```

## Quick validation checklist

Use `/Users/chris/devel/spotlight/macro-b-test.nc` and verify:

- `G` and `M` tokens are different colors
- `N` tokens have their own color
- `IF/THEN/WHILE/GOTO` have dedicated colors
- Nested comments like `(((SUB PROGRAM)))` do not produce stray red `)`
- An unclosed `(` comment is highlighted as invalid
