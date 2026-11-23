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
| `adminer` | Adminer, a database manager in one PHP file for MariaDB and PostgreSQL, served on port 8082 (installs PHP from the languages repository) |
| `aws-cli` | AWS CLI v2 (`aws`); credentials via `boxquell set <box> --env` |
| `azure-cli` | Azure CLI (`az`) |
| `bat` | A cat clone with syntax highlighting (`bat`) |
| `bitbucket-cli` | Bitbucket CLI (`bkt`) for Bitbucket Cloud |
| `build-essential` | gcc, g++, make and pkg-config from Debian |
| `caddy` | Caddy web server, from its official Debian repository; port 2015 is forwarded |
| `cargo-binstall` | cargo-binstall, installs Rust tools as prebuilt binaries (installs Rust from the languages repository) |
| `cargo-nextest` | cargo-nextest, a faster test runner for Rust (installs Rust from the languages repository) |
| `cmake` | CMake from the Kitware release installer (needs a C/C++ compiler, for example `build-essential`) |
| `composer` | Composer, the dependency manager for PHP (installs PHP from the languages repository) |
| `confluence-cli` | Confluence CLI (`confluence`, from npm; installs Node.js from the languages repository) |
| `delve` | Delve (`dlv`), the Go debugger (installs Go from the languages repository) |
| `docker` | Docker Engine with Buildx and Compose (see below) |
| `eslint` | ESLint as a global command (installs Node.js from the languages repository) |
| `fd` | Fast, friendly alternative to find (`fd`) |
| `ffmpeg` | FFmpeg and ffprobe for converting audio and video |
| `fzf` | Command-line fuzzy finder |
| `gcloud` | Google Cloud CLI (`gcloud`, `gsutil`, `bq`) |
| `gh` | GitHub CLI, with github.com allowed for git and the API |
| `git` | git with Git LFS |
| `glab` | GitLab CLI, with gitlab.com allowed for git and the API |
| `golangci-lint` | golangci-lint, the Go linters runner (installs Go from the languages repository) |
| `helm` | Helm, the Kubernetes package manager |
| `homebrew` | Homebrew, the package manager (`brew`), in /home/linuxbrew/.linuxbrew |
| `imagemagick` | ImageMagick command-line tools (`convert`, `identify`) |
| `jira-cli` | Jira CLI (`jira`) for Jira Cloud |
| `jq` | Command-line JSON processor |
| `jupyter` | JupyterLab on port 8888, started at boot, no token (installs Python from the languages repository) |
| `just` | `just`, a command runner for project recipes |
| `kubectl` | kubectl, the Kubernetes client |
| `laravel` | The Laravel installer (`laravel new`; installs Composer and PHP) |
| `mailpit` | Mailpit, catches outgoing mail: SMTP on port 1025 inside the sandbox, web UI on port 8025; started at boot |
| `mariadb` | MariaDB server and clients (Debian ships MariaDB, not MySQL), started at boot on localhost; user and database `dev` without a password |
| `netlify` | Netlify CLI (`netlify`; installs Node.js from the languages repository); a `netlify` secret can carry NETLIFY_AUTH_TOKEN |
| `opentofu` | OpenTofu (`tofu`) |
| `phpmyadmin` | phpMyAdmin for the local MariaDB, served on port 8081 and signed in as `dev` (installs PHP from the languages repository and MariaDB) |
| `playwright` | Playwright with headless Chromium and its system libraries (installs Node.js from the languages repository) |
| `pnpm` | pnpm, the disk-efficient package manager for Node.js (installs Node.js from the languages repository) |
| `poetry` | Poetry, dependency management for Python (installs Python from the languages repository) |
| `postgres` | PostgreSQL server and `psql`, started at boot on localhost; role and database `dev` without a password |
| `prettier` | Prettier, the code formatter, as a global command (installs Node.js from the languages repository) |
| `rails` | Ruby on Rails (`rails`; installs Ruby from the languages repository) |
| `redis` | Redis server and `redis-cli`, started at boot on localhost |
| `ripgrep` | Fast recursive search (`rg`) |
| `ruff` | Ruff, a fast Python linter and formatter |
| `sentry-cli` | Sentry CLI (`sentry-cli`); a `sentry` secret can carry SENTRY_AUTH_TOKEN |
| `shellcheck` | Static analysis for shell scripts |
| `sqlite` | `sqlite3` command-line shell |
| `stripe` | Stripe CLI (`stripe`), from Stripe's Debian repository |
| `symfony-cli` | The Symfony CLI (`symfony`; installs PHP from the languages repository) |
| `terraform` | Terraform from HashiCorp's apt repository |
| `tmux` | Terminal multiplexer |
| `typescript` | The TypeScript compiler (`tsc`) as a global command (installs Node.js from the languages repository) |
| `vercel` | Vercel CLI (`vercel`; installs Node.js from the languages repository); a `vercel` secret can carry VERCEL_TOKEN |
| `wrangler` | Wrangler, the Cloudflare Workers CLI (installs Node.js from the languages repository); a `cloudflare` secret can carry CLOUDFLARE_API_TOKEN |
| `yarn` | Yarn (modern), through Corepack (installs Node.js from the languages repository) |

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

A recipe may carry `icon = "<file>.svg"` right after its `description`; the file lives in `icons/` and is a single-colour SVG under 60 KB. Icons in `icons/` come from [Simple Icons](https://simpleicons.org) (CC0), generic glyphs from [Lucide](https://lucide.dev) (ISC), and a few are the projects' own logos. The logos remain trademarks of their owners.

## License

Licensed under either of [Apache License 2.0](LICENSE-APACHE) or [MIT license](LICENSE-MIT) at your option.
