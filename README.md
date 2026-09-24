# CopyPilot - preproduction du frontend independant

Copie **exacte** du frontend LIVE de `copy-pilot.io`, servie par GitHub Pages pour prouver
qu'elle reste accessible si `.24` et tous les VPS de trading disparaissent.

- `index.html` : identique au bit pres au fichier servi en production
- `404.html`   : meme fichier, pour que `/login`, `/pricing` et `/app/*` fonctionnent au
                 rafraichissement direct (GitHub Pages n'a pas de repli SPA natif)
- `.nojekyll`  : desactive Jekyll

**Aucune donnee, aucun secret.** L'API n'est pas servie ici : sans backend joignable,
l'interface s'affiche en mode degrade, ce qui est precisement ce qui est teste.

Ce depot est une PREPRODUCTION. `copy-pilot.io` n'est pas bascule.
