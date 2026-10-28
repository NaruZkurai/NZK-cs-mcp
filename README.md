# NZK-cs-mcp

The **v3 csgraph** engine and its stdio MCP server, mirroring the engine used by
the native [cs viewer v3](https://github.com/NaruZkurai/nzk-cs-viewer) (`3.0.0-beta.9`).

`core/` is `csgraph-core` — lexer, parser, relation graph, document synthesis,
reorganisation, dedupe and the `/api/*` surface — plus the `csgraph` CLI, whose
`--mcp` flag speaks the Model Context Protocol over stdio.

## Build

```sh
cargo build --release -p csgraph-core
# -> target/release/csgraph
```

## Run as an MCP server

```sh
csgraph --mcp --repo /path/to/repo --root <rel-root> --threads 4
```

`--repo` is repeatable: every bound repo is served by one server, the first is
the default, and every tool takes an optional `repo` argument (1-based index,
path, or unique basename). `tools/list` currently advertises 42 tools.

## Related repositories

- **GUI cs viewer:** <https://github.com/NaruZkurai/nzk-cs-viewer> — the native
  v3 host (winit + wgpu + egui) that uses this engine.
- **DSH plugin:** <https://github.com/NaruZkurai/nzk-cs-mcp-dsh-plugin> — the
  DeepSeek Harness bundle that registers this server as `mcp__csgraph__*`.

## Verify

```sh
node <plugin>/test/smoke.mjs   # initialize -> tools/list against the real binary
```
