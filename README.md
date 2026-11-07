# Limites des provinces et territoires du Canada — GeoJSON simplifié

GeoJSON des **13 provinces et territoires** du Canada selon les limites du
**Recensement 2021 de Statistiques Canada** (produit `lpr_000b21s_f`), simplifié
pour un affichage rapide dans des cartes choroplèthes (Metabase, QGIS, Leaflet…).

## Fichier

- [`provinces_2021.geojson`](provinces_2021.geojson) — 13 entités `MultiPolygon`,
  CRS WGS84 (EPSG:4326), ~1,1 Mo.
- Propriété d'identification : **`PRANOM`** (nom anglais de la province ou du
  territoire, p. ex. `Quebec`, `Northwest Territories`, `Nunavut`).
- Autres propriétés du produit source (PRIDU, PRFNOM, SUPTERRE…) non conservées ;
  la version intégrale se trouve dans le
  [produit officiel](https://www12.statcan.gc.ca/census-recensement/2021/geo/sip-sis/boundary-limites/index-fra.cfm).

## Simplification appliquée

À partir du GeoPackage officiel (référence, résolution intégrale) :

1. réparation des géométries (`make_valid`, méthode structure) et extraction des
   parties polygonales ;
2. **suppression des îles de moins de ~130 km²** (îlots arctiques sans valeur à
   l'échelle nationale) ;
3. simplification Douglas-Peucker avec préservation de la topologie
   (tolérance 0,008°) ;
4. arrondi des coordonnées à 2 décimales (~1,1 km).

Résultat : géométries valides, ~1,1 Mo (Metabase recommande moins de 5 Mo).

## Utilisation avec Metabase (carte régionale personnalisée)

Admin → Settings → Maps → Custom Maps → Add a Map :

- URL : `https://raw.githubusercontent.com/franc00018/canada-provinces-geojson/main/provinces_2021.geojson`
- Region identifier / name : `PRANOM`

## Licence et attribution

Contient des données géographiques dérivées de produits de Statistiques Canada
(limites du Recensement 2021), mises à disposition sous la
**Licence ouverte du gouvernement du Canada** :
<https://www.statcan.gc.ca/fr/reference/licence>.

Attribution requise : « Contient des informations sous licence du gouvernement
ouvert – Canada ».

---

Dépôt créé pour le cours « Je valide ça, service-conseil » sur l'entrepôt de
données (dépôt principal :
[Presentations-Seances](https://github.com/Mentorat-2026-FY/Presentations-Seances)).
