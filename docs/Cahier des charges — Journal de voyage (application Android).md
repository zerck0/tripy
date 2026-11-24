# Cahier des charges — Journal de voyage (application Android)

Nov 10, 2026 · @Tom

## Présentation

Journal de voyage est une application Android pour garder la trace de ses voyages : on explore les pays, on note ceux qu'on a visités ou qu'on veut visiter, et on tient un journal pour chaque voyage. Pour la rendre plus ludique, l'utilisateur gagne de l'XP et un grade de voyageur selon ses voyages.

C'est le projet de soutenance : Kotlin et Jetpack Compose uniquement, en équipe de 2 à 3.

## Fonctionnalités

**Essentielles**

- Explorer les pays, les rechercher et les filtrer par continent.
- Voir la fiche d'un pays et le marquer « visité » ou « à visiter ».
- Créer des voyages et tenir un journal daté pour chacun.
- Voir ses statistiques : pays visités, continents.
- Consulter ses données sans connexion.

**Importantes**

- Une bucket list des pays à visiter, avec une priorité.
- Un système d'XP et de grades, avec une vitrine de 3 voyages favoris sur le profil.
- Une connexion et un profil.
- Un « pays du jour » mis en avant en haut d'Explorer, qui change chaque jour.
- Pour chaque voyage, une carte avec ses lieux, restaurants et activités, ajoutés par l'utilisateur.

**Bonus**, si le temps le permet : des photos pour chaque voyage.

## Écrans

Quatre onglets en bas de l'écran (Explorer, Bucket list, Mes voyages, Statistiques), deux écrans de détail, plus la connexion et le profil.

- **Explorer** : pays du jour en haut, liste des pays, recherche, filtre par continent.
- **Fiche pays** : infos du pays, boutons « visité » et « à visiter ».
- **Mes voyages** : liste des voyages, étoile pour les mettre en vitrine.
- **Journal du voyage** : deux onglets, le journal (entrées datées) et les lieux (carte, restaurants, activités).
- **Bucket list** : pays à visiter, avec leur priorité.
- **Statistiques** : pays visités, répartition par continent.
- **Connexion** : identification au lancement.
- **Profil** : pseudo, grade, barre d'XP, vitrine.

## Choix techniques

- Kotlin et Jetpack Compose uniquement, sans XML ; thème Material 3 clair et sombre selon le réglage du téléphone.
- Architecture MVVM : écrans, ViewModels, repositories.
- Hilt (injection), Coroutines et Flow, Retrofit (réseau), Room (base locale), Coil (images), Navigation Compose.
- Tests avec JUnit et Mockito ; couverture mesurée avec JaCoCo.
- Carte : Maps Compose (Google Maps). Elle demande une clé d'API, gardée hors de Git et expliquée dans le README.

Le sujet cite Hilt, Coroutines/Flow et Coil. Un mot à l'enseignant pour Retrofit et JaCoCo leverà tout doute.

## Données

- **API** : REST Countries pour les pays (drapeau, capitale, langues, monnaie, continent) et Wikipedia pour le résumé de chaque pays.
- **Room** : sert de cache et garde les données de l'utilisateur (statuts des pays, voyages, entrées de journal, favoris, profil).
- **Principe** : l'écran affiche toujours les données de Room, que le repository met à jour depuis les API. Sans réseau, l'app fonctionne avec ce qui est déjà enregistré, et propose de réessayer en cas d'erreur.
- **Pays du jour** : choisi à partir de la date parmi les pays déjà enregistrés. Il reste le même toute la journée, sans rien stocker, et fonctionne hors ligne.
- **Lieux** : chaque voyage a ses lieux (nom, type, position, note), enregistrés dans Room. On les ajoute par appui long sur la carte. La liste reste consultable sans réseau, même quand la carte ne s'affiche pas.

## Progression

L'XP et le grade se calculent à partir des voyages : ils ne sont pas stockés. Les valeurs ci-dessous sont des propositions à ajuster.

- Pays visité : 100 XP.
- Premier pays visité d'un nouveau continent : 250 XP en plus.
- Voyage créé : 50 XP. Entrée de journal : 10 XP.
- Grades : Touriste (0 XP), Baroudeur (200), Globe-trotter (500), Explorateur (1 000), Légende (2 000).

La vitrine du profil contient 3 voyages favoris au maximum, choisis avec l'étoile de Mes voyages.

## Qualité et équipe

- **Tests** : tests unitaires des ViewModels, des repositories et du calcul de l'XP et du choix du pays du jour, pour couvrir au moins 50 % du code. Chaque branche livre ses tests.
- **Git** : branches `main`, `develop` et une branche par fonctionnalité ; fusion par pull request relue par un autre membre ; commits clairs.
- **Équipe** : chacun prend une zone (données, logique et tests, interface) et contribue avec ses propres commits.

## Planning

Le rendu est dû la veille de la soutenance ; les dates de chaque étape sont à fixer à partir de cette échéance.

1. **Cadrage** : cahier des charges, maquettes, dépôt Git.
2. **Socle** : projet, Room, thème clair et sombre, navigation.
3. **Données** : API, cache, écrans Explorer et Fiche pays.
4. **Journal** : voyages, journal, bucket list, statistiques, progression, lieux et carte.
5. **Qualité** : tests, corrections, finitions.
6. **Rendu** : README, historique Git propre, répétition de la démo.

Si le temps manque, les photos sont abandonnées en premier, puis l'affichage de la carte (la liste des lieux suffit).
