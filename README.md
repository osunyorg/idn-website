# International Degrowth Network website

The source code for the [degrowth.net/](https://degrowth.net) web site.

## Preparation

1. Clone the git repository
2. Initialise the git submodules

## Installation

Collect the dependencies.

```sh
yarn install
```

## Development

Run a development webserver with hot-reloading.

```sh
yarn osuny dev
```

## Building

Build the website into `public/`.

```sh
yarn osuny build
```

## CI

Two workflows are used for this repository:

- `deuxfleurs.yml` to deploy the `main` branch in the [osunyorg/idn-website](https://github.com/osunyorg/idn-website) repository to DeuxFleurs' Garage service, published at [degrowth.net/](https://degrowth.net)
- `preview-next-github-pages.yml` to preview the `next` branch in the [degrowth/idn-website](https://github.com/degrowth/idn-website) fork with GitHub pages, published at [next.degrowth.net/](https://next.degrowth.net)

## Development Container

This repository contains a `.devcontainer.json` configuration file, which provides configuration for a [Development Container](https://containers.dev/).

It can be used with GitHub Codespaces: [Introduction to dev containers - GitHub Docs](https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces/adding-a-dev-container-configuration/introduction-to-dev-containers).

After GitHub Codespaces has started the development container, you can start an integrated development server with:

```sh
$ yarn codespaces
```

You can also [use the development container extension for Microsoft Visual Studio Code](https://code.visualstudio.com/docs/devcontainers/containers). Install the extension: [Dev Containers - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers). Once installed, it will prompt you, when a development container is detected in a repository. Do what the prompt suggests and your Osuny build environment is made available from within the container.

<details><summary>Advanced usage with the official CLI.</summary>

The CLI currently has no support for `forwardPorts`[¹](https://github.com/devcontainers/cli/issues/22), why we keep compatibility with using the `appPort` setting.

Install the CLI:

```sh
yarn global add @devcontainers/cli
```

Lify cycle of a development container:

```sh
devcontainer build --workspace-folder ./
devcontainer up --workspace-folder ./
```

You can now open the website generated from the development server at http://localhost:1313/.

</details>

## Authors

- Taylor A. Ahlstrom
- Arnaud Lévy
- Jon Richter

## License

The content under `content/` is under copyright, unless otherwise stated.

The rest of the repository is licensed under the MIT license.

See the LICENSE file for details.

## Copyright

© 2023—2024 International Degrowth Network contributors
