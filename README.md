<div align="center">

<img src="assets/logo.png" alt="ShipBattle" width="260">

# ShipBattle

**Bataille navale en Java avec LibGDX**

`Java` `LibGDX` `Gradle` `JUnit 5` `MVC`

</div>

Projet de jeu de bataille navale développé en Java avec LibGDX dans le cadre d'un projet universitaire.

> **Contexte.** Projet d'équipe réalisé à trois pendant ma formation (2025). L'historique du dépôt conserve les commits de chacun.

## Répartition initiale de l'équipe

| Participant | Responsabilités initiales |
|---|---|
| **Chris** | Base du projet et préparation des branches ; contrôleur de jeu (`GameController` dans la consigne initiale), `ConsoleView`, modèles `Player` et `Game`. |
| **Daouda** | Modèles `Grid`, `Cell` et `Coordinate` ; recherches sur la Javadoc et les conventions de commits avec James. |
| **James** | Classe abstraite `Ship` et ses descendants, `AttackResponse`, enums `AttackResult`, `Direction` et `GameState` ; recherches sur la Javadoc et les conventions de commits avec Daouda. |

Les trois participants doivent documenter leur code dès le début, avec une Javadoc en anglais, brève et concise, et respecter les attributs et méthodes de l'UML. La [répartition détaillée](docs/REPARTITION_ROLES.md) relie chaque classe à son chemin actuel et précise les règles communes. Cette consigne historique, retransmise le 30 septembre 2026, ne donne ni noms de branches Java ni choix confirmé entre Conventional Commits et Gitmoji.

Ces responsabilités initiales n'attribuent pas exclusivement les évolutions ultérieures. Le contrôleur console actuel est `ConsoleGameController` ; le `GameController` du package GUI est distinct.

## Contributions de James

