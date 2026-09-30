# ShipBattle — répartition des rôles et règles de travail

Ce document consigne la répartition initiale déclarée entre **Chris, Daouda et James**, ainsi que les consignes communes de développement. Dans le message d'origine, « Moi » désigne **Chris**.

La date de la consigne historique est **inconnue**. Elle a été retransmise le **30 septembre 2026** ; cette date est celle de la transmission, pas celle du début du projet ni des contributions. Le projet universitaire est présenté dans le [README](../README.md) comme un projet de 2025.

Une responsabilité initiale décrit le travail prévu pour un participant. Elle ne démontre pas une réalisation complète, ni l'auteur exclusif de chaque évolution d'une classe. Les contributions effectivement réalisées se vérifient dans le [code](../core/src/main/java/com/par_28/ship_battle/) et l'[historique du dépôt](https://github.com/OhBadBoy/Ship-Battle/commits/main/).

## Répartition déclarée

| Participant | Responsabilités initiales |
|---|---|
| **Chris** | Mettre en place la base du projet, puis préparer les branches ; prendre en charge le contrôleur de jeu `GameController` dans `controller`, `ConsoleView` dans `view`, ainsi que `Player` et `Game` dans `model`. |
| **Daouda** | Prendre en charge les classes `Grid`, `Cell` et `Coordinate` ; rechercher avec James comment rédiger la Javadoc, étudier les conventions de commits proposées et exprimer sa préférence. |
| **James** | Prendre en charge la classe abstraite `Ship` et ses descendants, `AttackResponse`, ainsi que les enums `AttackResult`, `Direction` et `GameState` ; effectuer avec Daouda les recherches sur la Javadoc, étudier les conventions de commits proposées et exprimer sa préférence. |
| **Tous les trois** | Documenter complètement leur travail dès le début ; écrire une Javadoc en anglais, brève et concise ; respecter l'UML, ses attributs et ses méthodes ; appliquer et vérifier la convention de commits une fois celle-ci choisie. |

## Classes et chemins actuels

Les chemins suivants ont été vérifiés dans le code présent lors de cette mise à jour. Tous partent de `core/src/main/java/com/par_28/ship_battle/`. Les packages ont évolué par rapport aux noms génériques `controller`, `view` et `model` de la consigne initiale.

| Élément de la consigne initiale | Responsable initial | Chemin actuel vérifié |
|---|---|---|
| `GameController` : contrôleur du parcours console | Chris | [`controller/console/ConsoleGameController.java`](../core/src/main/java/com/par_28/ship_battle/controller/console/ConsoleGameController.java) ; le nom actuel est `ConsoleGameController`. |
| `ConsoleView` | Chris | [`view/console/ConsoleView.java`](../core/src/main/java/com/par_28/ship_battle/view/console/ConsoleView.java) |
| `Player` | Chris | [`model/Player.java`](../core/src/main/java/com/par_28/ship_battle/model/Player.java) |
| `Game` | Chris | [`model/Game.java`](../core/src/main/java/com/par_28/ship_battle/model/Game.java) |
| `Grid` | Daouda | [`model/Grid.java`](../core/src/main/java/com/par_28/ship_battle/model/Grid.java) |
| `Cell` | Daouda | [`model/Cell.java`](../core/src/main/java/com/par_28/ship_battle/model/Cell.java) |
| `Coordinate` | Daouda | [`model/Coordinate.java`](../core/src/main/java/com/par_28/ship_battle/model/Coordinate.java) |
| `Ship` (classe abstraite) | James | [`model/Ship.java`](../core/src/main/java/com/par_28/ship_battle/model/Ship.java) |
| `Carrier` (descendant de `Ship`) | James | [`model/Carrier.java`](../core/src/main/java/com/par_28/ship_battle/model/Carrier.java) |
| `Cruiser` (descendant de `Ship`) | James | [`model/Cruiser.java`](../core/src/main/java/com/par_28/ship_battle/model/Cruiser.java) |
| `Destroyer` (descendant de `Ship`) | James | [`model/Destroyer.java`](../core/src/main/java/com/par_28/ship_battle/model/Destroyer.java) |
| `Torpedo` (descendant de `Ship`) | James | [`model/Torpedo.java`](../core/src/main/java/com/par_28/ship_battle/model/Torpedo.java) |
| `AttackResponse` | James | [`model/AttackResponse.java`](../core/src/main/java/com/par_28/ship_battle/model/AttackResponse.java) |
| `AttackResult` | James | [`model/enums/AttackResult.java`](../core/src/main/java/com/par_28/ship_battle/model/enums/AttackResult.java) |
| `Direction` | James | [`model/enums/Direction.java`](../core/src/main/java/com/par_28/ship_battle/model/enums/Direction.java) |
| `GameState` | James | [`model/enums/GameState.java`](../core/src/main/java/com/par_28/ship_battle/model/enums/GameState.java) |

La correspondance du contrôleur décrit son rôle dans le parcours console, sans prétendre démontrer un renommage historique. Le code contient également un [`controller/gui/GameController.java`](../core/src/main/java/com/par_28/ship_battle/controller/gui/GameController.java), qui étend `GuiController` et gère des vues LibGDX. Le nom `GameController` de la consigne initiale ne suffit pas à attribuer exclusivement ce contrôleur GUI actuel à Chris.

