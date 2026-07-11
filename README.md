# PixelGhost Privacy Policy

- **Effective date:** July 11, 2026
- **Extension operator:** Sagrid, operated by Abhishek Singh
- **Privacy and support contact:** <codecube99@gmail.com>

PixelGhost is a local-first browser extension that places user-selected
reference images over web pages for visual comparison. This policy describes
the data the extension handles, why it handles it, where it is stored, and the
choices available to users.

In this policy, “PixelGhost,” “we,” and “us” refer to the extension operator
identified above.

## Summary

- PixelGhost does not require an account.
- PixelGhost has no developer-operated data server, analytics, advertising,
  tracking, or telemetry.
- Workspace data and images are stored locally in the user's Chrome profile.
- PixelGhost handles the current page URL only to restore the workspace saved
  for that page.
- Clipboard image access is optional and occurs only after a user invokes a
  paste action.
- If a user supplies an HTTPS image URL, the browser requests that image
  directly from the server chosen by the user.
- PixelGhost renders overlays into the current page. Scripts running on that
  page may be able to inspect or remove the rendered elements and displayed
  image data.

## Data PixelGhost handles

PixelGhost handles the following information to provide its overlay-comparison
features:

| Data | How it is used |
| --- | --- |
| Current page URL | Associates an autosaved workspace with the page where the user created it. The URL fragment is removed; the scheme, host, path, and query string remain part of the local workspace key. |
| User-selected overlay images | Displays local files, folder selections, clipboard images, and user-supplied remote images as overlays. Local image bytes and thumbnails may be stored for restoration. |
| Image and project names | Labels layers and user-created named project snapshots. A local file's name may be used as its layer label. |
| Overlay state | Restores layer order, selected layer, visibility, lock state, opacity, blend mode, X/Y position, and scale. |
| Widget and display preferences | Restores widget collapse state, layer-list collapse state, and light/dark theme. The popup's visibility toggle applies live; widget position and hidden state reset on page load. |
| Privacy-consent record | Records the policy version, acceptance, and acceptance time so the first-use disclosure is not shown on every popup open. |

PixelGhost does not read or store the text of visited pages, form entries,
passwords, authentication cookies, financial information, health information,
personal communications, or a general browsing-history list. The content
script observes page geometry, scrolling, pointer input, and keyboard input as
needed to render and directly manipulate the overlay; it does not retain an
activity log.

User-selected images and project labels may themselves contain personal or
sensitive information. PixelGhost processes that content only for the
user-requested overlay and project features.

## Clipboard access

PixelGhost can receive an image through an ordinary paste event when the user
presses `Ctrl+V` in the popup. If the user selects the **Paste** button,
PixelGhost asks Chrome for the optional `clipboardRead` permission at that
time. If permission is granted, the extension examines the available
clipboard formats and reads image data only. Non-image clipboard content is
not saved.

The user may decline optional clipboard permission and use file upload,
folder selection, an HTTPS image URL, or ordinary `Ctrl+V` paste instead.

## Remote image URLs

PixelGhost accepts only HTTPS URLs without embedded usernames or passwords
through its remote-image input. When a user adds such a URL, the URL is stored
locally and the browser requests the image from that user-selected server so
it can be displayed. The remote server may
receive information ordinarily associated with an HTTPS request, such as the
user's IP address, request time, browser request headers, and cookies Chrome
sends for that server under applicable browser and site rules. PixelGhost sets
`no-referrer` on every image element that can display a remote image, so it
does not send the viewed page's URL in the HTTP `Referer` header.

That server is selected by the user and is not operated by PixelGhost. Its
handling of request data is governed by its own privacy policy. PixelGhost
does not send local overlay images, project data, or the user's workspace to
that server.

## Visibility to the current page

To provide an on-page comparison, PixelGhost inserts overlay image elements
and a floating-widget host into the page being viewed. Scripts running on that
page may be able to find, inspect, modify, or remove those elements. Depending
on browser behavior, this can expose layer names, image references, comparison
state shown in the widget, and displayed local-image data to the page and to
third-party scripts the page includes.

This rendering does not send data to the PixelGhost operator, but it means the
current page is not a confidential boundary for a displayed design. Users
should use private or sensitive reference images only on pages and with page
scripts they trust.

## Where data is stored

