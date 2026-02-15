# AoA - Festival Layout Planner

Outil interactif de planification de festival sur carte, conçu pour la **Place du Casino d'Avenches**.

Permet de placer, dimensionner et organiser tous les éléments d'une manifestation (scènes, bars, barrières, tentes, etc.) sur une carte à l'échelle, puis d'exporter le plan en XML ou PDF.

## Démarrage

Aucune installation requise. Ouvrir `index.html` dans un navigateur moderne (Chrome, Firefox, Edge).

```
git clone <repo-url>
cd AoA-
open index.html
```

La carte se charge automatiquement centrée sur la Place du Casino d'Avenches via OpenStreetMap (connexion internet nécessaire pour les tuiles).

## Fonctionnalités

### Carte interactive

- Basée sur **Leaflet.js** avec tuiles OpenStreetMap
- Centrée sur la Place du Casino d'Avenches (46.8823, 7.0420)
- Zoom de 14 à 22 (vue satellite-like au max)
- Indicateur d'échelle en temps réel (mètres/pixel)

### Bibliothèque d'éléments

30+ modules prédéfinis répartis en 5 catégories :

| Catégorie | Éléments |
|---|---|
| **Structures** | Grande scène (16x12m), petite scène (8x6m), tentes (6x3, 6x6, 10x5), podium |
| **Restauration** | Grand bar (8x3m), petit bar (4x2m), stand food, food truck, cuisine, buvette |
| **Sécurité** | Barrières (2m, 3m), entrée, sortie secours, poste secours, extincteur |
| **Technique** | Régie son, générateur, tour éclairage, chemin câbles, container, loge artistes |
| **Divers** | Bloc WC, WC PMR, point déchets, zone parking, zone VIP, point info |

Chaque élément a des dimensions réelles en mètres, un code couleur et une icône.

### Placement des éléments

Deux méthodes :
- **Drag & drop** : glisser un élément de la bibliothèque vers la carte
- **Clic** : cliquer sur un élément de la bibliothèque, puis cliquer sur la carte pour le placer

### Édition des éléments

Sélectionner un élément sur la carte pour accéder au panneau **Propriétés** :
- Nom personnalisable
- Largeur et profondeur en mètres
- Rotation (aussi via touche `R`)
- Couleur et opacité
- Notes libres
- Coordonnées GPS (lecture seule)

Déplacer un élément en le glissant directement sur la carte.

### Grille d'accrochage (Snap Grid)

- **Grille visuelle** : affiche un quadrillage sur la carte (touche `G`)
- **Pas configurable** : 0.5m, 1m, 2m, 5m, 10m via le sélecteur de la toolbar
- **Accrochage** : les éléments se calent sur les intersections de la grille (touche `S`)
- L'accrochage fonctionne au placement, au drag et au déplacement clavier

### Mesure de distance

- Activer le mode mesure (touche `M` ou bouton toolbar)
- Cliquer pour poser des points successifs (polyligne)
- Distance affichée en temps réel sur chaque segment
- Total cumulé affiché pour les polylignes
- Clic droit ou `Echap` pour terminer la mesure
- Bouton **Effacer** pour supprimer toutes les mesures

### Export / Import XML

Le format XML sauvegarde l'intégralité du plan :
- Métadonnées (nom, lieu, centre de la carte, zoom, date)
- Tous les éléments avec position, dimensions, rotation, couleur, notes
- Les éléments personnalisés ajoutés à la bibliothèque

```xml
<?xml version="1.0" encoding="UTF-8"?>
<FestivalPlan>
  <Meta>
    <Name>Festival Avenches</Name>
    <Location>Place du Casino, Avenches</Location>
    <CenterLat>46.8823</CenterLat>
    <CenterLng>7.042</CenterLng>
    <Zoom>19</Zoom>
    <ExportDate>2026-02-15T10:30:00.000Z</ExportDate>
  </Meta>
  <Elements>
    <Element>
      <Id>1</Id>
      <TypeId>scene_grande</TypeId>
      <Name>Grande scène</Name>
      <Icon>🎤</Icon>
      <Width>16</Width>
      <Height>12</Height>
      <Color>#e74c3c</Color>
      <Opacity>0.6</Opacity>
      <Rotation>0</Rotation>
      <Lat>46.88230</Lat>
      <Lng>7.04200</Lng>
      <Notes></Notes>
    </Element>
  </Elements>
  <CustomLibrary/>
</FestivalPlan>
```

Import via copier-coller ou chargement de fichier `.xml`.

### Export PDF

Génère un document PDF professionnel avec :
- Titre personnalisable
- Format au choix : A4, A3, A2
- Orientation : paysage ou portrait
- Capture haute résolution de la carte
- Légende optionnelle avec pastilles couleur, noms, dimensions et quantités
- En-tête avec lieu et date, pied de page

### Éléments personnalisés

Bouton **+ Élément custom** pour créer ses propres modules :
- Nom, icône (emoji), dimensions par défaut, couleur
- Affectation à une catégorie existante
- Sauvegardé dans l'export XML

## Raccourcis clavier

| Touche | Action |
|---|---|
| `G` | Afficher / masquer la grille |
| `S` | Activer / désactiver l'accrochage (snap) |
| `M` | Activer / désactiver le mode mesure |
| `R` | Rotation +15° de l'élément sélectionné |
| `Shift+R` | Rotation +1° (précision) |
| `Flèches` | Déplacer l'élément de 0.1m |
| `Shift+Flèches` | Déplacer l'élément de 0.5m |
| `Suppr` / `Backspace` | Supprimer l'élément sélectionné |
| `Ctrl+Z` | Annuler |
| `Ctrl+Y` | Rétablir |
| `Echap` | Désélectionner / quitter le mode mesure |

## Stack technique

- **HTML/CSS/JS** : application mono-fichier, aucun build nécessaire
- **Leaflet.js 1.9.4** : carte interactive avec tuiles OpenStreetMap
- **html2canvas 1.4.1** : capture de la carte pour l'export PDF
- **jsPDF 2.5.2** : génération du document PDF
- Toutes les dépendances sont chargées via CDN (connexion internet requise)
