# electron36-vesktop

This repository provides a custom Electron build for Arch Linux, with a specific patch to improve integration with PipeWire and PulseAudio on Linux systems.

## Why Patch Electron?

By default, Electron apps do not have a unique name or icon in PipeWire and PulseAudio streams. This is a long-standing issue tracked in the Electron project: [electron/electron#27581](https://github.com/electron/electron/issues/27581). As a result, all Electron-based applications appear as "Chromium" in audio management applications like pavucontrol. This makes it impossible to set different default volumes or default audio devices for each application, since all streams are grouped under the same name.

## What Does This PKGBUILD Change?

This PKGBUILD applies a patch to Chromium's `pulse_util.cc` file (used by Electron) to set a unique `PRODUCT_STRING` and `kBrowserDisplayName` for the build. Specifically, it changes these values from the generic "Chromium" to "Vesktop". This ensures that when using audio management tools (e.g., pavucontrol), the application is correctly identified by its own name and icon, rather than the default Chromium/Electron branding.

## Patch Details

The patch modifies the following in `media/audio/pulse/pulse_util.cc`:

- `kBrowserDisplayName` is set to `"vesktop"` instead of `"chromium-browser"`.
- `PRODUCT_STRING` is set to `"Vesktop"` instead of `"Chromium"`.

This change is essential for better user experience and application identification in modern Linux desktop environments, especially for managing audio streams independently.

## References
- [electron/electron#27581](https://github.com/electron/electron/issues/27581)
- [Arch Linux PKGBUILD documentation](https://wiki.archlinux.org/title/PKGBUILD)

---
Maintainer: Sophie Langer <sophie@lungoo.dev>
