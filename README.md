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

- `deploy-main-deuxfleurs-garage.yml` to deploy the `main` branch in the osunyorg/idn-website repository to DeuxFleurs' Garage service, published at [degrowth.net/](https://degrowth.net)
- `preview-next-github-pages.yml` to preview the `next` branch in the degrowth/idn-website fork with GitHub pages, published at [next.degrowth.net/](https://next.degrowth.net)

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
