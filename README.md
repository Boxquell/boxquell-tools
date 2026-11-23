# boxquell-tools

Official tool recipes for [Boxquell](https://github.com/ToBee94/boxquell). Boxquell adds this repository by itself on first use.

```sh
boxquell recipes                      # everything that can be installed
boxquell add mybox jq ripgrep
boxquell repo update tools          # fetch the latest recipes
```

## Recipes

| Recipe | What it installs |
|---|---|
| `build-essential` | gcc, g++, make and pkg-config from Debian |
| `composer` | Composer, the dependency manager for PHP (installs PHP from the languages repository) |
| `docker` | Docker Engine with Buildx and Compose (see below) |
| `gh` | GitHub CLI, with github.com allowed for git and the API |
| `git` | git with Git LFS |
| `jq` | Command-line JSON processor |
| `ripgrep` | Fast recursive search (`rg`) |

## Docker in a sandbox

The sandbox kernel has no NAT, so Docker runs without its own bridge. Give containers the sandbox's network:

```sh
docker run --rm --network host alpine wget -qO- https://example.com
docker build --network host -t app .
```

In Compose files use `network_mode: host`. Containers are held to the sandbox's network rules, and their connections show up in the network log. Without `--network host` a container has no network.

## Contributing

One TOML file per recipe in `recipes/`. The format is described in [docs/recipes.md](https://github.com/ToBee94/boxquell/blob/main/docs/recipes.md); the workflow in this repository checks every file.

## License

Licensed under either of [Apache License 2.0](LICENSE-APACHE) or [MIT license](LICENSE-MIT) at your option.
