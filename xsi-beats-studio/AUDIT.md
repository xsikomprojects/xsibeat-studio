# Xsi Beats Studio — audit and release notes

## Findings addressed

- **Imported-track metadata looked like analysis but was generated from the filename.** Replaced it with on-device heuristic BPM, key, energy and waveform estimation using Web Audio. Low-confidence/non-tonal audio reports `Unknown` rather than forcing a key. Genre/vibe and AlbatroS-specific features remain visibly demo/simulated.
- **Imported audio and session choices were lost after reload.** Local audio blobs now persist in IndexedDB; theme, language, deck selections, pitch, loop/sync, crossfader, Smart Set order and selected controls auto-save locally. Tracks can be removed from the local library.
- **No real mix recording path existed.** Added local master-bus recording with `MediaRecorder` where supported, download on stop, a recording timer and feedback when unsupported.
- **No keyboard help or session save control existed.** Added `Space`, `Shift+Space`, `R` and `Ctrl/Cmd+S` shortcuts, with a help dialog and manual local-save button.
- **Audio/context setup and local deletion paths could fail quietly.** Guarded Web Audio initialization/resume/recording support; added feedback for local storage and analysis failures; delayed object-URL revocation after downloads.
- **The brand and legal pages were missing.** Added the supplied XsiKOM logo, Impressum and a privacy notice for this local-first prototype, with footer links.
- **Deployment configuration was Netlify-oriented, despite the requested Vercel target.** Replaced it with Vercel static config, clean legal-page URLs, device-permission/security headers and a PWA shell cache.

## Verification performed

- Application JavaScript and service worker parse with `node --check`.
- HTML parses with `lxml`; IDs are unique and local asset references resolve.
- Vercel config and PWA manifest parse as JSON; XsiKOM logo SVG parses.
- i18n scan found all 102 data-attribute keys in the translation tables.
- Local DSP fixture returned 120 BPM / C major for a synthetic tonal rhythm and `Unknown` for broadband noise.
- Served the app, legal pages, logo, manifest and service worker locally and verified HTTP 200 responses.

## Still requires external setup

- Real AlbatroS inference/mastering/stem backend and approved streaming-platform OAuth integrations.
- A valid Vercel credential with access to the account/team that owns `xsikomdigitalprojects.app`. The latest credential validation returned **Invalid credentials**; project/domain reads also returned **Access denied**. No project creation, deployment or DNS/domain change was attempted.
- After access is restored, deploy the static project, assign **`beatstudio.xsikomdigitalprojects.app`**, and follow Vercel's exact DNS instructions at the registrar. The connector cannot provide deployment/domain outcomes while its credential is rejected.
- Review the privacy statement against the actual Vercel account's region, logging and data-processing agreement before public launch.
