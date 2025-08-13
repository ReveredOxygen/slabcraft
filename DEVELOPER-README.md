# Update process

1. Use commands similar to this in order to copy Slabcraft's changes to a new FO version
   ```sh
   git diff 70ed6c5 --binary Packwiz/1.21 > ../patch
   git apply --reject --directory=Packwiz/1.21.4 -p2 ../patch
   ```
2. Manually handle any .rej files as necessary
3. Hard reset the mods folder back to FO's mod folder
4. Use this command to reinstall Slabcraft's mods, handling any mods which don't have releases for the new minecraft version
   ```sh
   xargs -I % -n 1 sh -c "echo %; packwiz mr install -y %" < added-by-me
   ```

# Build process

1. Do changes. Test by building pack with `packwiz mr export`. Use ViaFabricPlus to test on Slab if necessary.
2. Update the version in `config/isxander-main-menu-credits.json`, `config/configpatcher/slabcraft/current-version.txt`, and `pack.toml`
3. Remember to remove ViaFabricPlus
4. Build pack with `packwiz mr export`
5. Publish manually to GitHub, Modrinth
