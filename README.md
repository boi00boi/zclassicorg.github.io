# Zclassic website

A responsive community frontend for [zclassic.org](https://zclassic.org/), built with HTML, CSS, and vanilla JavaScript. It runs as a static website with no build step, package installation, or external UI libraries.

## Features

- Responsive layouts for mobile, tablet, and desktop.
- Light and dark themes, with the selected theme saved locally.
- A scalable copper SVG logo used in the header, footer, and hero coin.
- Wallet platform tabs, resource search and category filters, and a copyable Z23 command.
- Accessible navigation, reduced motion support, and usable content with JavaScript disabled.
- PNG, SVG, ICO, Apple touch, and web manifest icons generated with [RealFaviconGenerator](https://realfavicongenerator.net/).

## Repository layout

Keep `index.html` and `README.md` at the repository root. Put the frontend assets in `frontend-zcl/`.

| Path | Purpose |
| --- | --- |
| `index.html` | Page content, inline SVG illustrations, and JavaScript interactions |
| `README.md` | Setup and contribution instructions |
| `frontend-zcl/style.css` | All page styling, responsive rules, embedded fonts, and font license notices |
| `frontend-zcl/zclassic.svg` | Zclassic logo |
| `frontend-zcl/cc0.svg` | Linked CC0 badge in the footer |
| `frontend-zcl/favicon.svg` | Scalable browser icon |
| `frontend-zcl/favicon-96x96.png` | 96 × 96 browser icon |
| `frontend-zcl/favicon.ico` | ICO browser icon |
| `frontend-zcl/apple-touch-icon.png` | 180 × 180 Apple touch icon |
| `frontend-zcl/site.webmanifest` | App name, icon locations, and launch settings |
| `frontend-zcl/web-app-manifest-192x192.png` | 192 × 192 app icon |
| `frontend-zcl/web-app-manifest-512x512.png` | 512 × 512 app icon |

Existing repository files, including `CNAME` and the linked PDF documents, should stay in place.

## Local preview

From the directory containing `index.html`, run:

```sh
python3 -m http.server 8000
```

Open [http://localhost:8000/](http://localhost:8000/) in your browser. Stop the server with `Ctrl+C`.

You can also open `index.html` directly to preview the page. Use the local server when checking favicon and manifest behavior. Keep the `frontend-zcl` folder beside `index.html` in either case.

## Editing the website

Edit page text, resource destinations, and JavaScript interactions in `index.html`. Edit colors, spacing, typography, breakpoints, and animations in `frontend-zcl/style.css`.

The stylesheet contains embedded Manrope and Space Grotesk fonts, so the page does not need to download fonts from another service. Their complete license notices are preserved at the end of the stylesheet.

Telegram and the main Zclassic repository link are available through the footer icons. Their duplicate entries have been removed from Resources. Links to specific tools, source repositories, and wallet downloads remain available where relevant.

## Favicons

The HTML head includes these paths:

```html
<link rel="stylesheet" href="./frontend-zcl/style.css">
<link rel="icon" type="image/png" href="./frontend-zcl/favicon-96x96.png" sizes="96x96">
<link rel="icon" type="image/svg+xml" href="./frontend-zcl/favicon.svg">
<link rel="shortcut icon" href="./frontend-zcl/favicon.ico">
<link rel="apple-touch-icon" sizes="180x180" href="./frontend-zcl/apple-touch-icon.png">
<meta name="apple-mobile-web-app-title" content="Zclassic">
<link rel="manifest" href="./frontend-zcl/site.webmanifest">
```

The manifest's icon paths are relative to the manifest file, so they point to the PNG files in the same folder. Its `start_url` and `scope` use `../` to point back to the homepage. These relative paths also support a preview hosted under a repository subdirectory.

When regenerating favicons, replace the seven generated favicon files in `frontend-zcl/` and retain this folder arrangement. If the generator produces root paths such as `/web-app-manifest-192x192.png`, update them to `./web-app-manifest-192x192.png` in `site.webmanifest`.

## Contributing through GitHub

1. Fork [ZclassicCommunity/zclassicorg.github.io](https://github.com/ZclassicCommunity/zclassicorg.github.io) and create a branch for your changes.
2. Upload the updated `index.html`, this `README.md`, and the complete `frontend-zcl/` folder at the repository root. Upload the files and folder, rather than the ZIP itself.
3. Keep the repository's existing domain configuration and documents. Commit the new asset paths and their files together.
4. Preview the homepage on mobile and desktop, check both themes, and confirm that all frontend assets load.
5. Open a pull request against the community repository's `main` branch. Maintainers can review and publish the change through the repository's existing hosting setup.

This homepage uses `frontend-zcl/style.css`. The old root-level `style.css` and `zclassic.png` are not referenced by this version. Root-level copies of `zclassic.svg` and `cc0.svg` are also replaced by the copies inside `frontend-zcl/`.

## Notices

The homepage's [CC0 public domain notice](https://creativecommons.org/publicdomain/zero/1.0/) is preserved. The CC0 badge comes from the [official Creative Commons downloads](https://creativecommons.org/mission/downloads/).

Manrope and Space Grotesk font software retain their SIL Open Font License 1.1 notices in `frontend-zcl/style.css`. Keep those notices with the embedded fonts.

## References

- [RealFaviconGenerator](https://realfavicongenerator.net/)
- [Manifest icon path reference](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Manifest/Reference/icons)
- [GitHub pull request guide](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork)
