# G Code (Macro B) Syntax Highlighting for VS Code

This extension adds syntax highlighting for Fanuc-style G Code Macro B and registers all `.nc` files as `G Code`.

It highlights:

- Comments: `; ...` and `( ... )`
- G codes: `G0`, `G1`, `G65`, etc.
- M codes: `M3`, `M30`, `M98`, etc.
- Sub programs: `O1234` and `M98 P1234` style calls
- Sub macros: `O9xxx` and `G65/G66 Pxxxx` style calls
- Variables: `#1`, `#500`, `#<name>`, `#[expr]`
- Sequence numbers: `N10`, `N20`, etc. (separate from G/M codes)
- Conditionals/control flow: `IF`, `THEN`, `WHILE`, `DO`, `END`, `GOTO`, etc.
- Brackets: `[` and `]`
- Parentheses: `(` and `)` delimiters

The language name in VS Code is exactly: `G Code`.

## Install in VS Code

### Option 1: Run it directly in Extension Development Host

1. Open this folder in VS Code.
2. Run:

```bash
npm install
```

3. Press `F5` (Run Extension).
4. In the new VS Code window, open any `.nc` file.
5. Confirm language mode (bottom-right) is `G Code`.

### Option 2: Package and install as a `.vsix`

1. From this folder, run:

```bash
npx @vscode/vsce package
```

2. Install the generated `.vsix`:

```bash
code --install-extension g-code-macro-b-0.0.1.vsix
```

3. Reload VS Code.

## Force all `.nc` files to `G Code` (if another extension conflicts)

Add this to your VS Code `settings.json`:

```json
{
  "files.associations": {
    "*.nc": "gcode"
  }
}
```

## Tokyo Night Storm

The grammar uses standard TextMate scopes (`keyword.control`, `entity.name.function`, `variable.other`, `comment`, `punctuation.section`) so Tokyo Night Storm should render each requested token group with distinct colors.