PixelGhost stores data within the extension's browser storage on the user's
device:

- IndexedDB stores URL-keyed workspaces, local image blobs, thumbnails, and
  named projects.
- `chrome.storage.local` stores the privacy-consent record and widget/theme
  preferences.
- Extension-page `localStorage` stores the popup theme.

While an overlay is displayed, temporary image references and controls are
also rendered in the current page as described above. They are removed when
the overlay/controller is removed; the persisted copy remains in extension
storage until deleted under the retention rules below.

This data is not sent to or made available through a PixelGhost-operated
server. It is not intentionally synchronized between devices by PixelGhost.
Access to local extension data is subject to the security of the user's
browser profile, operating-system account, and device.

## How data is used

PixelGhost uses handled data only to:

1. display and control reference-image overlays;
2. restore the workspace associated with the current page URL;
3. save, list, load, and delete user-created projects;
4. remember extension display preferences and consent; and
5. maintain the security and reliability of those user-facing features.

PixelGhost does not use data for advertising, marketing, analytics,
profiling, creditworthiness, lending, or sale. It does not build a browsing
profile.

## Sharing and disclosure

PixelGhost does not sell user data. It does not transfer workspace data,
local images, URLs, settings, or clipboard images to the extension operator,
advertisers, analytics providers, or data brokers.

The limited exceptions are:

- rendering user-selected overlays and controls into the current page, where
  page scripts may be able to inspect them, as described above;
- a browser request to a user-selected HTTPS image server, as described
  above;
- information the user intentionally includes in a support request;
- disclosure required to comply with applicable law; or
- disclosure necessary to protect users, the extension, or others from
  malware, fraud, abuse, or a security threat.

Because PixelGhost has no data backend, its personnel cannot inspect locally
stored user data. Support personnel can see only information a user chooses to
send with a support request.

## Retention and deletion

Workspace data remains in local browser storage until the user removes the
relevant layers or workspace, clears the extension's stored data, resets the
browser profile, or uninstalls the extension. Named projects remain until the
user deletes them or clears extension data. Widget, theme, and consent
preferences remain until extension storage is cleared or the extension is
uninstalled.

Users can remove individual layers, remove all layers for a page, and delete
named projects from the extension interface. Chrome can remove all remaining
PixelGhost data when the extension is uninstalled. Users may also clear the
extension's site/storage data through Chrome's extension developer or browser
data controls where available.

The extension operator does not hold a server-side copy and therefore cannot
retrieve, export, correct, or delete local extension data on the user's
behalf.

## Security

PixelGhost packages its executable code with the extension and does not
execute remotely hosted code. User-entered remote image addresses are limited
to HTTPS. Persisted data is kept in extension storage, but displayed overlays
are deliberately rendered into the current page and are not isolated from all
page scripts. Local data is also subject to Chrome, browser-profile,
operating-system, and device security controls.

No local storage mechanism can guarantee absolute security. Users should not
add sensitive images on a shared or untrusted browser profile, should display
confidential designs only on pages they trust, and should use remote image
URLs only from servers they trust.

## External services and links

The extension may open its privacy-policy or support page in a normal browser
tab when the user selects the relevant link. The operator of that website may
process the visit under its own privacy policy. Chrome Web Store and the
Chrome browser may separately process installation, update, diagnostic, or
store activity under Google's policies; that processing is not performed by
PixelGhost.

## Children

PixelGhost is a professional design and development utility and is not
directed to children under 13 or the minimum age required by local law. The
extension does not knowingly request personal information from children.

## Chrome Web Store Limited Use

PixelGhost's use of information received from Google APIs adheres to the
Chrome Web Store User Data Policy, including the Limited Use requirements.
PixelGhost limits its use of user data to providing or improving its disclosed
single purpose and does not use or transfer user data for personalized
advertising, unrelated purposes, or creditworthiness or lending decisions.

## Changes to this policy

If PixelGhost's data practices change, this policy, the Chrome Web Store
privacy disclosures, and any required in-product disclosure will be updated
before the changed practice begins. The effective date at the top identifies
the current version.

## Contact

Questions, privacy requests, and security reports should be sent to:

<codecube99@gmail.com>

Because user workspaces are stored only on the user's device, do not attach
private overlay images or sensitive page URLs to a support request unless they
are necessary and the user intends to share them.
