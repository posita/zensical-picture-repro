# Relative paths in `<picture>`

This reproduces different handling of the same relative path in `<source srcset>` and `<img src>`. It does not use mkdocstrings or any other plugin.

Tested with Zensical 0.0.65 and MkDocs 1.6.1:

```sh
zensical build --clean
mkdocs build -d site-mkdocs
```

In `docs/symptom.md`, both attributes contain `../images/example.svg`. In `site/symptom/index.html`, Zensical leaves `srcset` as `../images/example.svg` but changes `src` to `../../images/example.svg`. MkDocs leaves both as `../images/example.svg` in `site-mkdocs/symptom/index.html`.

The image exists at `site/images/example.svg`. Thus, from `site/symptom/index.html`, the Zensical `<source>` path reaches the image, while the fallback `<img>` path does not. The reproduction uses a dark-only `<source>` so a light-mode browser uses the fallback.
