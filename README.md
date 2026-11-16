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
  actuelles, 1965-1980 et 1950-1965, carte de 1950 ; OpenStreetMap ; le Plan
  IGN est affiché au départ, les autres se déplient avec « Autres fonds de
  carte » (un fond affiché reste visible dans la liste repliée) ;
- plans anciens de Roubaix géoréférencés, toujours au-dessus des fonds :
  1899 (P. Pachy), 1889 (service de la voirie, 1/4000), 1855 (E. Barbotin,
  centre-ville) et Roubaix vers 1811 (plan d'É. Verscheure, 1911) ;
- dans la boîte des couches, fonds et plans anciens ont la même fiche
  (vignette et nom) : l'œil affiche ou masque la couche (plusieurs à la
  fois, superposées), la poignée ⠿ se glisse pour régler l'ordre d'affichage
  (en haut de la liste = au-dessus ; au clavier, flèches haut et bas), et le
  chevron déplie l'opacité, la source et, pour les plans, « Centrer sur le
  plan » ;
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
| `plans/<année>/` | tuiles des plans anciens (XYZ, WebP) : `1899`, `1889`, `1855`, `1811`, et `vignette.webp` (un carré pris au milieu du plan, pour la fiche) |
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

Si un plan ancien a été recalé, recopier ses tuiles (même correspondance pour
`tuiles` → `1899`, `tuiles_1855` → `1855`, `tuiles_1811` → `1811`) :

```bash
rsync -a --delete --exclude vignette.webp data/geo/plans_anciens/leaflet_1899/tuiles_1889/ ../carte-bnr/plans/1889/
```

puis refaire sa vignette (un carré au milieu du plan) et la recopier :

```bash
python3 scripts/ead/vignettes_plans_anciens.py
```

```bash
cp data/geo/plans_anciens/leaflet_1899/vignettes/1889.webp ../carte-bnr/plans/1889/vignette.webp
```

Puis, dans `carte-bnr` :

```bash
git add index.html plans && git commit -m "Mise à jour de la carte" && git push
```

La carte en ligne est à jour une à deux minutes plus tard.

## Sources

- Lieux, liens et nombre de mentions : inventaires de la BN-R, Médiathèque
  de Roubaix ;
- quartiers et rues : référentiel des lieux de la BN-R (contours et tracés
  d'après la MEL, la BD TOPO de l'IGN et la BAN) ;
- fonds de carte : IGN, Géoplateforme ; © contributeurs OpenStreetMap ;
- plans anciens : Archives municipales de Roubaix (6Fi024, plan de 1899 ;
  6Fi022, plan de 1889) ; BN-R (PLA_B_033, Roubaix vers 1811) ; BnF,
  Ge C 3003 (plan de 1855, [Gallica](https://gallica.bnf.fr/)) ;
  géoréférencement BN-R ;
- bibliothèque cartographique : [Leaflet](https://leafletjs.com/).
