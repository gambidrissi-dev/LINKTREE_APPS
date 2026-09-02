# LINKTREE_APPS

Page de liens personnelle de gambidrissi-dev : une sélection d'apps macOS partagées en dehors du Collectif Cobalt, chacune pointant vers sa page de téléchargement (`<nom>-Share`).

Pendant du [LINKTREE_COLLECTIFCOBALT](https://github.com/gambidrissi-dev/LINKTREE_COLLECTIFCOBALT) côté studio, mais identité et contenu propres — vanilla HTML/CSS, sans dépendance, sans build. Même traitement PWA que le Linktree du studio : installable, fonctionne hors ligne, thème clair/sombre persistant.

## Structure

Tout tient dans `index.html` (CSS et contenu inline). Les icônes d'app (Parure, Skillotheque…) sont embarquées en base64 directement dans le HTML — pas de dossier `assets/` pour elles. Le reste :

- `manifest.webmanifest` + `icon-192.png` / `icon-512.png` / `icon-maskable-512.png` / `apple-touch-icon.png` — installation sur Dock/écran d'accueil
- `sw.js` — service worker (navigation network-first, assets cache-first, cache versionné purgé à l'activation)
- `fonts/` — Bricolage Grotesque 700, Manrope 400, JetBrains Mono 400 en `.woff2` self-hébergés (seuls les poids réellement utilisés ; pas de requête vers Google Fonts, fonctionne hors ligne)
- `og-image.jpg` — aperçu de partage (Open Graph / Twitter Card)
- Toggle de thème (bouton en haut à droite) persisté dans `localStorage`, avec script anti-flash dans le `<head>`

Icônes et image OG générées avec Pillow (dégradé + monogramme « GD », même style que les icônes d'app réelles).

## Ajouter une app

Dupliquer un bloc `<a class="app">…</a>` dans `<nav class="shelf">` et renseigner :

- `href` — l'URL de la page `<nom>-Share`
- `.app-icon` — icône embarquée en `data:image/png;base64,…` (extraite du `.icns` de l'app : `sips -s format png AppIcon.icns --out icon.png -Z 256`, puis `base64 -b 0 -i icon.png`)
- `.app-name`, `.app-tag` — nom et description en une ligne
- `.app-meta` — version (tag git le plus récent de préférence) et stack

## Développement local

```bash
python3 -m http.server 8080
```

## Déploiement

GitHub Pages, branche `main`, racine `/`. Le fichier `.nojekyll` désactive le traitement Jekyll (sinon certains fichiers commençant par `_` seraient ignorés).
