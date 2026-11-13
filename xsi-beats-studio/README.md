# Xsi Beats Studio

Static, local-first DJ-studio prototype for the Xsi Beats Studio / AlbatroS concept. No build step or npm dependencies are required. Review `AUDIT.md` for findings and verification notes, or `VERCEL_DEPLOY_GUIDE.md` for the release checklist.

## Run locally

```bash
python3 -m http.server 8000 --bind 0.0.0.0
```

Open `http://localhost:8000`. Browser hardware APIs require a secure context: HTTPS when hosted, or `localhost` for local development.

## Product features

- Two-deck mixer with pitch, cue, loop, equal-power crossfader, sync, visualizer and phrase suggestions.
- Import local audio, playback through Web Audio, and local mix capture/download through `MediaRecorder` where supported.
- Imported audio gets on-device heuristic BPM/key/energy estimates and a waveform preview. This is signal-processing assistance, not an AI model or guaranteed musicological analysis.
- Imported audio blobs persist in browser IndexedDB; session preferences and deck/queue selections auto-save locally. The browser's site data controls can clear this local library.
- Library search, per-track deck loading, remove-from-library action, drag-and-drop import and quota/error handling.
- Keyboard controls: `Space` Deck A, `Shift+Space` Deck B, `R` start/stop recording, `Ctrl/Cmd+S` save session.
- Theme switcher: Classic Vinyl, Minimal Producer and Afrocentric; UI languages: German, English, French, Spanish, Portuguese, Yoruba and Swahili.
- Demo modules: harmonic suggestions, Smart Set ordering, mastering/stem/arrangement previews, Afrobeat sequencer and crowd feedback.
- Bluetooth audio-output selection where supported; BLE GATT controller connect/disconnect; browser-visible network status and Wi-Fi setup guidance.
- User-provided XsiKOM logo, Impressum and a privacy-notice draft.
- PWA manifest, app-shell service worker cache, Vercel config and response headers.

## Deploy on Vercel

1. Import this folder/repository into Vercel as a static **Other** project.
2. Keep the project root as the folder containing `index.html` and `vercel.json`; no build command or install command is needed, and the output is the project root.
3. Add `beatstudio.xsikomdigitalprojects.app` to the Vercel project and follow Vercel's DNS instructions at the domain registrar. HTTPS is required for Web Bluetooth and audio-output selection.
4. The project includes `vercel.json` for clean legal-page URLs and security/device-permission headers. Confirm the final host configuration and check that `/impressum` and `/datenschutz` load after deployment.

## Legal and privacy review

The Impressum uses the company/contact details supplied by the owner. The Datenschutzerklärung reflects the current local-first demo and expected Vercel hosting. Before public launch, verify the actual Vercel data region/log retention and provider contract against the deployed account; update the privacy text if the app's data flows change.

## Prototype boundaries

Sample-track BPM/key/genre values are illustrative metadata. Imported files receive approximate client-side BPM/key/energy estimates; genre/vibe, AlbatroS recommendations, mastering, stem separation, arrangement analysis and crowd scoring remain demo logic, not a trained AI service. Uploaded local audio is played in the browser. Direct Spotify, YouTube, SoundCloud, TikTok and Suno OAuth/API upload flows are not implemented. The app does not send local audio or BLE device details to its own backend. Production integrations require a secure backend and provider approval; never store OAuth secrets in browser code.

Web Bluetooth is for compatible BLE/GATT controllers—not Bluetooth headphones. For Bluetooth audio, pair the device in the operating system and select it in the browser if the browser exposes `selectAudioOutput()` and `AudioContext.setSinkId()`. Browsers do not let websites scan for or join Wi-Fi networks; the Wi-Fi card only reports browser-exposed connectivity state.
