# LINKTREE_APPS

Page de liens personnelle de gambidrissi-dev : une sélection d'apps macOS partagées en dehors du Collectif Cobalt, chacune pointant vers sa page de téléchargement (`<nom>-Share`).

Pendant du [LINKTREE_COLLECTIFCOBALT](https://github.com/gambidrissi-dev/LINKTREE_COLLECTIFCOBALT) côté studio, mais identité et contenu propres — vanilla HTML/CSS, sans dépendance, sans build.

## Structure

Tout tient dans `index.html` (une seule page, CSS et contenu inline). Les icônes d'app sont embarquées en base64 directement dans le CSS/HTML — pas de dossier `assets/`.

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
