# Documentation Produit – F-ing Ship

**Version du document** : 1.1  
**Date** : 24 mars 2026   
**Objectif du document** : Vision du projet. Référence pour le développement, le design et le contenu.

---

## 1. Vision du Jeu

**Titre officiel** : F-ing Ship  
**Tagline** : « Ton vaisseau est une merde. Fais-en une légende. »

Jeu de gestion browser ultra-simple, trashy et addictif dans l’esprit de *La Brute*, mais sur le thème spatial et vaisseaux spatiaux.  
Aucun moteur 2D/3D : tout se passe via des interactions web classiques (clics, formulaires, rapports texte).  

Tu reçois un tas de ferraille volante dès la création du compte et tu passes ton temps à le faire évoluer en le jetant dans des combats PvP, des missions à risque et des upgrades ridicules.  
Le ton est **space-punk** : néons qui clignotent, peinture écaillée, jurons, humour noir et gros ego. Tout le monde bosse pour l’**Empire Galactique** et doit allégeance à l’**Empereur** (qui est clairement un gros con, mais on l’aime bien).

**Public cible** : Hommes 18-35 ans, fans de jeux de gestion old-school, memes et humour bien trash.  
**Langues** : Français & Anglais (100 % bilingue dès le départ).

---

## 2. Mécaniques de Base (Version 1.0 – Un seul vaisseau)

### 2.1 Création & Onboarding
- Compte créé → 1 vaisseau gratuit (modèle de base : « Tas de Boulons Mk I »).
- Le vaisseau reçoit **un skin (image) randomisé** parmi une liste prédéfinie de skins de base.
- Le joueur peut **personnaliser le nom de son vaisseau** dès la création (et le changer plus tard).
- Tutoriel très court et humoristique (3 écrans max).

### 2.2 Statistiques du vaisseau
| Stat          | Nom en jeu          | Effet                                      |
|---------------|---------------------|--------------------------------------------|
| Attaque       | **Punch**           | Dégâts de base + puissance des compétences |
| Vitesse       | **RPM**             | Fréquence de tours (plus haut = joue plus souvent) |
| Coque         | **Durabilité**      | Points de vie                              |

### 2.3 Progression & Rangs
- **EXP de rang** : gagne uniquement en PvP.
- À chaque palier d’EXP max → l’EXP se **cap** jusqu’à ce que le joueur achète l’**Amélioration de Rang**.
- À chaque rang up → choix entre **3 bonus** (compétence active / passif / boost de stat).
- Exemple de progression visuelle (noms à confirmer) :
  - Rang 1 : Épave
  - Rang 2 : Poubelle Volante
  - Rang 3 : Ferraille Armée
  - Rang 4 : Ça Commence à Ressembler à Quelque Chose
  - … jusqu’à des noms complètement absurdes et épiques.

### 2.4 Ressources
- **Fémur Galactique** (monnaie principale) : récompenses missions uniquement.
- **Foktonium** :
  - +1 toutes les 10 minutes
  - Max 20
  - Sert uniquement à lancer un combat PvP contre un autre joueur.

### 2.5 Combats PvP
- Instantanés côté serveur.
- Rapport de combat détaillé et **hilarant** (style log de combat La Brute + commentaires sarcastiques).
- Système tour-par-tour basé sur la **vitesse** :
  - Exemple : 100 RPM vs 50 RPM → ordre A A B A A B …
- Chaque tour : 50 % chance attaque de base / 50 % chance compétence active (si le vaisseau en a).
- Passifs : se déclenchent automatiquement (début/fin de tour, prise de dégâts, etc.).
- **Récompense** : uniquement de l’**EXP de rang**.

### 2.6 Missions Quotidiennes
- 3 missions aléatoires chaque jour (reset à 00:00 UTC).
- Types :
  - **Livraison** (temps fixe, pas de risque)
  - **Exploration** (temps + petite chance de bonus/loot)
  - **Combat** (le vaisseau part, combat auto contre PNJ, succès selon stats/compétences)
- Pendant la mission le vaisseau est **verrouillé** (possibilité de rappel prématuré = mission ratée).
- **Récompense** : uniquement du **Fémur Galactique**.

---

