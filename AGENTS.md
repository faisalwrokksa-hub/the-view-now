# Development guidance — The View Now

Read `CONTRIBUTOR_MASTER_PROMPT.md` and the current README first; preserve the single-dashboard Home/Watch/Discover/Settings structure, existing working streams, market charts and deployment boundaries. 

## Modern Web Guidance
Use [the project integration skill](.agents/skills/modern-web-guidance/SKILL.md) for browser UI, CSS, accessibility, responsive layout and JavaScript updates. Its upstream CLI is **not automatically installed or run** by the presence of this file. Target TV remotes/D-pad and touch/mouse/keyboard. Preserve a fixed-viewport TV dashboard with focus visibility, no offscreen panels, and responsive layouts on 1920×1080, 1440×900, 1366×768, 768×1024 and 390×844. **Android 14 with WebView 113 was a reported physical test target:** do not adopt newly shipped Chromium/CSS features without detecting support or an inexpensive fallback verified on that WebView. If necessary, prefer established CSS over exciting but unsupported APIs. Do not weaken media-source checks, iframe restrictions or app security; third-party sites may deny embedding and that must be handled honestly.

No production deployment, signing, API key changes or browser feature claims without verified tests and release authorization.
