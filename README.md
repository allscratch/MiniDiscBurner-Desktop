# MiniDiscBurner (desktop)

Application desktop pour transférer de la musique vers des enregistreurs MiniDisc NetMD / HiMD.

Fork personnel de [ElectronWMD](https://github.com/asivery/ElectronWMD), lui-même basé sur [Web MiniDisc Pro](https://github.com/asivery/webminidisc). Licence GPL-2.0, crédits conservés.

## Construction

Le projet se compose de deux parties :

- `webminidisc/` : sous-module contenant le renderer (le fork `MiniDiscBurner`).
- `src/` : le code Electron (accès USB natif, fenêtre, encodeur local, réglages).

Pour un clonage depuis GitHub, le sous-module pointe vers `https://github.com/allscratch/MiniDiscBurner.git`. Pour une copie locale sans dépôt distant, copie simplement le dossier `renderer/` dans `webminidisc/` (un lien symbolique **ne fonctionne pas** avec le script de build, qui supprime `../renderer`).

```bash
npm i --legacy-peer-deps
npm start        # développement
npm run dist-mac # paquets macOS (.app / .dmg, x64 et arm64)
npm run dist     # Linux + Windows (x64)
```

Après une modification du renderer, supprime le dossier `renderer/` généré avant de relancer le build.

Les DMG livrés dans `build/` contiennent une application **signée ad hoc** (signature locale, pas de certificat Developer ID). Si macOS refuse de l'ouvrir, retire le quarantainage : `xattr -d com.apple.quarantine /Volumes/MiniDiscBurner/MiniDiscBurner.app`.

## macOS

```bash
xattr -d com.apple.quarantine "build/MiniDiscBurner.app"
codesign --sign - --force --deep "build/MiniDiscBurner.app"
```

Merci à cybercase, Stefano Brilli et asivery pour le projet d'origine.
