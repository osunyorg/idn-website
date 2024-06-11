# Internal links

This repository is configured to run workflows that use the Lychee link checker.

In addition to the workflows, here we also include a recipe to check for absoulte URLs to the main `degrowth.net` domain, which may be undesireable for local builds and additional environments, such as `next`. With this information we can change them to relative links.

## Find absolute internal links

First we create a local build of the page that is scoped at the base URL `https://next.degrowth.net`. Then we can use the generated output to check the internal links and store the result in a file called `lychee.json`.

```sh
yarn install
HUGO_BASEURL=https://next.degrowth.net yarn osuny build
podman run --init --rm -it -v ${PWD}:/input -w /input lycheeverse/lychee -c .github/lychee.internal.toml --base https://next.degrowth.net --no-progress --include-fragments --format json --output /input/lychee.json public
```

This file in return can be used to check for internal links that point at a different base URL than the one specified.

```sh
jq '
  .success_map |
  to_entries |
  map(
    select(
      .value |
      any(.url | startswith("https://degrowth.net"))
    ) |
    {(.key): [.value[] | select(.url | startswith("https://degrowth.net")) | .url]}
  ) |
  add
' lychee.json
```

This creates a list of pages that use absolute URLs to address pages from within the content.

The output of the above will look like:

```sh
{
  "public/individual-membership/index.html": [
    "https://degrowth.net/join-us/group-membership/",
    "https://degrowth.net/structure/",
    "https://degrowth.net/about/principles/"
  ],
  "public/about-us/index.html": [
    "https://degrowth.net/en/about/principles/"
  ],
  "public/pontevedra-assembly-2024/index.html": [
    "https://degrowth.net/members/"
  ],
  "public/index.html": [
    "https://degrowth.net/join-us/"
  ]
}
```

## Shape the data to preview relative internal links

We can remove some prefixes in the strings to shape the output into a form that is easier to read by us:

```sh
jq '
  .success_map |
  to_entries |
  map(
    select(
      .value |
      any(.url | startswith("https://degrowth.net"))
    ) |
    {
      (.key | sub("^public/"; "")):
      [.value[] | select(.url | startswith("https://degrowth.net")) | .url | sub("https://degrowth.net"; "")]
    }
  ) |
  add
' lychee.json
```

Which gives us a nice list of pages and links that we can change in the Osuny backend at [idn.osuny.org/](https://idn.osuny.org):

```json
{
  "individual-membership/index.html": [
    "/join-us/group-membership/",
    "/structure/",
    "/about/principles/"
  ],
  "about-us/index.html": [
    "/en/about/principles/"
  ],
  "pontevedra-assembly-2024/index.html": [
    "/members/"
  ],
  "index.html": [
    "/join-us/"
  ]
}
```
