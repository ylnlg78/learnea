# Direction de design — Atelier Sous-Réseaux

## Trois pistes explorées

| Nom | Intention | Probabilité |
| --- | --- | --- |
| **Blueprint Opératoire** | Une console de travail inspirée des plans techniques d’atelier : précision, repères gradués et apprentissage par manipulation. | 0,07 |
| **Classe Cartographique** | Un environnement lumineux, éditorial et serein, où les notions de réseau prennent la forme de territoires à explorer. | 0,04 |
| **Signal de Nuit** | Une salle de contrôle sombre et dense, ponctuée de signaux lumineux et de données en mouvement. | 0,09 |

## Direction retenue — Blueprint Opératoire

### Mouvement de design

L’interface adopte le langage visuel des **blueprints industriels contemporains** et des carnets techniques : un espace de travail clair, méthodique et légèrement tactile. Cette direction sert l’objectif pédagogique en faisant du sous-réseautage une opération visible plutôt qu’une formule abstraite.

### Principes fondamentaux

L’application privilégie une lecture par couches : le contexte et le résultat sont visibles avant le détail mathématique. Chaque nombre important est ancré dans une représentation spatiale, notamment à travers des segments d’adresses et des blocs binaires. La hiérarchie est volontairement fonctionnelle ; les éléments actionnables affichent un comportement net, les explications restent calmes, et les feedbacks de réussite sont immédiatement compréhensibles. Enfin, la densité technique est contrebalancée par de grands respirations et des zones de travail bien délimitées.

### Philosophie des couleurs

Le fond « papier minéral » très clair installe une atmosphère studieuse et accessible. Le bleu encre incarne le réseau de départ et la fiabilité ; l’orange signal est réservé aux manipulations, aux emprunts de bits et aux appels à l’action. Un vert de validation confirme les réponses justes sans devenir décoratif. Cette opposition bleu/orange crée une lecture instantanée des données et des décisions.

### Paradigme de mise en page

Le poste de travail est organisé comme un établi horizontal : une colonne de navigation compacte pose le parcours, tandis que le canevas principal assemble une zone de raisonnement, un panneau de résultat et un registre pédagogique. Les panneaux ne forment pas une grille uniforme ; ils s’imbriquent selon leur rôle, comme des fiches techniques superposées autour d’un outil central.

### Éléments signatures

Les adresses IP sont découpées en capsules octet par octet, avec une couleur de bordure qui différencie réseau et hôtes. Des règles graduées et des repères de coordonnées parcourent les grandes surfaces. Un fin motif de pixels et de lignes de liaison donne un relief discret, sans nuire à la lisibilité.

### Philosophie d’interaction

Chaque action agit comme une manipulation d’atelier : modifier un préfixe CIDR déplace visiblement la frontière réseau/hôtes, choisir une réponse révèle un feedback local et les raccourcis de parcours donnent toujours une destination claire. Les éléments ne promettent jamais une action inexistante.

### Animation

Les états interactifs suivent une courbe rapide `cubic-bezier(0.23, 1, 0.32, 1)`. Les modules s’installent par un léger décalage vertical et une montée d’opacité ; les barres binaires s’animent uniquement lors des changements de préfixe. Les boutons réagissent par une pression brève. Les animations décoratives disparaissent lorsque l’utilisateur préfère réduire les mouvements.

### Système typographique

**Space Grotesk** porte les titres, compteurs et données chiffrées grâce à son rythme géométrique précis. **DM Sans** assure la lecture courante et les explications. Les adresses, masques et fragments binaires emploient **IBM Plex Mono** afin de matérialiser le code. Les titres sont compactes et structurés, tandis que les paragraphes restent généreusement espacés.

### Essence de marque

**Atelier Sous-Réseaux transforme le CIDR en gestes, repères et décisions compréhensibles pour les personnes qui apprennent l’administration réseau.** Sa personnalité est précise, encourageante et concrète.

### Voix de marque

La voix est directe, rassurante et technique sans jargon inutile. Les titres formulent une action, les appels à l’action annoncent un résultat, et les microcopies expliquent la conséquence d’un choix.

> « Découpez l’espace d’adressage, pas votre confiance. »

> « Déplacez le préfixe. Observez la frontière changer. »

### Mot-symbole et logo

Le symbole est un **nœud de réseau** : quatre petits blocs carrés reliés par deux diagonales, avec un segment orange qui matérialise la séparation réseau/hôtes. Aucun texte n’est intégré au logo ; le mot-symbole est composé avec Space Grotesk en capitales espacées.

### Couleur signature

**Orange balise — `#FF6B35`** : la couleur de décision et de découpage, immédiatement reconnaissable dans l’univers de l’application.

## Style Decisions

Le nœud de réseau et le mot-symbole espacé **ATELIER SOUS-RÉSEAUX** doivent accompagner toute navigation principale, notamment en en-tête sur mobile. Les sections reproduisent le vocabulaire d’un seul atelier : surfaces minérales, réseaux de blocs bleu encre, traits de construction discrets et séparations orange. L’orange reste strictement réservé aux décisions, frontières CIDR, bits empruntés, actions actives et numéraux pédagogiques clés.

La signature **ATELIER SOUS-RÉSEAUX** et son nœud à quatre blocs sont le premier repère de la navigation, avant le parcours et le niveau. Tout module d’exercice ou de validation porte au moins une règle graduée, capsule d’octet, ligne de liaison, repère de coordonnées ou frontière orange. L’orange ne souligne un titre que lorsqu’il nomme une contrainte, une action ou une décision réseau.
