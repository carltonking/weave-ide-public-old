# Weave fork patches

Every change this fork makes to upstream `microsoft/vscode`, so rebases stay manageable.
Rule: Weave code lives in `src/vs/workbench/contrib/weave/`. Anything outside that folder is listed here with a reason.

| File | Change | Why |
|---|---|---|
| `product.json` | Names, ids, data folders, URL protocol set to Weave; `extensionsGallery` points at Open VSX | Rebrand; forks can't use the Microsoft Marketplace |
| `FORK_PATCHES.md` | This file | Patch log |
| `.github/workflows/weave-build.yml` | Weave CI: install + compile on GitHub-hosted macOS | Upstream workflows need Microsoft's private runners; they are disabled in the fork's Actions settings, not deleted, to keep rebases clean |

Upstream base: `54ab7943` (shallow clone, Nov 2026).

## Build (macOS)

```sh
fnm use 24.22.1          # version from .nvmrc
corepack pnpm install    # fsevents build errors are expected (optional dependency)
corepack pnpm run compile
./scripts/code.sh        # launch Weave
```

The checkout must live at a path without spaces (`~/Developer/weave-ide`); VS Code's native module builds fail otherwise.
