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
| `gh` | GitHub CLI, with github.com allowed for git and the API |
| `jq` | Command-line JSON processor |
| `ripgrep` | Fast recursive search (`rg`) |

## Contributing

One TOML file per recipe in `recipes/`. The format is described in [docs/recipes.md](https://github.com/ToBee94/boxquell/blob/main/docs/recipes.md); the workflow in this repository checks every file.

## License

Licensed under either of [Apache License 2.0](LICENSE-APACHE) or [MIT license](LICENSE-MIT) at your option.
