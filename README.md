# Playbook — join and your machine powers the server

A **decentralised Minecraft server**: one shared world, no rented datacenter.
The coordinator is a tiny always-on Raspberry Pi; the actual game simulation
runs on **the players' own machines**. When you connect, your computer
automatically becomes a compute node that hosts the chunks around you — that
is the price (and the point) of playing here.

- **Minecraft:** 1.20.1 (Fabric)
- **Server address:** `practically-spearhead.tun.ply.gg`

## Install (once, ~2 minutes)

1. **Install Fabric Loader** for Minecraft 1.20.1 — run the official
   installer from <https://fabricmc.net/use/installer/> (select game version
   1.20.1, leave everything else default).
2. **Download both jars** from this repo and put them into your `mods`
   folder (`.minecraft/mods`, or your launcher instance's `mods` folder):
   - [`playbook-companion-0.1.0.jar`](mods/playbook-companion-0.1.0.jar)
     (direct: [download](https://github.com/saneowlprojects/towards-distribution-files/raw/main/mods/playbook-companion-0.1.0.jar))
   - [`fabric-api-0.92.12+1.20.1.jar`](mods/fabric-api-0.92.12+1.20.1.jar)
     (direct: [download](https://github.com/saneowlprojects/towards-distribution-files/raw/main/mods/fabric-api-0.92.12%2B1.20.1.jar))
3. Add the server address above in Minecraft and **join**.

That's everything. On first launch the companion automatically downloads the
Playbook pack (the node software + its configuration) from the server
itself, starts a Minecraft server on your machine in the background, and
connects you to it. No ports to forward, no configs to edit.

## What to expect

- **First join takes a minute or two.** Your node downloads the server
  software (~50 MB) and generates the world. You may see
  *"Your host node is still starting its server…"* — the mod reconnects by
  itself; just wait on that screen.
- **Your machine hosts the world around you.** Mobs, redstone, world
  generation near you are computed by your CPU. Chunks that other players
  stand in are computed by their machines, all stitched into one world.
- **The node lives exactly as long as your play session.** Leaving the
  server or closing the game stops it — nothing stays running in the
  background.
- **The pack is required.** Clients without the companion are kicked after
  ~10 seconds: everyone contributes their fair share of compute.

## Troubleshooting

- **Stuck on "no host node online":** the coordinator (Raspberry Pi) may be
  offline, or the pack failed to download. Try rejoining; if it persists,
  ping the operator.
- **Logs** (attach these when asking for help):
  - `.minecraft/playbook/nodemanager.log` — node registration/boot
  - `.minecraft/playbook/server/server-console.log` — the local game server
- **Low-end machine?** Hosting adds ~1–2 GB of RAM usage while you play.
- Deleted your `playbook` folder by accident? No problem — it re-downloads
  on the next launch.

## Licenses

- Playbook Companion: MIT (built from the private Playbook sources).
- Fabric API is redistributed here under the
  [Apache License 2.0](https://github.com/FabricMC/fabric/blob/1.20.1/LICENSE) —
  source: <https://github.com/FabricMC/fabric>. You can always get the
  original from [Modrinth](https://modrinth.com/mod/fabric-api).
