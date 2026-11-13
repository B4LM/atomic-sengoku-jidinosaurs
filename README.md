# Atomic Sengoku Jidinosaurs

**Minecraft 1.20.1 · Forge 47.4.28 · 84 mods**

This repo is our modpack. Prism Launcher reads it every time you click **Launch** and updates your mods and configs automatically, so you always match the server.

- [Setup for players](#setup-for-players)
- [The one mod you have to download yourself](#the-one-mod-you-have-to-download-yourself)
- [Good to know](#good-to-know)
- [If something goes wrong](#if-something-goes-wrong)
- [For the pack admin](#for-the-pack-admin)

---

## Setup for players

### What you need
- A Windows PC and your Minecraft Java account (Microsoft login)
- The file `Atomic-Sengoku.zip` from the pack admin (recommended), **or** about 10 extra minutes for the [manual setup](#manual-setup-without-the-zip)

### 1. Install Prism Launcher
Download it from [prismlauncher.org/download/windows](https://prismlauncher.org/download/windows/) and run the installer. The default options are fine.

### 2. First start: Java and login
- When Prism asks about Java, let it **download Java automatically**.
- Click the account button at the top right → **Manage Accounts** → **Add Microsoft**, and sign in with the account you play Minecraft with.

### 3. Import the pack
Click **Add Instance** → **Import** on the left → **Browse**, pick `Atomic-Sengoku.zip`, then click **OK**.

The zip already contains Forge, the memory setting, the auto-update tool and the [Epic Knights mod](#the-one-mod-you-have-to-download-yourself). You don't need to change anything.

### 4. Click Launch
Select the instance and click **Launch**. A small **packwiz** window appears first and downloads all the mods. The first time this takes a few minutes, later it takes seconds.

Then Minecraft starts. The first start with this many mods is slow, so give it a couple of minutes.

### 5. Join the server
**Multiplayer** → **Add Server**, with the same address as before. Ask the pack admin if you don't have it.

**Shaders (optional):** Options → Video Settings → Shader Packs → **Complementary Reimagined**. Turn them off again if your game gets laggy.

### Manual setup (without the zip)
Only needed if you don't have `Atomic-Sengoku.zip`. Do steps 1 and 2 above first.

1. **Add Instance** → **Vanilla** → version **1.20.1**. Name it `Atomic Sengoku`, click **OK**.
2. Right-click the instance → **Edit** → **Version** → **Install Forge** → choose **47.4.28**.
3. Download `packwiz-installer-bootstrap.jar` from the newest release at [github.com/packwiz/packwiz-installer-bootstrap/releases](https://github.com/packwiz/packwiz-installer-bootstrap/releases) (under "Assets").
4. Right-click the instance → **Folder**, open the `minecraft` folder (or `.minecraft`) and put the jar in there.
5. Right-click the instance → **Edit** → **Settings**:
   - **Java** tab: tick **Memory** and set **Maximum memory** to `6144` MB (`4096` if your PC has 8 GB RAM or less).
   - **Custom commands** tab: tick the box and paste this into **Pre-launch command**:
     ```
     "$INST_JAVA" -jar packwiz-installer-bootstrap.jar https://raw.githubusercontent.com/B4LM/atomic-sengoku-jidinosaurs/main/pack.toml
     ```
6. Download the [Epic Knights mod](#the-one-mod-you-have-to-download-yourself) as described below, then click **Launch**.

---

## The one mod you have to download yourself

The author of **Epic Knights: Japanese Armory** doesn't allow launchers to download it automatically, and it isn't on Modrinth. If you imported `Atomic-Sengoku.zip`, it's already included and you can skip this.

Otherwise, the first Launch stops with an error saying the mod *"is excluded from the CurseForge API and must be downloaded manually"*. Then:

1. Open [the mod's file page on CurseForge](https://www.curseforge.com/minecraft/mc-mods/epic-knights-japanese-armory/files/5294116) and click **Download**.
2. Save the file **with exactly this name**:
   `[1.20.1-forge]-Epic-Knights-Japanese-Armory-1.6.2.jar`
3. Put it in the instance's `mods` folder: right-click the instance in Prism → **Folder** → `minecraft` → `mods`.
4. Click **Launch** again.

You only need to do this once. You'll need to do it again only if this mod gets updated.

---

## Good to know

- **Always start the game through Prism.** The old CurseForge version doesn't get updates and stops matching the server.
- **Updates happen on their own.** When a mod is added or updated, you get it the next time you click Launch.
- **Don't add or remove mods in this instance yourself.** If your mods differ from the server's, you can't join. Ask the pack admin and they'll add it for everyone.
- **Keybinds and video settings** start fresh. To keep your old ones, copy `options.txt` from your old CurseForge instance folder into Prism's instance folder (right-click the instance → **Folder** → `minecraft`).

---

## If something goes wrong

**"This mod is excluded from the CurseForge API and must be downloaded manually"**
Follow [the steps above](#the-one-mod-you-have-to-download-yourself), using the link and folder from the error message. If the error names a different mod than Epic Knights, tell the pack admin.

**Can't join: "mod mismatch", "registry" or "missing" errors**
Close Minecraft and click **Launch** again so the newest version gets downloaded. If it still fails, send the error to the pack admin.

**Prism says the pre-launch command failed**
Usually a short internet or GitHub hiccup. Wait a minute and try again. If it keeps happening, send a screenshot to the pack admin.

**The game crashes or freezes while loading**
Right-click the instance → **Edit** → **Settings** → **Java** and check that **Maximum memory** is around `6144` MB (`4096` with 8 GB RAM or less). If it still crashes, send the newest file from the instance's `crash-reports` folder to the pack admin.

---

## For the pack admin

The pack is managed with [packwiz](https://packwiz.infra.link/). This repo only holds the mod list (`.pw.toml` files) and configs, not the mod jars.

### Add a mod
Find it on Modrinth (preferred) or CurseForge, then in the pack folder:
```
packwiz modrinth add <link>
packwiz curseforge add <link>
```
Required dependencies get added automatically. Then `git add -A`, `git commit -m "Add <mod>"`, `git push`.

### Update mods
```
packwiz update --all
```

### Every change must also go to the server
The server doesn't update itself. After adding or updating mods, upload the same mod files to the server's `mods` folder, otherwise nobody can join.

### Things to know
- **Prefer Modrinth.** Some CurseForge mods block automatic downloads. These 6 were switched to Modrinth for that reason: Armor of the Ages, Corail Tombstone, Dawn of Time, Ice and Fire: Curios and Trinkets, Ingenium API, Shippy Ships. Epic Knights: Japanese Armory is only on CurseForge, so players add it manually.
- **Client-only** (`side = "client"`, not installed on the server): Oculus and the Complementary Reimagined shader pack.
- **Fusion** must stay `side = "both"` because Dawn of Time needs it on the server, even though Modrinth labels it client-only.
- **Mixin Booster was removed** because it caused a registry mismatch (`create:cardboard_package_12x12`) when joining the server.
- `.gitattributes` (`* -text`) stops Git from changing line endings. Without it, config file hashes stop matching and the installer fails with *"Invalid mod file hash"*.
- `.packwizignore` keeps this README out of the pack, so it isn't downloaded into players' game folders.
- GitHub caches files for about 5 minutes after a push, so wait a moment before testing a change.