L'UML actuel comporte d'autres éléments, notamment l'IA, `PowerType` et `AIDifficulty`. Ils ne reçoivent pas de propriétaire individuel par déduction dans cette répartition initiale.

## UML et contrats entre les classes

Le [diagramme des classes du modèle](uml-model-classes.md) donne les attributs, méthodes et relations à respecter. Les [contrôleurs GUI](uml-gui-controllers.md) et [vues GUI](uml-gui-views.md) disposent de leurs propres diagrammes pour l'interface actuelle.

Chaque participant doit vérifier la cohérence de ses classes avec l'UML : noms et types des attributs, visibilité, signatures des méthodes et relations entre classes. Si un besoin impose une évolution, le code et la documentation doivent rester cohérents ; la répartition ne permet pas de modifier silencieusement le contrat partagé.

| Interface entre responsabilités | Coordination attendue |
|---|---|
| `Game` / `Player` / `Grid` | Chris et Daouda coordonnent le déroulement de la partie, le placement et les attaques. |
| `Grid` / `Cell` / `Coordinate` / `Ship` | Daouda et James coordonnent positions, orientation, occupation des cases et dégâts aux navires. |
| Attaques et états | James fournit les contrats `AttackResponse`, `AttackResult`, `Direction` et `GameState` ; Chris et Daouda les utilisent dans leurs classes. |
| Contrôleur / vue console / modèle | Chris relie les entrées et affichages console au déroulement de la partie, en utilisant les classes du modèle fournies par l'équipe. |

## Documentation et Javadoc

La documentation complète est une responsabilité **commune dès le début du développement**. Les recherches confiées à Daouda et James n'en font pas les seuls rédacteurs : chacun documente son code et les interfaces dont dépendent les autres.

La Javadoc doit être **en anglais, brève et concise**. Elle doit expliquer le rôle des classes, les attributs utiles et le comportement des constructeurs et méthodes, avec les paramètres, valeurs retournées et exceptions lorsque cela s'applique. Une formulation courte doit rester assez précise pour comprendre le contrat, sans répéter inutilement l'implémentation.

Avant d'envoyer une modification, vérifier que la documentation correspond au comportement et aux signatures du code, et que l'UML reste cohérent. La présente consigne ne certifie pas que toute la documentation existante est déjà complète ou correcte.

## Conventions de commits : comparaison et décision

Chris a présenté les deux références transmises par Hugo. Daouda et James ont pour responsabilité initiale de les étudier, de les comparer et de dire laquelle ils préfèrent ; la proposition de ces options ne leur est pas attribuée. Les références à étudier sont les suivantes :

| Option | Principe | Points à comparer pour l'équipe |
|---|---|---|
| [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/) | Un type textuel, un scope facultatif et une description ; les changements incompatibles peuvent être signalés par `!` ou `BREAKING CHANGE`. | Structure exploitable par des outils, distinction des fonctionnalités et corrections, règles communes de rédaction. |
| [Gitmoji](https://gitmoji.dev/) | Des emojis ou leurs codes identifient la nature d'une modification, par exemple une fonctionnalité, un correctif ou une modification de documentation. | Lisibilité visuelle, choix d'un emoji cohérent et format retenu par l'équipe. |

**Choix non confirmé :** la consigne transmise ne précise pas quelle convention a finalement été adoptée. Ce document ne déclare donc l'adoption ni de Conventional Commits, ni de Gitmoji, ni d'une combinaison des deux. La comparaison doit conduire à un choix commun consigné explicitement.

**Une fois la convention choisie**, chaque participant doit la respecter et vérifier ses messages de commits **avant leur envoi** : structure conforme, type ou emoji approprié et description fidèle aux changements. Cette règle ne demande pas de réécrire rétroactivement l'historique existant.

## Branches

La mise en place de la base du projet et la préparation des branches relèvent du rôle initial de **Chris**. Aucun nom, nombre ou format de branche Java n'a été fourni dans cette consigne : ce document n'en invente pas. Les règles des 14 branches d'EpiTalk concernent un autre projet et ne s'appliquent pas à ShipBattle.

## Contributions supplémentaires et portée de l'attribution

Le [README](../README.md#contributions-de-james) et l'[historique des contributions de James](https://github.com/OhBadBoy/Ship-Battle/commits/main/?author=OhBadBoy) documentent aussi son travail supplémentaire sur le placement des navires avec LibGDX : aperçu suivant le curseur, rotation, alignement sur les cases, changement de sélection, réinitialisation, validation avant la partie et adaptation de la mise en page à la fenêtre. Cette contribution complète son périmètre initial ; elle doit être conservée dans la présentation du projet.

L'intelligence artificielle, la suite de tests et la couverture de code restent présentées comme des travaux d'équipe. La matrice initiale n'attribue pas automatiquement à un participant toutes les fonctionnalités ajoutées ensuite dans une classe, ni l'intégralité de l'interface graphique.
