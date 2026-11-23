# boxquell-recipes

Extra recipes for [Boxquell](https://github.com/ToBee94/boxquell): agents, languages and tools you can install into a sandbox.

```sh
boxquell repo add https://github.com/ToBee94/boxquell-recipes
boxquell recipes                 # lists them as recipes:<name>
boxquell add mybox recipes:jq
boxquell repo update             # fetch the latest recipes later
```

## Recipes in this repository

| Recipe | Category | What it installs |
|---|---|---|
| `jq` | tool | Command-line JSON processor |
| `ripgrep` | tool | Fast recursive search (`rg`) |

The recipes for Claude Code, Codex, opencode, pi, Node.js, Python, Go, Rust, C/C++ build tools and the GitHub CLI are built into Boxquell itself.

## Make your own repository

A recipe repository is any git repository with `*.toml` files in a `recipes` directory (or at its top level). The file name is the recipe's id. Add it with `boxquell repo add <git URL or local path>`; its recipes are then named `<repository>:<id>`.

```toml
name = "Node.js"                       # shown in lists
category = "language"                  # agent, language, tool or ide
description = "Node.js with npm"

versions = ["24", "22"]                # optional; first is the default, chosen as node@22
requires = ["build-essential"]         # optional; installed first (same repository, then built-in)
install_allow = ["nodejs.org"]         # destinations open only while the install script runs
allow = ["registry.npmjs.org"]         # destinations the software needs afterwards
secrets = ["anthropic"]                # optional; host secrets this software can use
command = "node"                       # agents only: the command that starts it

install = '''
# Runs in the sandbox as user `dev` with passwordless sudo, under `set -euo pipefail`.
# $BOXQUELL_VERSION holds the chosen version when the recipe has versions.
curl -fsSL "https://nodejs.org/dist/latest-v$BOXQUELL_VERSION.x/..." | ...
'''

[env]                                  # optional; variables for sessions in the sandbox
EXAMPLE = "1"
```

Rules of thumb:

- List every host the install script contacts in `install_allow`. Anything else is blocked, and `boxquell logs <sandbox> --blocked` shows what was refused.
- Keep `allow` as small as possible: these destinations stay open for the sandbox.
- The guest is Debian. Install to system paths (`/usr/local`) so every session finds the software.
- Never put credentials into a recipe. Name a secret instead; its value stays on the host.

Recipes run their own scripts inside the sandbox and open the destinations they list. Users are told so when they add a repository, and should add only repositories they trust.

## License

Licensed under either of [Apache License 2.0](LICENSE-APACHE) or [MIT license](LICENSE-MIT) at your option.
