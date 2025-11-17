# Prompt détaillé pour un AI Coder

## Objectif
Créer une **Single Page Application** immersive pour le "**Tesla Group Project**". La page, en **mode sombre par défaut** avec option de mode clair, doit combiner design glassmorphism, animations fluides, interactions 3D (Three.js) et navigation par onglets/swap pour présenter les informations du projet.

## Livrable attendu
Un seul fichier `index.html` contenant **tout** le HTML, le CSS et le JavaScript nécessaires (chargement des bibliothèques via CDN : Three.js, GSAP, Chart.js facultatif). Aucune dépendance externe supplémentaire.

## Structure générale
- **Disposition principale `<main>`** : grille à **2 colonnes** (gauche 360px, droite 1fr) sur desktop, repli en **1 colonne < 980px**.
- **Fond 3D** : champ de particules animé en arrière-plan, réactif au mouvement de la souris.
- **Panneaux en verre dépoli** : `.panel-container` avec fond semi-transparent et `backdrop-filter: blur(12px)`. Mode clair = fonds clairs + texte foncé.

## En-tête (sticky)
- Gauche : logo Tesla, titre "Tesla Group Project", texte "Dec 2 · EL HANAFI MOHAMMED · ABDERRAHMAN TAHIRI · ALI AHMED · ADHAM".
- Droite : boutons **"Export PDF"** (déclenche `window.print()`) et **"Toggle Theme"** (ajoute/enlève `.light` sur `<body>` et alterne icône soleil/lune).
- Style : fond **dégradé rouge vif**.

## Barre d’onglets (sticky)
- Quatre onglets : **Members**, **Company**, **CEO KPIs**, **Production KPIs**.
- L’onglet actif utilise un fond rouge transparent distinct.

## Colonne de gauche (aside sticky)
- Photo d’Elon Musk.
- Nom "Elon Musk", rôle "CEO".
- Bloc "Quick facts" : Fondé le 1er juillet 2003 · QG : Austin, Texas · Industrie : Automotive & Renewable Energy.

## Colonne de droite (panneaux)
Afficher **un seul panneau actif** à la fois. Les autres sont masqués.

### Panneau 1 — Members (par défaut)
- Titre : "Group Members".
- Grille de 4 cartes `.square` :
  1. EL HANAFI MOHAMMED — Project Lead
  2. ABDERRAHMAN TAHIRI — Data & Research
  3. ALI AHMED AMIN MOHAMED IBRAHIM — Frontend & Design
  4. ADHAM — QA & Testing

### Panneau 2 — Company
- Titre : "Company Overview - Tesla, Inc." + paragraphe de mission.
- **Cube 3D Cybertruck** (`#company-3d-container` ~300px) : `BoxGeometry` texturé avec 6 images Cybertruck, interactif via drag souris (`mousedown` + `mousemove`).
- Grille de 3 cartes : "Fondateurs — Martin Eberhard & Marc Tarpenning", "CEO — Elon Musk", "Produits Clés — Electric Vehicles, Solar Energy, Battery Storage".

### Panneau 3 — CEO KPIs
- Titre : "CEO KPIs".
- Grille `.kpi-grid` de 5 cartes `.kpi-square` :
  - **EBITDA Margin** — Formule `(EBITDA / Total Revenue) * 100` — Pourquoi : profitabilité opérationnelle.
  - **Vehicle Delivery Growth Rate** — `((Current - Previous) / Previous) * 100` — Pourquoi : croissance des livraisons.
  - **Energy Storage Deployment** — `Sum of deployed battery capacity` — Pourquoi : suivi de la croissance énergie (GWh).
  - **Free Cash Flow** — `Operating Cash Flow - CapEx` — Pourquoi : cash disponible (USD).
  - **Global EV Market Share** — `(Tesla EV Sales / Global EV Sales) * 100` — Pourquoi : compétitivité mondiale (%).

### Panneau 4 — Production KPIs
- Titre : "Production KPIs" + paragraphe d’intro.
- **Batterie 4680 3D** (`#production-3d-container` ~300px) : `CylinderGeometry` pour le corps, petit cylindre pour capuchon, petit cylindre pour terminal. Matériaux métalliques (`MeshStandardMaterial`). Rotation lente + drag interactif.
- Grille de 6 cartes KPI :
  - Production Throughput — `Unités produites / jour` — Pourquoi : vitesse de chaîne.
  - First Pass Yield (FPY) — `(Unités OK / Total) * 100` — Pourquoi : qualité de production.
  - Cycle Time — `Temps pour 1 unité` — Pourquoi : goulots d’étranglement.
  - Equipment Utilization Rate — `(Temps Opération / Temps Dispo) * 100` — Pourquoi : efficacité machine.
  - Inventory Turnover — `COGS / Inventaire Moyen` — Pourquoi : efficacité de l’inventaire.
  - Labor Productivity — `Unités / Heures de travail` — Pourquoi : efficacité main d’œuvre.

## Fonctionnalités JavaScript
- **Tabs** : clic = `.panel` active (classe `.active`), autres masquées.
- **Swipe** : sur `#right-panel-container`, écouter `touchstart/touchend`. Glisse gauche → onglet suivant ; droite → onglet précédent.
- **Animations d’apparition** : toutes les cartes/panneaux portent `.animated-item` (opacity 0, translateY 20px). Via `IntersectionObserver` ou `GSAP ScrollTrigger`, ajouter `.is-visible` quand visible. **Réinitialiser** l’animation lors du changement d’onglet pour le contenu entrant.
- **3D** : utiliser Three.js via CDN pour le fond particules, le cube et la batterie. GSAP pour animations (optionnel mais recommandé). Chart.js peut être préchargé même si non utilisé.

## Style & thèmes
- Mode sombre par défaut; `.light` pour mode clair (fonds blancs/gris, texte noir).
- Panneaux glassmorphism, coins arrondis, ombres douces; transitions/hover subtils.
- Header et onglet actif à dominante **rouge** pour cohérence.

## Raccourcis de test
- Vérifier :
  - Bouton Export PDF déclenche bien `window.print()`.
  - Bouton Toggle Theme ajoute/retire `.light` et alterne l’icône.
  - Changement d’onglet + swipe met à jour le panneau visible et relance les animations `.animated-item`.
  - Interactions 3D (drag cube/batterie) fonctionnent et le fond particules suit la souris.

Collez ce prompt dans votre AI Coder : il doit produire un `index.html` complet qui respecte scrupuleusement ces spécifications.
