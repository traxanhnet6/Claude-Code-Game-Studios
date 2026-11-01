---
name: build-android
description: "Package the verified web build into a signed Android APK (online or offline variant), verify signature/permissions/size, and report device evidence."
argument-hint: "[online|offline] [graphics-tier]"
user-invocable: true
allowed-tools: Read, Glob, Grep, Write, Edit, Bash
model: sonnet
---

# Build Android APK

Packages the game's verified web build into an Android APK under the authority of the `android-specialist` agent. This skill exists in this fork because the studio's projects ship to Android as well as the web; the stock template only covered Godot/Unity/Unreal.

## Preconditions — all must hold before packaging

1. **Frozen input.** The input is a verified deploy/staging tree at a known commit. If the source tree is being edited by anyone, stop — packaging a moving tree ships other people's half-work.
2. **Variant chosen.** `online` (WebView loads the live URL; content follows web deploys) or `offline` (assets bundled; no INTERNET permission; fully playable offline). Default: ask once if not specified.
3. **Graphics tier chosen for offline builds.** Bundle exactly one tier (e.g. the project's medium tier) unless the user explicitly accepts the size of bundling more.
4. **Identity set.** Package id, versionName, versionCode (strictly greater than the last shipped build).

## Steps

1. **Snapshot the input** — record the commit/tree hash of the web build being packaged; the build report names it.
2. **Assemble the wrapper** — WebView shell with DOM storage enabled, orientation unlocked unless the design locks it. For offline builds, copy the asset tree minus every non-target graphics tier.
3. **Declare permissions** — only what the variant needs. Offline: none beyond defaults. Online: INTERNET only.
4. **Build and sign** — use the project's established toolchain and keystore (keystore never enters the repo or the report; report only that signing succeeded).
5. **Verify — all four, no exceptions:**
   - `apksigner verify` passes.
   - `aapt dump badging` shows the expected package id, versionName/versionCode, and exactly the intended permission list.
   - Final APK size in bytes, with the dominant content named.
   - Offline builds: grep the merged manifest to prove INTERNET is absent.
6. **Device evidence** — install and launch on a real device or emulator; confirm the first playable screen renders and input works; retain a screenshot. If this step cannot run, the report must say so in its first lines — an untested-on-device APK is a known limitation, not a detail for the footnotes.

## Build report (required output)

One short report: variant, input commit, file path, size, package id, version, permissions, signature result, device-evidence status, and the build's one honest weakness. No build is "done" without this report; no report claims a check that was not actually run.
