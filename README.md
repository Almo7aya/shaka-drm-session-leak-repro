# Shaka Player DRM session leak repro (temporary)

Live page: https://almo7aya.github.io/shaka-drm-session-leak-repro/

When a license request fails while another session is still open, Shaka Player's `DrmEngine` removes that
`MediaKeySession` from its list without closing it, and `destroy()` only closes the sessions still on the list. The
page plays the Shaka demo asset "Multi-DRM, multi-key" (one key per representation, so several sessions), makes
license requests fail, destroys the player, and reports which sessions are still open.

Direct links (open in Chrome or Edge):

| Shaka build | License requests fail | License requests succeed (control) |
|---|---|---|
| 4.16.10 | [run](https://almo7aya.github.io/shaka-drm-session-leak-repro/?version=4.16.10&mode=fail&run=1) | [run](https://almo7aya.github.io/shaka-drm-session-leak-repro/?version=4.16.10&mode=ok&run=1) |
| 5.3.1 | [run](https://almo7aya.github.io/shaka-drm-session-leak-repro/?version=5.3.1&mode=fail&run=1) | [run](https://almo7aya.github.io/shaka-drm-session-leak-repro/?version=5.3.1&mode=ok&run=1) |
| nightly (`main`) | [run](https://almo7aya.github.io/shaka-drm-session-leak-repro/?version=nightly&mode=fail&run=1) | [run](https://almo7aya.github.io/shaka-drm-session-leak-repro/?version=nightly&mode=ok&run=1) |
| `main` + fix | [run](https://almo7aya.github.io/shaka-drm-session-leak-repro/?version=fix&mode=fail&run=1) | [run](https://almo7aya.github.io/shaka-drm-session-leak-repro/?version=fix&mode=ok&run=1) |

`builds/shaka-player.fix-drm-close-dropped-sessions.debug.js` is a debug build (`python3 build/build.py --mode debug`)
of Shaka Player `main` at `612cdb4c8` with the fix applied.

This repository only exists for the bug report and will be deleted once it is resolved.
