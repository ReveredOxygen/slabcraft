# Fabulously Optimized repository

Welcome to my repository.
Here you'll find the resources for:

* Packwiz files. This is the only part used by Slabcraft, but the rest is left in place to make git happy [(read more)](https://github.com/comp500/packwiz#packwiz)
* CurseForge modpack [(read more)](https://support.curseforge.com/en/support/solutions/articles/9000196904-creating-a-custom-profile)
* MultiMC modpack [(read more)](https://github.com/MultiMC/MultiMC5/wiki/Instance-settings)
* MultiMC modpack with packwiz [(read more)](https://github.com/comp500/packwiz#packwiz-installer-for-pack-installation)
* Modrinth files [(read more)](https://github.com/Madis0/fabulously-optimized/issues/63)
* Changelog, license, readme, [cape](https://github.com/Madis0/fabulously-optimized/wiki/Free-cape)
* GitHub meta files in `.github` [(read more)](https://stackoverflow.com/a/61301254)
* GitHub page in `docs` [(read more)](https://pages.github.com/) - currently just a redirection to CF page

Other things to note:

* As seen in the `.gitignore` file, this repo will not include JAR files of any kind to respect the modders. If you want to build a pack based on this, get the JARs manually via any method you like (CurseForge Launcher, CurseForge website, Modrinth, packwiz, ...).
   * Because there are no JARs, some folders would usually not be uploaded by Git at all, this is worked around using a `.gitkeep` file [(read more)](https://stackoverflow.com/a/7229996) to keep the folder structure.
* Since some folders are duplicated - such as config folders, I am using Windows-like soft symlinks [(read more)](https://blogs.windows.com/windowsdeveloper/2016/12/02/symlinks-windows-10/). Those don't work very well in GitHub, so I recommend using a [local Git client](https://desktop.github.com).

### Update process

1. Use commands similar to this in order to copy Slabcraft's changes to a new FO version
   ```sh
   git diff 70ed6c5 --binary Packwiz/1.21 > ../patch
   git apply --reject --directory=Packwiz/1.21.4 -p2 ../patch
   ```
2. Manually handle any .rej files as necessary
3. Hard reset the mods folder back to FO's mod folder
4. Use this command to reinstall Slabcraft's mods, handling any mods which don't have releases for the new minecraft version
   ```sh
   xargs -I % -n 1 "echo %; packwiz mr install -y %" < added-by-me
   ```

### Build process

1. Do changes. Test by building pack with `packwiz mr export`. Use ViaFabricPlus to test on Slab if necessary.
2. Update the version in `config/isxander-main-menu-credits.json`, `config/configpatcher/slabcraft/current-version.txt`, and `pack.toml`
3. Remember to remove ViaFabricPlus
4. Build pack with `packwiz mr export`
5. Publish manually to GitHub, Modrinth
