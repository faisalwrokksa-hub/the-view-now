---
name: modern-web-guidance
description: Consult GoogleChrome Modern Web Guidance before making HTML/CSS/client-side JavaScript or browser UX changes; skip backend/infra-only tasks. This is a project-local integration adapter, not a vendored copy of Google's skill or an installed npm dependency.
---

# Modern Web Guidance — project integration

Official source: https://github.com/GoogleChrome/modern-web-guidance  
Official docs: https://developer.chrome.com/docs/modern-web-guidance  
Upstream license: Apache-2.0. This file is project-authored integration guidance rather than copied upstream source.  
Reviewed upstream package metadata on 2026-11-15: npm version `1.0.0`; review later upgrades rather than using unpinned `@latest` in automation.

## Trigger
Before changing HTML, CSS, web accessibility, browser API logic, browser-side JavaScript/TypeScript, layout, loading states, animations, forms, browser security/sanitization, media interactions, WebView behavior, responsive UI or Core Web Vitals.

Do **not** use for purely backend API, SQL, Android native-only code, security policy, repo/CI/DNS or documentation changes unrelated to a web surface.

## Recommended workflow (manual/authorized developer environment)
1. Check the repo-specific browser/runtime policy in root `AGENTS.md` and existing test suite. Preserve existing frameworks, security controls and product requirements.
2. If the approved developer environment has Node >= 22, outbound npm access and permission to execute the pinned package, search one narrow capability (2-5 terms) before implementation:
   ```sh
   npx -y modern-web-guidance@1.0.0 search "responsive data table"
   ```
3. Read matching descriptions. Retrieve **only** relevant guide IDs (do not invent IDs):
   ```sh
   npx -y modern-web-guidance@1.0.0 retrieve "<actual-guide-id>"
   ```
   Refine the search once if necessary. If no relevant guide is found or npm/network access is unavailable, use existing project standards and verified web platform docs; report the omission.
4. Follow the guide **only if** compatible with the declared supported browsers and app security model. Apply feature detection/graceful degradation for features not Baseline Widely Available and verify behavior on older target WebViews. Do not force a new dependency, a speculative polyfill or a rewrite merely to use a feature.
5. Include accessibility (semantic HTML, focus order, keyboard/D-pad, reduced motion), performance (INP/LCP/CLS), SSR/client boundaries, RTL, privacy/security and responsive checks as applicable.
6. For an explicitly broad legacy-modernization request only, an approved developer can run:
   ```sh
   npx -y modern-web-guidance@1.0.0 legacy-scan . --json
   ```
   Review all findings for false positives and valid fallbacks. Never run scanners automatically in CI or silently change code to attain zero findings.
7. In the PR summary cite retrieved guide ID(s), what was used, measured test evidence, browser support, fallbacks, and any skipped guidance. Do not claim the CLI was executed unless it actually was.

## Security and operations
- **No** network package fetch, plugin installation, package.json edits, remote execution, CI workflows or production operations are authorized by this instruction alone.
- Do not run `npx` with elevated privileges or install `@latest` automatically. Review npm/source integrity and request approval in restricted environments.
- Do not relax Content Security Policy, token handling, tenant isolation, Chrome extension permissions or Android device-consent controls.
- This instruction is a review-time development aid. It is not a runtime library, cloud service, product feature or a guarantee of WebView compatibility.
