Elden Ring Archipelago 1.0.2.1 — Worldwide game 2.7.2.0 compatibility

UPDATING AN EXISTING 1.0.2 INSTALLATION
Close Elden Ring. Replace eldenring_archipelago.dll in your existing me3/profile
installation with the DLL in this archive. Keep your profile, server settings,
MapForGoblins adapter and saves. No new seed or YAML is required for an existing
compatible run. Hosts may install the separately supplied eldenring.apworld for
new generations. This is an update package, not a complete first-time installer.
For a first-time installation, install the 1.0.2 player bundle, then this update.

Supports Worldwide game 2.7.2.0 and retains all previously supported executables.
Japanese 2.7.2.x is not enabled. No seed contract or saved-state migration.

VALIDATION
107 binding addresses mapper-generated against Steam build 25827938; client
addresses independently audited. Windows release build, 1,760 client/support
tests, one binding dispatch test, 136 world tests (884 subtests), formatting and
default/profile Clippy pass. The actual executable version resource was tested.
Live gameplay, runtime pointer readback and struct-layout parity remain unverified.
This replacement DLL is unsigned. Existing signed components are unchanged.

Client source commit: 97abc990ae6b7ef46ab627c76db631dce602b84b
Public client source: bee99e81621e8ec0d2318eed4c5b3a9e229d1d14
Public world source: 909884733f7824062f7dda7c9346643ba36b2050
