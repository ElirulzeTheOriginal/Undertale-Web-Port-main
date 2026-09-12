# Undertale Web Port

A browser build of the game using the compiled GameMaker runtime.

## Run Locally

Open a terminal in the project folder:

```bash
cd /workspaces/Undertale-Web-Port-main
python3 -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

Do not open `index.html` directly with `file://`; the game needs an HTTP server to load its runtime and data files.

## Restart The Server

Use this command to stop anything currently using port 8000 and start a fresh server:

```bash
cd /workspaces/Undertale-Web-Port-main
fuser -k 8000/tcp 2>/dev/null || true
python3 -m http.server 8000
```

The terminal must stay open while playing. Stop the server with `Ctrl+C`.

## Verify The Server

Check that the page and required runtime files are reachable:

```bash
curl -I http://localhost:8000/index.html
curl -I http://localhost:8000/runner.js
curl -I http://localhost:8000/runner.wasm
curl -I http://localhost:8000/runner.data
curl -I http://localhost:8000/game.unx
```

Check the supplied fonts:

```bash
for file in fonts/*; do
  [[ -f "$file" ]] && printf '%s -> ' "$file" && fc-scan --format '%{family} | %{style}\n' "$file" | head -n 1
done
```

## Browser Refresh

After changing files, use `Ctrl+Shift+R` to bypass the browser cache, then reopen the local URL.

The opening sequence uses `Z`, `Enter`, or `Space` to continue or skip its dialogue.

## Project Files

- `index.html`: browser wrapper, scaling, font registration, and runtime startup
- `runner.js`: generated Emscripten runtime
- `runner.wasm`: compiled game runtime
- `runner.data`: language and support data package
- `game.unx`: compiled GameMaker game package
- `audio/`: game music and sound effects
- `fonts/`: supplied font files

The original editable GameMaker project is not included; the game package is a compiled export. The active `game.unx` is the original verified build. Experimental compiled patches are preserved as `game-relative-path.unx` and `game-absolute-path.unx`.

Audio files are stored in `audio/`. Root-level symbolic links are kept because the compiled game requests the original root filenames.
# Undertale