## 3. Thème & Style (Space Punk Trash)

Ton des textes : très vulgaire mais jamais gratuit.  
Exemple : « Ton tas de ferraille vient de se faire démonter par un vaisseau qui pue encore moins que le tien. Bravo champion. »

---

## 4. Interface Utilisateur

**Pages principales (React Router)**

1. **Hangar** (home) – Vue principale du vaisseau + stats + rang actuel + bouton renommer
2. **Arène** – Liste des joueurs à défier (filtré par rang proche) + bouton “Dépenser 1 Foktonium”  
   → Sous-page **Rapports PvP** (historique des combats PvP)
3. **Missions** – Les 3 du jour + timer + bouton “Rappeler”  
   → Sous-page **Rapports Missions** (historique des missions)
4. **Améliorations** – Arbre des rangs + choix des 3 bonus
5. **Profil** – Stats globales, titre ridicule, skins équipés, et section **Flex Kills** (historique manuel que le joueur choisit d’enregistrer pour montrer ses plus beaux rapports)

**Design** : mobile-first.

---

## 5. Roadmap

**Version 1.0 (MVP – ce qu’on code maintenant)**
- 1 seul vaisseau
- PvP + missions + progression rang
- Tout le système de combat et rapports
- Auth + base de données (Prisma + Turso)
- Jour de l’Empereur : double Foktonium tous les dimanches (événement récurrent V1)

**Version 1.1 / 1.2 (mises à jour sociales – 3-6 mois)**
- Système d’**Alliance** (simple regroupement de joueurs avec bonus collectifs)
- Batailles d’alliances
- Messagerie in-game
- Autres features sociales

