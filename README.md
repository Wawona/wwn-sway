# wwn-sway

Wawona's port of **sway** — the i3-compatible wlroots Wayland compositor — to run
nested under Wawona on the Apple ecosystem and Android, App Store compliant.

> **Status: SKELETON.** flake + `registryFragment` skeleton + this port plan
> only. Build stubs fail intentionally; full port is downstream.

## Delivery model

sway is a wlroots compositor → runs **nested** (client of Wawona), never
replacing the Wawona compositor. wlroots' DRM/libinput backends are unused on
Apple/Android; sway uses its nested Wayland backend.

## Port plan

1. Toolchain via `wwn-toolchain` (`buildForIOS/macOS/Android`).
2. Compliance: no JIT / no external `fork+exec`, sandbox-safe runtime dirs,
   bundled default config, no `swaymsg` shelling out to arbitrary binaries.
3. wlroots dependency: build the nested-Wayland backend only.
4. Replace `dependencies/sway/stub.nix` with per-platform derivations; expose
   `sway-{ios,macos,android}`; register in Wawona.
5. `wwn-apt` lists `sway` `status: planned` → flip to `approved` post-review.

Convention: [wwn-* porting convention](https://github.com/Wawona/Wawona/blob/main/docs/2026-wwn-porting-convention.md).
