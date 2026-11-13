# Elden Ring 2.7.2.0 compatibility evidence

Measured on Windows on 2026-10-21, against the installed Worldwide executable:

- Steam build: 25827938; depot 1245621 manifest: 1925130620768035844.
- File/product version: 2.7.2.0.
- SHA256: `f9118fea2cfd8fa3901e8060bfadb1552cb2471771ded8a5b662c4e298ffb328`.

The unchanged vendored `crates/eldenring/mapper-profile.toml` resolved all 107
captures using upstream `tools/binary-mapper` from revision `893cdd37`.
99 addresses differ from the previous 2.7.1.0 table. The new table is generated
output, not an offset applied to the previous table. The mapper was built as a
standalone scratch package using its unchanged `main.rs` and the vendored shared
crate; this avoids resolving unrelated tools in the upstream workspace.

Reproduce with the upstream mapper:

```text
binary-mapper map --profile vendor/fromsoftware-rs/crates/eldenring/mapper-profile.toml --exe <eldenring.exe> --output rust > <mapper-output.rs>
python tools/audit_er_2720.py <eldenring.exe> <mapper-output.rs>
```

The audit requires `pefile`. It checks the executable hash, shipped function
signatures, data-reference counts and every generated table field. It does not
write executable bytes. The original executable stays local.

## Client addresses outside the generated bindings

| Purpose | RVA | Offline evidence |
| --- | --- | --- |
| AddItemFunc | `0x5618b0` | Shipped prologue; instructions at `0x561902` read the count through `rdx`, bound it to ten, then iterate entries at `0x561940`. The nearby prologue match at `0x564170` takes `edx` as an integer instead of a buffer pointer. |
| Inventory pointer slot | `0x3d6eae0` | 133 RIP-relative mov/lea references. |
| LuaWarp | `0x59af10` | Unique shipped signature match across `.text`. |
| Lua manager candidates | `0x3d6eed8`, `0x3d62060` | 264 and 30 RIP-relative mov/lea references. |
| FMG repository slot | `0x3d84588` | 236 RIP-relative mov/lea references. |
| FMG search | `0x2671370` | Unique shipped signature match across `.text`. |
| ChrAsm assignment | `0x245c00` | Shipped prologue and equipment-copy body: 22-entry loop beginning at `0x245c51`, followed by the parallel copy at `0x245c70`. |

All four data-slot counts exactly reproduce the previous table's documented
2.7.1.0 census at new addresses (+0x3020). This is relocation evidence, not a
runtime pointer readback. Existing signature and pointer guards remain enabled.

## Limits

This is offline binary evidence and automated-test coverage. No live-game test
has yet confirmed startup, item grant/suppression, warps, FMG injection or equipment
updates. Struct-layout parity is not established by the RVA mapper. The spell-slot
census retains the existing Tarnished baseline and is explicitly unmeasured on
2.7.2.0. Startup logs state that the addresses have not been live-game verified.
Japanese 2.7.2.x is not enabled without a corresponding executable and table.

The client-only 1.0.2.1 fixpack changes neither the seed contract nor persisted
state. All previous supported executable versions remain accepted.
