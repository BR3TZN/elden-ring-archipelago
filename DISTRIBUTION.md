# Distribution

Players start at [Peliarch Elden Ring](https://peliarch.ca/elden-ring/) and download the current matched bundle from [Peliarch Downloads](https://peliarch.ca/downloads#elden-ring). The public source and player documentation live at [er-archipelago-public](https://git.peliarch.ca/alaric/er-archipelago-public). Do not point players to the private working repository.

## A matched pair

The `eldenring.apworld` and `eldenring_archipelago.dll` must come from the same release. The apworld puts a contract hash in the seed's slot data, and the client checks it when connecting. A mismatch is reported as `VERSION MISMATCH`; install the matching client or regenerate with the matching apworld before playing. Packaging both in one player bundle makes the correct pairing easy to find. A host who only generates seeds may use a separately published apworld from that same release.

Do not mirror or re-upload the bundle in Discord or on another mod page. Link to [Peliarch Downloads](https://peliarch.ca/downloads#elden-ring) so players can get the current package, its release notes, and the matching world and client.

## The options builder

The [browser builder](https://peliarch.ca/er/) explains the options and previews seed size. An offline copy may accompany a release. A YAML is still interpreted by the apworld installed by the host; if generation warns about unknown options, use the template or builder for that release and update the host's apworld. The builder does not replace the host's installed world.

## What the bundle contains

The player bundle carries the apworld, runtime client, me3 profile, documentation, and companion map integration. The client and apworld are original MIT-licensed components. The MapForGoblins companion has its own upstream license and notices, which remain with it in `me3/MFG-LICENSE.txt`. [Attribution](ATTRIBUTION.md) and [Provenance](../PROVENANCE.md) describe the other credits and data boundaries. The bundle does not include FromSoftware game assets or thefifthmatt's randomizer.

The map companion is built from the source and inputs pinned for the release. Its provenance is recorded in `MFG-VERSION.json` and the packaged provenance file. Check those pins during release preparation; do not substitute a hand-copied DLL.

The pin check is an actual release gate:

- `python tools/mfg_pin.py --check` fails if the pinned MapForGoblins fork commit trails its head or the world's preset disagrees with the fork's preset script. Run it before packaging.
- `python tools/mfg_pin.py --bump` moves the source commit to the fork's head when its change belongs in this release. The separately pinned private inputs move only when those inputs change.

Review and commit a needed pin bump alongside the world change that depends on it. The packaged DLL and its provenance must then come from those pins.

## Release checks

The private Forgejo source has separate manual source-smoke and private-corpus workflows; their scopes are documented in [Forgejo CI](../docs/FORGEJO-CI.md). Source smoke does not prove full game-data regeneration, and neither workflow builds the Windows DLL. A player release needs the matching Windows client build, the private-corpus gate, package integrity checks, and a review of the resulting archive and download links. Publish only a package whose components were checked together.

For setup help, use [Peliarch Help](https://peliarch.ca/help?game=er). For run discussion, use the [Peliarch Discord](https://discord.gg/RVuXe9GpuH).

Public 1.x packages retain the native game icon and include only player-side AP Flower builders. Extracted menu atlases, game archives, and input databases are forbidden in both player and source archives. The packager rejects them and always stages detection JSON from the generated world source, even if a local me3 folder contains older copies.
