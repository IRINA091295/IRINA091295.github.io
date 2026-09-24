# Assets de marque CopyPilot AI

Ce dossier est l'emplacement prêt pour le vrai logo ("tête de taureau", verrouillé comme asset
fourni par l'utilisateur dans `DESIGN_SYSTEM.md` — jamais redessiné en code). Déposez les fichiers
suivants ici, sous ces noms **exacts** : le reste de l'application les détecte et les utilise
automatiquement, sans aucune modification de code ni de mise en page.

| Fichier attendu               | Où il apparaît                                           | Format recommandé |
|---------------------------------|-----------------------------------------------------------|--------------------|
| `logo-mark.svg`                | Sidebar (icône carrée 30×30) + écran de connexion (64×64) | SVG carré, fond transparent, dessin qui reste net à petite taille |
| `favicon.svg`                  | Fallback SVG de l'onglet navigateur                        | SVG carré simplifié (lisible à 16-32px) |
| `favicon.ico`                  | Onglet navigateur (`/favicon.ico`, prioritaire sur le SVG) | ICO multi-résolution 16/32/48 |
| `favicon-16x16.png`            | `<link rel="icon" sizes="16x16">`                          | PNG 16×16 |
| `favicon-32x32.png`            | `<link rel="icon" sizes="32x32">`                          | PNG 32×32 |
| `favicon-48x48.png`            | `<link rel="icon" sizes="48x48">`                          | PNG 48×48 |
| `apple-touch-icon.png`         | iOS "Ajouter à l'écran d'accueil" (`/apple-touch-icon.png` + `<link rel="apple-touch-icon">`) | PNG 180×180 |
| `android-chrome-192x192.png`   | `<link rel="icon" sizes="192x192">`                        | PNG 192×192 |
| `android-chrome-512x512.png`   | `<link rel="icon" sizes="512x512">`                        | PNG 512×512 |

Correction favicon (2026-08-22) : le pack fourni par l'utilisateur (tête de taureau seule, sans le
texte "CopyPilot AI") a remplacé l'ancien favicon SVG générique en zigzag - jamais la vraie marque.
Le glyphe était décalé d'environ 2% horizontal / 5% vertical dans son canevas carré sur TOUT le pack
fourni (bug réel détecté par analyse de la position du glyphe dans le canevas) - recentré une seule
fois avant dépôt ici, jamais régénéré/redessiné autrement.

## Comment ça se branche

- **Sidebar / écran de connexion** : au chargement de la page, `applyBrandAssets()`
  (`dashboard-src/dashboard.template.html`) vérifie si `/brand/logo-mark.svg` existe ; si oui, il
  remplace le monogramme placeholder par ce SVG, en conservant exactement la même taille de
  conteneur (aucune mise en page à refaire). Si le fichier n'existe pas encore, le placeholder
  actuel reste affiché tel quel.
- **Favicon** : `/favicon.ico` sert `public/brand/favicon.ico` (le vrai binaire, prioritaire) s'il
  existe, sinon `public/brand/favicon.svg`, sinon un placeholder SVG en dur (`src/main.ts`) -
  jamais un 204 vide. `/apple-touch-icon.png` sert `public/brand/apple-touch-icon.png` de la même
  façon. Les autres tailles PNG (16/32/48/192/512) sont servies via `/brand/<nom>` par
  `BrandAssetsController`. Tout est lu à CHAQUE requête (jamais mis en cache au démarrage du
  serveur) - déposer/remplacer un fichier suffit, aucun redémarrage requis pour qu'il soit servi.
- Toutes les routes `/brand/*` passent par la liste blanche stricte de
  `src/dashboard/brand-assets.controller.ts` - aucun autre nom de fichier n'est servi depuis ce
  dossier.

Rien à installer, rien à recompiler : déposez les fichiers, rechargez la page.
