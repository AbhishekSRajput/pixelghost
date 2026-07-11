# PixelGhost

PixelGhost is a Manifest V3 browser extension for comparing a reference image
with a live web page. Designers and frontend developers can place image
overlays over normal HTTP and HTTPS pages, then adjust their position,
opacity, scale, visibility, lock state, and blend mode.

The extension is local-first. Page workspace data, overlay images, named
projects, and comparison settings are stored in the browser profile. There is
no PixelGhost account, analytics service, advertising SDK, or
developer-operated data server. See [PRIVACY.md](PRIVACY.md) for the complete
behavioral policy.

> **Release status:** this repository is not cleared for public store
> submission. Resolve every stop-ship item in
> [docs/PROVENANCE.md](docs/PROVENANCE.md) and
> [docs/CHROME_WEB_STORE.md](docs/CHROME_WEB_STORE.md) before publishing or
> making non-infringement or clean-room claims.

## Features

- Add overlays from local image files, a folder, the clipboard, or an HTTPS
  image URL.
- Manage multiple layers from the popup and the on-page floating widget.
- Adjust opacity, X/Y position, scale, visibility, lock state, and CSS blend
  mode.
- Lock an overlay for scroll-based comparison or leave it viewport-relative.
- Autosave a workspace for each page URL and save reusable named projects.
- Use light and dark themes and the `Ctrl+Shift+Down` popup shortcut.

PixelGhost works on ordinary `http://` and `https://` pages. Browser-internal
pages, the Chrome Web Store, and other restricted pages do not allow content
script injection.

## Requirements

- Node.js 22.x recommended
- npm
- Chromium 127 or newer for the packaged extension

## Development

Install the locked dependency tree and validate the project:

```sh
npm ci
npm run typecheck
npm run build
npm run e2e
npm run release:check
```

`release:check` is intentionally stricter than the test suite. It rejects a
store release while legal/provenance gates, public URLs, required listing
assets, or reviewed package invariants remain unresolved.

`npm run e2e` tests the existing `dist/` directory, so run the build first.
The browser harness defaults to Microsoft Edge on Windows. Set `BROWSER_BIN`
to a compatible Chromium executable when it is installed elsewhere.

For popup-only UI iteration:

```sh
npm run dev
```

The Vite page does not provide the full extension environment. Test content
scripts, permissions, persistence, the service worker, and the floating widget
by loading the built extension:

1. Run `npm run build`.
2. Open `chrome://extensions` in a Chromium browser.
3. Enable **Developer mode**.
4. Select **Load unpacked** and choose `dist/`.
5. Open a normal HTTP or HTTPS page and accept the first-use privacy
   disclosure in the popup.

## Project structure

```text
.
|-- manifest.config.ts       Manifest V3 configuration and permissions
|-- vite.config.ts           Vite, React, and CRXJS build configuration
|-- public/icons/            Packaged extension icons
|-- scripts/                 Repository maintenance and asset scripts
|-- src/
|   |-- popup/               React popup entry point and layout
|   |-- components/          Popup controls and project UI
|   |-- hooks/               Zustand state, sync, persistence, theme, consent
|   |-- content/             Page renderer and Shadow DOM floating widget
|   |-- background/          MV3 service worker and persistence bridge
|   `-- lib/                 Shared types, messages, storage, and utilities
|-- e2e/                     Chromium extension end-to-end scenarios
`-- docs/                    Store-launch and provenance documentation
```

PixelGhost runs in three separate JavaScript contexts:

- The React popup owns the editor UI and its Zustand view of state.
- The content script owns page overlay DOM and the framework-free widget.
- The background service worker bridges widget mutations and URL workspace
  hydration to extension IndexedDB.

Shared contracts belong in `src/lib`. Changes to state or messages often need
coordinated updates in all three contexts.

## Storage and permissions

- IndexedDB stores URL-keyed workspaces, image blobs, thumbnails, and named
  projects.
- `chrome.storage.local` stores first-use consent and global widget/theme
  preferences.
- Popup `localStorage` stores the selected theme after first-use consent.
- HTTP/HTTPS page access is used to render overlays and associate a locally
  saved workspace with the current page URL.
- Rendered overlay elements and widget data live in the current page DOM while
  active and may be inspectable by scripts on that page. Use confidential
  designs only on pages you trust.
- Clipboard read access is optional and requested only when the user selects
  the **Paste** action. Ordinary `Ctrl+V` paste remains available without the
  optional permission.

## Contributing

Read [CONTRIBUTING.md](CONTRIBUTING.md) before changing the extension. It
documents the runtime architecture, synchronization invariants, IndexedDB
schema, common workflows, manual checks, and pull-request checklist.

Only submit code, artwork, copy, screenshots, or other material you created or
have the right to contribute under the project's license. Every commit must
include a Developer Certificate of Origin sign-off:

```sh
git commit -s -m "Describe the change"
```

## Release documentation

- [Privacy policy](PRIVACY.md)
- [Chrome Web Store submission runbook](docs/CHROME_WEB_STORE.md)
- [Internal provenance register](docs/PROVENANCE.md)
- [Third-party notices](THIRD_PARTY_NOTICES.md)

## License

PixelGhost is licensed under the Apache License 2.0. See [LICENSE](LICENSE).
Third-party components retain their own licenses as listed in
[THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
