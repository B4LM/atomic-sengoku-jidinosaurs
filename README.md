# Atomic Sengoku Jidinosaurs

![Minecraft 1.20.1](https://img.shields.io/badge/Minecraft-1.20.1-3c8527)
![Forge 47.4.28](https://img.shields.io/badge/Forge-47.4.28-1e2d4f)
![Launcher: Prism](https://img.shields.io/badge/Launcher-Prism-6e4ac9)

Samurai, dinosaurs, dragons and nuclear reactors. This repo is our modpack: Prism Launcher reads it every time you click **Launch** and keeps your mods and configs in sync with the server automatically.

---

## Quick start

You need the file **`Atomic-Sengoku.zip`** from the pack admin.

1. **Install [Prism Launcher](https://prismlauncher.org/download/windows/)** and start it. Let it download Java automatically.
2. **Sign in:** account button (top right) -> **Manage Accounts** -> **Add Microsoft**.
3. **Import:** **Add Instance** -> **Import** -> **Browse** -> pick `Atomic-Sengoku.zip` -> **OK**.
4. **Play:** select the instance and click **Launch**. The first time, a small *packwiz* window downloads all mods (a few minutes), then Minecraft starts.
5. **Join:** **Multiplayer** -> **Add Server**, same address as before.

That's it. From now on every **Launch** checks for updates by itself.

> No zip? Use the [manual setup](#manual-setup-without-the-zip) further down.

---

## The rules

- **Always start the game through Prism.** The old CurseForge version doesn't get updates and won't match the server anymore.
- **Don't add or remove mods yourself.** If your mods differ from the server's, you can't join. Ask the pack admin and they'll add it for everyone.
- **Updates are automatic.** When a mod is added or updated, you get it on your next Launch.

---

## The one mod you might have to download yourself

**Epic Knights: Japanese Armory** can't be downloaded automatically (the author blocked it). **It's already inside `Atomic-Sengoku.zip`**, so normally you never notice.

If Launch stops with *"This mod is excluded from the CurseForge API and must be downloaded manually"*:

1. Open the [mod's file page on CurseForge](https://www.curseforge.com/minecraft/mc-mods/epic-knights-japanese-armory/files/5294116) and click **Download**.
2. Save it with exactly this name: `[1.20.1-forge]-Epic-Knights-Japanese-Armory-1.6.2.jar`
3. Put it in the instance's mods folder: right-click the instance -> **Folder** -> `minecraft` -> `mods`.
4. Click **Launch** again.

If the error names a **different** mod, tell the pack admin.

---

## Extras

- **Shaders:** Options -> Video Settings -> Shader Packs -> **Complementary Reimagined**. Turn them off if the game gets laggy.
- **Keep your old keybinds and video settings:** copy `options.txt` from your old CurseForge instance folder into Prism's instance folder (right-click the instance -> **Folder** -> `minecraft`).

---

## If something goes wrong

| Problem | Fix |
|---|---|
| Can't join: *mod mismatch*, *registry* or *missing* errors | Close Minecraft and click **Launch** again so the newest version gets downloaded. Still broken? Send the error to the pack admin. |
| *"Must be downloaded manually"* | See [the one mod you might have to download yourself](#the-one-mod-you-might-have-to-download-yourself). |
| Prism says the *pre-launch command failed* | Usually a short internet or GitHub hiccup. Wait a minute and try again. |
| Crash or freeze while loading | Right-click the instance -> **Edit** -> **Settings** -> **Java**: set **Maximum memory** to `6144` MB (`4096` if your PC has 8 GB RAM or less). Still crashing? Send the newest file from the `crash-reports` folder to the pack admin. |

---

## Manual setup (without the zip)

1. Install Prism Launcher and sign in (steps 1 and 2 of the [quick start](#quick-start)).
2. **Add Instance** -> **Vanilla** -> **1.20.1**, name it `Atomic Sengoku`, click **OK**.
3. Right-click the instance -> **Edit** -> **Version** -> **Install Forge** -> **47.4.28**.
4. Download `packwiz-installer-bootstrap.jar` from the [newest release](https://github.com/packwiz/packwiz-installer-bootstrap/releases) (under *Assets*).
5. Right-click the instance -> **Folder**, open `minecraft` (or `.minecraft`) and put the jar there.
6. Right-click the instance -> **Edit** -> **Settings**:
   - **Java** tab: tick **Memory**, set **Maximum memory** to `6144` MB.
   - **Custom commands** tab: tick the box and paste into **Pre-launch command**:
     ```
     "$INST_JAVA" -jar packwiz-installer-bootstrap.jar https://raw.githubusercontent.com/B4LM/atomic-sengoku-jidinosaurs/main/pack.toml
     ```
7. Click **Launch**. When it stops for Epic Knights, follow [these steps](#the-one-mod-you-might-have-to-download-yourself).

---

## For the pack admin

The pack is managed with [packwiz](https://packwiz.infra.link/). This repo holds only the mod list (`.pw.toml` files) and configs, not the mod jars. The helper scripts live outside the repo in `D:\Atomic-Sengoku-Jidinosaur\tools`.

### Add a mod

1. Find the mod for **1.20.1 Forge** on modrinth.com (preferred) or curseforge.com. If its dependencies are already in the pack from one site, use the same site.
2. Run **`add-mod.bat`** and paste the link.
3. Dependencies: answer `y` for new ones, `n` for ones already in the pack. The script catches duplicates and undoes the change if needed.
4. Check the list. A yellow **CLIENT ONLY** on a mod that adds blocks, items or mobs is wrong (the server would need it). Fix that before uploading.
5. Type `y`. The mod is uploaded to GitHub, and players get it on their next Launch.

### Update the server

The server doesn't update itself, so after every change:

1. Wait about **5 minutes** (GitHub caches files).
2. **Test first:** Launch in Prism and open a singleplayer world.
3. **Stop** the server in the PebbleHost panel.
4. Run **`sync-server.bat`**. It shows what will be uploaded or deleted. Type `y` and enter the PebbleHost panel password.
5. **Start** the server.

Change configs in this repo, not directly on the server. The next sync overwrites changed files on the server with the pack's version.

### Update mods

In the pack folder: `packwiz update --all`, then `git add -A`, `git commit -m "Update mods"`, `git push`, then update the server as above.

### Undo a change

`git log --oneline` shows the history. `git revert <id>` undoes one change, then `git push` and update the server.

### Why things are the way they are

- **Modrinth instead of CurseForge** for Armor of the Ages, Corail Tombstone, Dawn of Time, Ice and Fire: Curios and Trinkets, Ingenium API and Shippy Ships: their CurseForge files block automatic downloads.
- **Epic Knights: Japanese Armory** is only on CurseForge and blocked, so it ships inside `Atomic-Sengoku.zip`. `sync-server.bat` takes it from the server backup. If it's ever updated, players have to download it manually again.
- **Client-only:** Oculus and the Complementary Reimagined shader pack.
- **Fusion stays `side = "both"`**: Dawn of Time needs it on the server, even though Modrinth labels it client-only.
- **Mixin Booster was removed**: it caused a registry mismatch (`create:cardboard_package_12x12`) when joining the server.
- **`.gitattributes`** (`* -text`) stops Git from changing line endings. Without it, config hashes don't match and Launch fails with *"Invalid mod file hash"*.
- **`.packwizignore`** keeps this README out of the pack, so it isn't downloaded into players' game folders.