**Version 2.0 / 3.0 (futur)**
- Plusieurs vaisseaux (déjà pensé dans la DB : un joueur pourra posséder techniquement une liste de `Ship` ; mais il en possèdera qu'un, le multi-vaisseau ne sera pas conçu dès maintenant, ça arrivera plus tard ou jamais).

---

## 6. Idées de fonctionnalités validées

- **Titres ridicules** : à chaque rang up le joueur débloque un titre visible dans l’arène (« Capitaine de la Ferraille », « Empereur des Poubelles », « Flingueur de Mères de l’Hyperespace »).
- **Skins cosmétiques supplémentaires** : uniquement payants via boutique (future version).
- **Événements temporaires** : Jour de l’Empereur (double Foktonium tous les dimanches) déjà en V1.
- **Flex Kills** : le joueur peut enregistrer manuellement un rapport de combat sur son profil pour flex (pas automatique, pas tout l’historique).
- **Notifications push** : via service worker (« Ton Foktonium est plein, viens te battre enfoiré ! »).

## 7. Liste des rangs

20 rangs au total.

1. Épave
2. Tas de Boulons
3. Poubelle Volante
4. Ferraille Rouillée
5. Merde Orbitale
6. Cafetière Spatiale
7. Navette de Déchetterie
8. Corbillard Cosmique
9. Bricolage Spatial
10. Chasseur de Pacotille
11. Vaisseau Qui Fait Le Job
12. Rafiot Respectable
13. Destroyer de Proximité
14. Frégate de Guerre
15. Croiseur Lourd
16. Vaisseau d’Assaut
17. Maraudeur Galactique
18. Destructeur Stellaire
19. Conquérant des Étoiles
20. Légende Galactique

## 8. Exemples de lignes de textes

Toutes dans le style space-punk trashy/humoristique du jeu (vulgaire mais jamais gratuit, sarcasme à fond, ego bien gonflé, allégeance à l’Empereur).

### 1. Notifications & Infos générales (10 lignes)
1. Ton Foktonium est plein à craquer, enculé. Va démonter du vaisseau avant que je m’énerve.
2. L’Empereur te regarde. Et il se marre. Bouge ton cul et va te battre.
3. +1 Foktonium. T’as encore 19 chances de te faire humilier aujourd’hui.
4. Ton tas de ferraille est prêt à voler. Enfin… si on peut appeler ça voler.
5. Mission terminée. Ton vaisseau pue la sueur et la gloire. Bien joué, champion.
6. T’as pas assez de Fémur Galactique, pauvre merde. Retourne bosser.
7. L’Empire te remercie d’exister. Même si c’est à peine.
8. Ton vaisseau vient de roter. C’est bon signe, il est motivé.
9. Attention : ton rang est encore une blague. Monte ou crève.
10. L’Empereur a parlé : « Arrête de faire pitié et va casser du cul. »

### 2. Rapports de Combat – Victoire (10 lignes)
11. Ton opposant vient de se faire démonter comme une vieille conserve. Victoire écrasante, sale bête.
12. Tu l’as pulvérisé. L’Empereur est fier… ou il était bourré, on sait pas.
13. L’autre connard a fini en confettis spatiaux. Bien joué, tas de boulons.
14. Victoire ! Ton vaisseau a dansé sur son cadavre. Respect.
15. Il a pleuré comme une princesse de l’hyperespace. Toi t’as juste ri.
16. Écrasé, humilié, orbitalisé. C’est beau ce que tu fais.
17. L’Empire te doit une bière. T’as fait du propre aujourd’hui.
18. Il reste plus rien de l’autre vaisseau. Juste de la fumée et de la honte.
19. Ton RPM a tout défoncé. L’autre a même pas eu le temps de dire « maman ».
20. Victoire totale. T’es officiellement moins nul qu’hier.

### 3. Rapports de Combat – Défaite (10 lignes)
21. Ton tas de ferraille s’est fait démolir. Bravo champion, t’as perdu contre une épave.
22. L’autre t’a marché dessus comme sur une merde de chien stellaire. Bienvenue en bas.
23. Défaite. Ton vaisseau est rentré en pleurant. L’Empereur est déçu.
24. T’as pris cher. Très cher. Genre « je vais devoir changer de slip » cher.
25. L’adversaire t’a recyclé en pièces détachées. C’est presque poétique.
26. Défaite humiliante. Même ton propre vaisseau a honte de toi.
27. Il t’a enculé si fort que t’as vu les anneaux de Saturne.
28. Retour à l’Empereur les mains vides et le cul en feu. Prochain coup on fait mieux.
29. T’as perdu. Ton rang vient de baisser d’un cran dans mon estime.
30. L’autre vaisseau t’a transformé en feu d’artifice. Magnifique… pour lui.

### 4. Missions & Résultats (10 lignes)
31. Mission livraison réussie. Ton vaisseau pue encore le colis et la sueur.
32. Exploration terminée. T’as trouvé que dalle mais au moins t’as pas explosé.
33. Mission combat : succès. Le PNJ a fini en orbite basse. Bien joué.
34. Mission ratée. Ton vaisseau est rentré la queue entre les réacteurs.
35. Livraison terminée. L’Empereur te remercie… en te donnant des cacahuètes.
36. Exploration : jackpot ! T’as ramené un bout de ferraille qui pue le profit.
37. Combat de mission réussi. T’as cassé du cul comme un pro.
38. Mission annulée. T’as rappelé ton vaisseau comme une mauviette. Dommage.
39. Bien joué, la mission est validée. Ton Fémur Galactique sent bon la victoire.
40. Mission foirée. L’Empire note : « ce pilote est une déception intergalactique ».

### 5. Montée de rang & Améliorations (5 lignes)
41. Rang up ! T’es plus une simple épave. T’es une épave avec de l’ambition.
42. Amélioration achetée. Ton vaisseau vient de passer de « poubelle » à « poubelle qui tue ».
43. Choix de bonus effectué. L’Empereur approuve… ou il s’en bat les couilles.
44. Nouveau rang débloqué. T’es officiellement moins ridicule qu’avant.
45. T’as passé le cap. Ton vaisseau bande rien qu’à l’idée de se battre.

### 6. Divers / Hangar / Arène / Profil (5 lignes)
46. Ton vaisseau est beau comme un camion poubelle après la pluie. Respect.
47. Dans l’arène, tout le monde te regarde. Surtout pour se marrer.
48. Profil mis à jour. T’as toujours l’air d’un loser, mais un loser qui progresse.
49. Renommage validé. « Le F-ing Ship Ultime » sonne mieux que « Merde Volante ».
50. L’Empire te surveille. Et il se demande encore pourquoi il t’a donné un vaisseau.

