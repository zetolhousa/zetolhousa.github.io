# Thejazeto Lhousa

Personal Hugo site published with GitHub Pages.

## Owner notes

### First setup

```sh
git clone git@github.com:zetolhousa/zetolhousa.github.io.git
cd zetolhousa.github.io
git submodule update --init --recursive
hugo server
```

Requires Hugo installed locally.

### Local dev

```sh
hugo server
```

Local site:

```text
http://localhost:1313/
```

### New blog post

```sh
hugo new posts/my-new-post.md
```

Edit the front matter, write the post, then remove or set `draft: false`.

### Static projects

Standalone apps can live under:

```text
static/projects/<project-name>/index.html
```

Example URLs:

```text
/projects/focus-notes/
/projects/hello-world/
```

Use relative asset paths inside project folders. Do not edit `public/` directly.

### Build check

```sh
hugo --minify
```

`public/` is generated output. Do not commit it.

### Deploy

Push to `main`. GitHub Actions builds the Hugo site and publishes `public/` to GitHub Pages.
