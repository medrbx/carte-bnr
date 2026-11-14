# Lieux de Roubaix dans les archives de la BN-R

Carte interactive des rues, quartiers et sites de Roubaix cités dans les
inventaires d'archives de la Bibliothèque numérique de Roubaix (BN-R).
Chaque lieu renvoie vers la recherche correspondante sur
[bn-r.fr](https://www.bn-r.fr/).

**Carte en ligne : https://medrbx.github.io/carte-bnr/**

> Prototype (novembre 2026).

## Fonctions

- quartiers de Roubaix (deux quartiers voisins de couleurs différentes) ;
- rues et sites cités dans les inventaires, avec leurs anciens noms, leur(s)
  quartier(s) et un lien « Voir les documents sur la BN-R » ;
- recherche d'une rue par son nom actuel ou ancien ;
- choix d'un quartier ;
- fonds de carte actuels et anciens de l'IGN : plan, photographies aériennes
  actuelles, 1965-1980 et 1950-1965, carte de 1950, carte de l'état-major
  (1820-1866), carte de Cassini (XVIIIᵉ siècle) ; OpenStreetMap ;
- liens directs : `#voie=grande_rue`, `#quartier=epeule`.

## Intégrer la carte dans une page

```html
<iframe src="https://medrbx.github.io/carte-bnr/"
        title="Carte des lieux de Roubaix dans les archives de la BN-R"
        width="100%" height="600" style="border:0" loading="lazy"
        allow="fullscreen"></iframe>
```

Pour ouvrir la carte sur une rue : `src="https://medrbx.github.io/carte-bnr/#voie=grande_rue"`.
Dans un iframe, la carte affiche un lien « Ouvrir en plein écran ».

## Contenu du dépôt

| Fichier | Rôle |
|---|---|
| `index.html` | la carte : page unique, données incluses (Leaflet et fonds de carte chargés en ligne) |
| `.nojekyll` | demande à GitHub Pages de servir les fichiers tels quels |
| `README.md` | ce fichier |

`index.html` n'est **pas modifié à la main** : il est produit par le script
`scripts/ead/carte_leaflet.py` du dépôt de travail `rbx-bnr-data`.

## Mettre à jour la carte

Depuis `rbx-bnr-data` :

```bash
python scripts/ead/geogname_ir2kml.py
```

```bash
python scripts/ead/carte_leaflet.py
```

```bash
cp results/ead/indexation/carte_bnr/index.html ../carte-bnr/
```

Puis, dans `carte-bnr` :

```bash
git add index.html && git commit -m "Mise à jour de la carte" && git push
```

La carte en ligne est à jour une à deux minutes plus tard.

## Sources

- Lieux, liens et nombre de mentions : inventaires de la BN-R, Médiathèque
  de Roubaix ;
- quartiers et rues : référentiel des lieux de la BN-R (contours et tracés
  d'après la MEL, la BD TOPO de l'IGN et la BAN) ;
- fonds de carte : IGN, Géoplateforme ; © contributeurs OpenStreetMap ;
- bibliothèque cartographique : [Leaflet](https://leafletjs.com/).
