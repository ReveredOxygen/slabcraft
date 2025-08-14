# Update process

1. Copy new FO version to slabcraft folder. isxander-main-menu-credits.json and fabric_loader_dependencies.json need formatted.
2. Use commands similar to this in order to copy Slabcraft's changes to a new FO version
   ```sh
   diff -ruNa --binary fabulously-optimized-ab70e025264a50561bd427b18af5f083675eae55/Packwiz/1.21.4 slabcraft/src/1.21.4 > patch
   cd slabcraft/src/1.21.8
   patch --binary -p3 < ../../../patch
   ```
3. Manually handle any .rej files as necessary
4. Hard reset the mods folder back to FO's mod folder
5. Use this command to reinstall Slabcraft's mods, handling any mods which don't have releases for the new minecraft version
   ```sh
   xargs -I % -n 1 sh -c "echo %; packwiz mr install -y %" < added-by-me
   ```

# Build process

1. Do changes. Test by building pack with `packwiz mr export`. Use ViaFabricPlus to test on Slab if necessary.
2. Update the version in `config/isxander-main-menu-credits.json`, `config/configpatcher/slabcraft/current-version.txt` (and assume-previous-version.txt), and `pack.toml`
3. Remember to remove ViaFabricPlus
4. Build pack with `packwiz mr export`
5. Publish manually to GitHub, Modrinth
