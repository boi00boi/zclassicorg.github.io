# Zclassic frontend review and remediation report

**Review date:** 5 October 2026  
**Reviewer:** Codex automated self-review  
**Submitted rating:** 6/10  
**Corrected version, published to PR #1:** 8/10

This report was produced with Codex. The contributor's earlier reference to Claude was a naming mistake. The assistant that helped create the redesign also performed this review; it is a self-review, not an independent audit.

## Source and publication status

The review examined the actual files submitted to [ZclassicCommunity/zclassicorg.github.io PR #1](https://github.com/ZclassicCommunity/zclassicorg.github.io/pull/1), rather than relying on an earlier local ZIP.

| Reference | Commit |
| --- | --- |
| Upstream baseline | `ca4c11b672cdba8097ae13c2390e188e9f5c667b` |
| Reviewed PR head | `4cbc1cd08b6df0c798a3cc308db7a2ec31997554` |
| Corrected local commit | `e692c3b44a1d792ebfc6faab67b242e148ca0b78` |
| Published correction commit | `5d8e1ae82aa32ac05caf74b14718f0021dfe8b4c` |
| Verified corrected tree | `71a11e453bb2aec1af2310aa4972ad90c21fb50f` |

The correction was published as one new commit to the contributor's fork `main`, updating the existing PR #1. That correction's Git tree exactly matches the tested local version. The corrected archive and patches contain the same code. This report is provided as a separate documentation addition to the PR. The PR remains open for maintainer review.

GitHub allowed writes to the contributor's fork but returned HTTP 403, “Resource not accessible by integration,” when updating the upstream PR title and description. Those metadata edits could not be published through the connection. The prepared title and description are provided separately for the contributor to paste into the existing PR.

## Assessment

The submitted design has a strong visual foundation: responsive sections, SVG branding, useful wallet controls, keyboard navigation, reduced-motion support and a usable no-JavaScript fallback. It has no third-party UI runtime dependencies. However, broken manifest paths, deleted compatibility assets, excessive embedded font weight and changes outside the intended UI scope make 6/10 appropriate for the submitted code.

The corrected version resolves those confirmed regressions and passes the checks listed below. An 8/10 rating reflects the improved reliability and smaller payload while acknowledging that the redesign remains substantially larger than the original minimal page and still needs a maintainer's review and broader browser testing. These scores are subjective engineering assessments, not standardized audit grades.

## Confirmed findings and fixes

| Finding | Evidence in the submitted PR | Correction |
| --- | --- | --- |
| Excessive HTML/CSS weight | Two embedded webfont payloads inflated compressed HTML plus CSS to 70,662 bytes, 14.68× the original. | Removed embedded fonts and their associated notices together. Use native system fonts; compressed HTML plus CSS is now 19,957 bytes. |
| Broken manifest icon paths | The manifest requested `/web-app-manifest-192x192.png` and `/web-app-manifest-512x512.png`; both returned HTTP 404 in the submitted local preview. | Use `./web-app-manifest-192x192.png` and `./web-app-manifest-512x512.png`, relative to the manifest in `frontend-zcl/`. Both return HTTP 200. |
| README and manifest disagree | README described launch settings absent from the uploaded manifest. | Add `start_url` and `scope` as `../`, align app naming and theme colors, and document the actual settings. |
| Existing URLs removed | Root `style.css`, `zclassic.png`, `zclassic.ico` and `cc0.png` were deleted. Requests to those paths returned HTTP 404. | Restore all four byte-for-byte from upstream. The homepage can use new SVG assets while existing consumers retain their old URLs. |
| Unrelated licence edit | The MIT copyright year changed from 2021 to 2026. | Restore the entire `LICENSE` byte-for-byte from upstream. |
| SEO and social metadata lost | Original canonical URL and Open Graph metadata were absent. | Restore canonical URL, Open Graph fields, original page title and description. The original social-preview PNG is available again. |
| Z23 instructions and technical copy changed | The redesign added `make doctor` and rewrote technical descriptions as part of a UI change. | Restore upstream setup commands, status wording and six capability descriptions. Preserve the new visual layout. |
| Copy commands maintained separately | The JavaScript copy string duplicated the displayed setup commands. | Derive copied commands from the displayed code, excluding decorative shell prompts. This avoids future disagreement between display and clipboard. |
| Small-screen code readability | Mobile terminal font was reduced to 7–8 pixels. | Use 12-pixel code text with scrolling confined to the terminal. No page-level horizontal overflow was detected. |

The PDF links now resolve to the repository's existing local documents, supporting local previews without changing their production destinations. Telegram and the main GitHub link remain outside the Resources list as requested.

## Measured weight

| Version | Raw HTML + referenced CSS | Gzipped HTML + referenced CSS | Ratio to upstream |
| --- | ---: | ---: | ---: |
| Upstream baseline | 14,491 bytes | 4,814 bytes / 4.70 KiB | 1.00× |
| Submitted PR | 152,895 bytes | 70,662 bytes / 69.01 KiB | 14.68× |
| Corrected version | 81,125 bytes | 19,957 bytes / 19.49 KiB | 4.15× |

**Reduction from the submitted version: 71.76%.**

Method: independently compress `index.html` and its referenced stylesheet with Python `gzip.compress` at the default level 9 and `mtime=0`, then sum the lengths. This measures these two source files only. It excludes favicon/install PNGs, SVG files, PDFs, transport headers and caching. It is not a Lighthouse score or a measurement of live-site loading time. The restored legacy stylesheet is not requested by the new homepage.

## Validation results

| Check | Result |
| --- | --- |
| Standard-library checker | Passed asset references, fragment IDs, duplicate IDs, new-tab link attributes, manifest resolution at `/` and `/preview/`, and the 22 KiB compressed HTML/CSS budget. |
| Upstream comparison | Passed byte parity for protected compatibility files and `LICENSE`, release-download URL parity, exact Z23 command parity, and canonical/Open Graph metadata parity. |
| Additional file hashes | `CNAME` and all three existing PDFs are also byte-for-byte unchanged. Nine protected files in total match upstream. |
| Responsive layout | Passed at widths 320, 375, 680, 768, 900, 901, 1024, 1440 and 1920 pixels. No page-level horizontal overflow; all page images loaded. |
| Primary interactions | All 17 checks passed: theme switching/persistence, mobile menu/focus/Escape, wallet targets and keyboard tabs, resource filtering/search/empty state, and copying commands. |
| Clipboard fallbacks | Successful legacy copy and manual-selection fallback both produced the exact three upstream commands. |
| JavaScript disabled | Windows, macOS and Linux wallet links remain visible with exact upstream targets; navigation remains usable; inactive interactive controls are hidden; no horizontal overflow. |
| Direct-file preview | `file://` page rendering loaded its images without horizontal overflow in the tested desktop viewport. Manifest behavior was checked through HTTP. |
| Reduced motion | Reduced-motion preference honored in the tested renderer. |
| Automated accessibility | axe-core WCAG 2 A/AA and 2.1 AA checks reported zero violations for mobile light, desktop light and desktop dark views. |
| Runtime requests/errors | No third-party runtime requests or JavaScript errors were observed in the tested page sessions. |
| HTTP asset checks | Both manifest icons, four original compatibility assets and four primary favicon/touch assets returned HTTP 200. |
| Patch application | Both the correction patch against the reviewed PR head and the complete redesign patch against the upstream baseline passed `git apply --check`. |

Browser checks used an isolated headless Chromium renderer with Playwright. Automated accessibility checks and layout checks are useful evidence, but do not establish complete accessibility conformance or Safari/Firefox/physical-device compatibility. Download targets were compared; the wallet binaries themselves were not audited or executed.

## Reproducing repository checks

Python 3.9 or newer is sufficient; no packages are required:

```sh
python3 tools/check_frontend.py
python3 tools/check_frontend.py --base ca4c11b672cdba8097ae13c2390e188e9f5c667b
```

The second command requires a Git checkout containing the baseline commit. For visual checks, serve the directory using `python3 -m http.server 8000` and open `http://localhost:8000/`.

## PR scope and remaining review

The final difference from upstream changes `index.html` and adds the frontend asset folder, README, standard-library checker and this review report. It leaves the original root assets, `LICENSE`, domain configuration and PDFs unchanged.

The existing PR had 14 commits from the contributor's fork `main` at the reviewed snapshot. One correction commit and a separate report addition preserve that history; they do not create a missing prior issue. Maintainers can decide whether to squash the PR. A complete code patch against the upstream baseline is also provided if maintainers request a clean feature branch. No remote history has been rewritten, and no duplicate PR has been opened.

Maintainers should inspect the final diff, review the preserved content and preview the native-font layout in their browsers before merging. The 4.15× HTML/CSS weight relative to the minimal original remains a deliberate visual-design tradeoff.
