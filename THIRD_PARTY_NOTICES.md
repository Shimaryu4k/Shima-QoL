# Third-party components

Shima QoL's settings use genuine **Dear ImGui 1.89.7**, through its **cimgui** C ABI.
The native Windows x64 binary is embedded inside `ShimaQoL.dll` as the manifest
resource `ShimaQoL.Native.cimgui.dll`. The matching MIT notices and this document
are also embedded under `ShimaQoL.Licenses.*`, so distributing the single DLL
retains the required notices.

On first opening settings, the mod extracts verified bytes under
`%LOCALAPPDATA%\ShimaQoL\Native\<SHA256>\shimaqol_cimgui_1_89_7_8a8464f3.dll`.
Windows loads that cache copy using an absolute path. Only the managed
`ShimaQoL.dll` needs to be installed in BepInEx; this is a single-file
distribution with an automatic native cache, not a disk-free native loader.

- Dear ImGui: https://github.com/ocornut/imgui/tree/v1.89.7 — MIT; see `LICENSE-imgui.txt`.
- cimgui: https://github.com/cimgui/cimgui — MIT; see `LICENSE-cimgui.txt`.
- Binary distribution: ImGui.NET NuGet package **1.89.7.1**, entry
  `runtimes/win-x64/native/cimgui.dll`, obtained from
  https://api.nuget.org/v3-flatcontainer/imgui.net/1.89.7.1/imgui.net.1.89.7.1.nupkg.
  The managed ImGui.NET wrapper is not required or distributed.
- Native binary SHA256: `8A8464F3707D59ED5D63D3102EB81D1A60BF844745DD2D87F064940DFB87108C`.

The native API declarations and structure prefixes follow the upstream header
preserved at `vendor/dear-imgui/imgui.h`. The wrapper, menu and Unity rendering
adapter in `src` are part of this project. `SOURCE.json` records the downloaded
package's provenance and checksum.

The optional Segoe UI font is read from Windows' installed fonts at runtime and
is not redistributed. Dear ImGui's built-in font is the fallback.

REFramework was a reference for the UI:
https://github.com/praydog/REFramework and https://refdocs.praydog.com/api/imgui.html.
Its `dinput8.dll` and RE Engine hooks are not distributed or loaded by this mod.

Action input filtering, Stack Splitter and Automation Chest hooks use the Harmony library supplied by BepInEx 5.
Harmony and Sun Haven/Unity assemblies are compile references and are not
redistributed in this package.

Automation Chest uses the Mirror networking and ZeroFormatter serialization
libraries supplied with Sun Haven. They are read-only build references; their
assemblies and game code/assets are not redistributed in this package.
