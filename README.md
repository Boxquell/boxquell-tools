# boxquell-tools

Official tool recipes for [Boxquell](https://github.com/Boxquell/boxquell). Boxquell adds this repository by itself on first use.

```sh
boxquell recipes                      # everything that can be installed
boxquell add mybox jq ripgrep
boxquell repo update tools          # fetch the latest recipes
```

## Recipes

| Recipe | What it installs |
|---|---|
| `bitbucket-cli` | Bitbucket CLI (`bkt`) for Bitbucket Cloud |
| `build-essential` | gcc, g++, make and pkg-config from Debian |
| `composer` | Composer, the dependency manager for PHP (installs PHP from the languages repository) |
| `confluence-cli` | Confluence CLI (`confluence`, from npm; installs Node.js from the languages repository) |
| `docker` | Docker Engine with Buildx and Compose (see below) |
| `gh` | GitHub CLI, with github.com allowed for git and the API |
| `git` | git with Git LFS |
| `glab` | GitLab CLI, with gitlab.com allowed for git and the API |
| `jira-cli` | Jira CLI (`jira`) for Jira Cloud |
| `jq` | Command-line JSON processor |
| `playwright` | Playwright with headless Chromium and its system libraries (installs Node.js from the languages repository) |
| `ripgrep` | Fast recursive search (`rg`) |

## IDEs

| Recipe | What it does |
|---|---|
| `code-server` | VS Code in the browser. Start it with `boxquell run mybox code-server`, then open http://127.0.0.1:8080 (forwarded on install). |
| `vscode-remote` | Allows the hosts VS Code's Remote-SSH needs to install its server and extensions in the sandbox. |
| `jetbrains-remote` | Allows the hosts JetBrains Gateway needs to install an IDE backend and plugins in the sandbox. |

For the last two, run `boxquell ssh-config --install` once and connect the IDE to the ssh host `boxquell-<name>`.

## Docker in a sandbox

The sandbox kernel has no NAT, so Docker runs without its own bridge. Give containers the sandbox's network:

```sh
docker run --rm --network host alpine wget -qO- https://example.com
docker build --network host -t app .
```

In Compose files use `network_mode: host`. Containers are held to the sandbox's network rules, and their connections show up in the network log. Without `--network host` a container has no network.

## Contributing

One TOML file per recipe in `recipes/`. The format is described in [docs/recipes.md](https://github.com/Boxquell/boxquell/blob/main/docs/recipes.md); the workflow in this repository checks every file.

A recipe may carry `icon = "<file>.svg"` right after its `description`; the file lives in `icons/` and is a single-colour SVG under 8 KB. Icons in `icons/` come from [Simple Icons](https://simpleicons.org) (CC0). The logos remain trademarks of their owners.

## License

Licensed under either of [Apache License 2.0](LICENSE-APACHE) or [MIT license](LICENSE-MIT) at your option.