Les contributions de James sont consultables dans [l'historique du dépôt](https://github.com/OhBadBoy/Ship-Battle/commits/main/?author=OhBadBoy) :

- Modèle des navires : classe abstraite `Ship` et types `Carrier`, `Cruiser`, `Destroyer` et `Torpedo`, avec leurs méthodes de jeu.
- Réponses d'attaque (`AttackResponse`) et énumérations d'états de partie.
- Documentation Javadoc des classes et harmonisation des constructeurs.
- Interface de placement des navires avec LibGDX : aperçu qui suit le curseur, rotation, alignement sur les cases, changement de sélection, réinitialisation, validation avant le début de partie, mise en page adaptée à la fenêtre.

Le travail sur le placement LibGDX complète le périmètre initial de James. L'intelligence artificielle, la suite de tests et la couverture de code sont des travaux d'équipe ; elles ne lui sont pas attribuées individuellement.

## Aperçu

<div align="center">

<img src="gdd-assets/ship_placement_menu.png" alt="Écran de placement des navires" width="640">

<sub>Écran de placement des navires (interface LibGDX)</sub>

</div>

## Description

Implémentation complète du jeu classique de bataille navale avec :
- Interface graphique 2D (LibGDX)
- Mode Joueur vs Joueur
- Mode Joueur vs IA (3 niveaux de difficulté)
- Pouvoirs spéciaux (Bombe, Radar)
- Architecture MVC
- Tests unitaires avec JUnit 5

## Fonctionnalités

### Modes de jeu
- **Joueur vs Joueur** : Deux joueurs humains s'affrontent en local
- **Joueur vs IA** : Affrontez une intelligence artificielle avec 3 niveaux :
  - **Facile** : Tirs aléatoires
  - **Moyen** : Système HUNT/TARGET (cible les cases adjacentes après un tir réussi)
  - **Difficile** : Algorithme de probabilité avec analyse d'orientation des navires

### Système d'attaque
- **Attaque normale** : Cible une seule case
- **Bombe** (2 charges) : Attaque en zone 3x3
- **Radar** (3 charges) : Détecte les navires dans une zone 3x3 sans infliger de dégâts

### Navires
| Navire                        | Taille  | Quantité |
|-------------------------------|---------|----------|
| Porte-avion (Carrier)         | 5 cases | 1        |
| Croiseur (Cruiser)            | 4 cases | 1        |
| Contre-torpilleur (Destroyer) | 3 cases | 2        |
| Torpilleur (Torpedo)          | 2 cases | 1        |

### Bonus
- **Code Konami** : Séquence secrète pour recharger tous les pouvoirs
- Animations de personnages inspirées des animés
- Références à la pop culture

## Technologies

- **Java** : 17+
- **Framework** : LibGDX
- **UI** : Scene2D, VisUI
- **Build** : Gradle
- **Tests** : JUnit 5

## Installation

### Prérequis
- JDK 17 ou supérieur
- Gradle (ou utiliser le wrapper inclus)

### Compilation et exécution
```bash
# Compiler le projet
./gradlew build

# Lancer le jeu (version desktop)
./gradlew lwjgl3:run

# Exécuter les tests
./gradlew test
```

Sous Windows, utilisez `gradlew.bat` à la place de `./gradlew`.

### Création du JAR
```bash
./gradlew lwjgl3:jar
```

## Comment jouer

1. Lancer le jeu
2. Choisir le mode de jeu (vs IA ou vs Joueur)
3. Sélectionner la difficulté (si mode IA)
4. Entrer le(s) nom(s) du/des joueur(s)
5. Placer vos navires sur la grille :
   - Cliquer sur un navire dans la liste
   - Cliquer sur la grille pour le placer
   - Utiliser le bouton de rotation pour changer l'orientation
   - Option de placement aléatoire disponible
6. Pendant la partie :
   - Cliquer sur la grille adverse pour attaquer
   - Utiliser les boutons Bombe/Radar pour les pouvoirs spéciaux
7. Le premier à couler tous les navires adverses gagne !

### Contrôles
- **Souris** : Sélection et placement
- **Clavier** : Rotation des navires, Code Konami

## Structure du projet

```
ShipBattle/
├── core/src/main/java/com/par_28/ship_battle/
│   ├── model/
│   │   ├── ai/                # Intelligence artificielle (Easy, Medium, Hard)
│   │   ├── enums/             # Énumérations (GameState, Direction, AttackResult)
│   │   ├── Cell.java          # Cellule de grille
│   │   ├── Coordinate.java    # Système de coordonnées
│   │   ├── Grid.java          # Grille de jeu
│   │   ├── Ship.java          # Classe abstraite des navires
│   │   ├── Player.java        # Joueur
│   │   ├── Game.java          # Logique de partie
│   │   └── AttackResponse.java
│   ├── controller/
│   │   ├── console/           # ConsoleGameController
│   │   └── gui/               # Contrôleurs GUI, dont GameController
│   └── view/
│       ├── console/           # ConsoleView
│       └── gui/               # Vues LibGDX (menus, jeu, etc.)
├── lwjgl3/                    # Module desktop (LWJGL3)
├── assets/                    # Sprites, sons, musiques
└── gdd-assets/                # Assets du Game Design Document
```

## Assets et crédits

Les assets proviennent de sources open source :
- **Navires** : [Naval Battle Assets Pack](https://opengameart.org/content/naval-battle-assets-pack)
- **Radar** : [Animated Radar Assets](https://opengameart.org/content/animated-radar-assets)
- **Explosions** : [Bomb Explosion](https://opengameart.org/content/bomb-explosion)
- **Musiques** : Reprise du jeu **Crimson Skies**

## Documentation

- **Équipe et consignes de travail** : [répartition des rôles](docs/REPARTITION_ROLES.md), classes, UML, Javadoc et conventions de commits à comparer.
- **Game Design Document** : [game design document.md](game%20design%20document.md)
- **Javadoc** : `docs/javadoc/index.html` (fichiers HTML générés, à ouvrir en local)
- **Couverture de code** : `docs/coverage/index.html` (rapport JaCoCo, à ouvrir en local)

La documentation en ligne (GitHub Pages) citée dans la version d'origine de ce README n'est plus disponible.

### Diagrammes UML

- **Modèles** : [uml-model-classes.md](docs/uml-model-classes.md) - Classes du domaine (Game, Player, Ship, Grid, AI)
- **Contrôleurs GUI** : [uml-gui-controllers.md](docs/uml-gui-controllers.md) - Architecture MVC côté contrôleurs
- **Vues GUI** : [uml-gui-views.md](docs/uml-gui-views.md) - Interfaces graphiques et handlers

### Couverture de code (JaCoCo)

| Package            | Couverture Instructions | Couverture Branches |
|--------------------|-------------------------|---------------------|
| `model`            | 99%                     | 97%                 |
| `model.ai`         | 93%                     | 87%                 |
| `model.enums`      | 100%                    | n/a                 |
| `model.exceptions` | 100%                    | n/a                 |

> Note : Les packages `view.gui` et `controller.gui` ne sont pas encore testés pour le moment, leur dépendance à libGDX rend la question plus délicate.

Ces taux sont ceux annoncés par l'équipe pour les packages `model` et `model.ai` ; ils n'ont pas été recalculés. Rapport généré via `./gradlew :core:test :core:jacocoTestReport`.

## Limites connues

- Aucune archive précompilée n'est publiée dans ce dépôt : `RELEASE_NOTES.md` mentionne des archives Windows et macOS qui n'y sont pas disponibles. Le jeu se lance avec Gradle.
- L'interface et les contrôleurs ne sont pas couverts par les tests automatisés.

## Auteurs

Projet universitaire Epitech - 2025

| Prénom | GitHub |
|---|---|
| Chris | [@Crisxzu](https://github.com/Crisxzu) |
| James | [@OhBadBoy](https://github.com/OhBadBoy) |
| Daouda | [@Daoudbamba](https://github.com/Daoudbamba) |

## Licence

Projet universitaire - Usage éducatif
