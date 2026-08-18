# Atelier Sous-Réseaux — Conception produit, gamification et analytics

**Document de conception.** Cette proposition prolonge la direction **Blueprint Opératoire** : l’apprentissage n’est pas représenté comme une suite de badges, mais comme la maîtrise progressive d’un établi réseau. Chaque action laisse une trace lisible, chaque erreur est une donnée de diagnostic, et chaque niveau témoigne d’une capacité d’ingénierie concrète.

> **Principe directeur :** le joueur ne « gagne » pas des récompenses décoratives. Il gagne le droit d’opérer sur un espace d’adressage plus complexe, avec davantage de contraintes et moins de guidage.

## 1. Cadre d’expérience et règles visuelles

Le produit doit conserver un fond **papier minéral**, des surfaces de calcul bleu encre, l’orange balise `#FF6B35` pour les décisions actives, et des validations vert-de-gris. Space Grotesk porte les titres, objectifs et grades ; IBM Plex Mono est réservé aux adresses, préfixes, chronomètres, repères et métriques ; DM Sans conserve la lisibilité des explications. Toute fonction d’apprentissage doit incorporer au moins un marqueur de l’atelier : règle graduée, capsule d’octet, ligne de construction, repère de coordonnées ou frontière orange.

| Élément | Rôle UX | Traduction Blueprint Opératoire |
| --- | --- | --- |
| Décision de l’apprenant | Faire comprendre qu’un choix modifie l’espace réseau | Frontière orange, poignée de préfixe, capsule sélectionnée |
| Progression | Rendre la maîtrise visible sans infantilisation | Sous-réseaux stabilisés, rail de parcours, indice de précision |
| Erreur | Faire du raisonnement une étape observable | Fiche de diagnostic à bordure rouge terre cuite |
| Validation | Confirmer une méthode, pas seulement une valeur | Trait vert-de-gris, tampon « méthode validée », bloc verrouillé |
| Temps | Augmenter la tension sans masquer les données | Compteur mono, jauge de session et marqueur `T–` |

## 2. Extension des fonctionnalités pédagogiques

### 2.1. Dépannage de réseau cassé

Le joueur reçoit une topologie qui fonctionne presque : un routeur, deux VLAN et plusieurs hôtes apparaissent sous forme de blocs d’adressage connectés. Un seul paramètre est incohérent — masque, passerelle, plage DHCP, route statique ou chevauchement de sous-réseaux. Il doit **inspecter, isoler puis corriger** la panne en manipulant les capsules d’octets et les liens de la carte.

L’interaction commence par une vue de diagnostic : les paquets animés s’arrêtent au premier segment invalide. L’apprenant tire ensuite une ligne de test entre deux hôtes ou clique sur une interface pour ouvrir sa fiche technique. Il déplace la frontière CIDR ou remplace une adresse ; la carte se recalcule immédiatement. Le système ne révèle pas l’erreur : il indique seulement si le trajet redevient cohérent. La fiche finale expose la cause, le symptôme et le correctif exact.

| Moment | Geste | Feedback | Compétence mesurée |
| --- | --- | --- | --- |
| Observation | Sélectionner un flux ou une interface | Ligne de paquet interrompue | Lecture de topologie |
| Hypothèse | Marquer un segment suspect | Annotation en pointillé | Priorisation du diagnostic |
| Correction | Ajuster masque, route ou passerelle | Recalcul instantané des blocs | Cohérence d’adressage |
| Validation | Relancer le flux | Ligne continue et rapport | Vérification systémique |

### 2.2. Atelier de découpage par contraintes

Cette fonction présente un bloc de départ et une série de contraintes concrètes : « 58 postes bureaux », « 12 imprimantes », « 2 liaisons point à point », « réserve de croissance 20 % ». Au lieu de répondre à une question isolée, le joueur doit **découper un même espace** en plaçant successivement des sous-réseaux sur une règle d’adresses.

Les besoins sont des cartes mobiles ; le joueur les trie d’abord du plus grand au plus petit, puis les pose sur une bande d’adressage. Chaque pose suggère une taille minimale, mais l’apprenant garde la possibilité d’allouer un bloc trop grand. La carte rend immédiatement visibles le gaspillage, les chevauchements et l’espace restant. Cette mécanique transforme le VLSM en un geste de composition spatiale.

La difficulté progresse de la répartition guidée à l’allocation sous contraintes. Aux niveaux avancés, une contrainte de continuité impose de laisser un bloc voisin libre pour une future extension, ce qui force une lecture stratégique plutôt qu’un simple calcul.

### 2.3. Générateur de topologie paramétrique

Le générateur permet de passer de la formule à l’architecture. L’utilisateur choisit le nombre de sites, de départements, de VLAN, de liaisons WAN et une plage IPv4 disponible. L’outil propose un plan, mais le joueur peut **verrouiller certaines décisions** et demander une nouvelle distribution pour comparer les compromis.

La topologie est matérialisée par des nœuds bleu encre et des territoires d’adressage. Les liens et les étiquettes de plage sont en IBM Plex Mono. Un onglet « arbitrages » indique par exemple qu’un choix favorise l’agrégation des routes, tandis qu’un autre préserve davantage de capacité. Le mode entraînement transforme ce générateur en exercice : une topologie est fournie avec deux règles d’architecture à respecter ; l’apprenant doit produire un plan valide.

### 2.4. Relais sous contrainte temporelle

Ce mode complète l’examen actuel par des mini-séquences de 20 à 45 secondes. Une suite alterne calcul de masque, identification de broadcast, allocation VLSM et détection d’un conflit. Le joueur décide de répondre, de passer une question ou d’utiliser un unique « gel de plan » de cinq secondes.

Le geste important n’est pas seulement la rapidité : il s’agit de savoir quand **ne pas s’engager**. Une réponse erronée fait perdre une unité de précision de session ; un passage ne pénalise que le rythme. À la fin, la trace chronologique affiche les secondes consommées, les changements de réponse et les familles de questions qui ont ralenti le joueur.

## 3. Logique de suivi des scores et progression

### 3.1. Score de maîtrise

Le score ne doit jamais être un chiffre opaque. Il est composé de trois signaux visibles et expliqués : **précision**, **rythme** et **propreté de manipulation**. La précision reste dominante afin d’éviter que la vitesse incite à deviner.

| Composante | Calcul proposé | Poids | Lecture d’interface |
| --- | --- | --- | --- |
| Précision | Réponses correctes / réponses soumises | 60 % | Pourcentage bleu encre et sous-réseaux stabilisés |
| Rythme | Temps de résolution comparé à un temps de référence par type d’exercice | 25 % | Courbe fine et repère `T–` |
| Propreté | Première réponse correcte, absence de manipulation annulée, absence de chevauchement | 15 % | Trait vert-de-gris et mention « sans reprise » |

La formule de session est :

> **Indice de maîtrise = (Précision × 0,60) + (Rythme × 0,25) + (Propreté × 0,15).**

Le bonus de propreté est plafonné : il valorise une démarche sûre sans effacer l’impact d’une erreur conceptuelle. Pour les scénarios VLSM et les topologies, la propreté tient compte du respect des contraintes, de l’absence de chevauchement et de l’espace résiduel cohérent. Les scores restent comparables car l’application enregistre aussi le type d’exercice, la difficulté et la durée choisie.

### 3.2. Grades d’ingénierie réseau

Les grades remplacent les étoiles par des fonctions opérationnelles. Ils sont obtenus par l’atteinte conjointe d’un seuil de précision et d’une preuve de compétence, jamais par le temps passé seul. Chaque grade prend la forme d’un **cartouche de plan technique** : code, nom, seuil et territoire maîtrisé.

| Grade | Conditions de déblocage | Preuve attendue | Cartouche visuel |
| --- | --- | --- | --- |
| `G–01 · Opérateur d’octets` | 70 % de précision sur 20 calculs fondamentaux | Lire et convertir un masque | Quatre capsules d’octets alignées |
| `G–02 · Technicien de surface d’adressage` | 75 % sur CIDR et broadcast | Délimiter une plage sans erreur | Bloc /24 quadrillé et frontière orange |
| `G–03 · Planificateur de segments` | 80 % sur VLSM guidé | Allouer trois besoins sans chevauchement | Trois territoires contigus stabilisés |
| `G–04 · Diagnosticien de routage` | 80 % sur réseaux cassés | Identifier la cause avant correction | Ligne de paquet rétablie |
| `G–05 · Architecte CIDR Master` | 85 % sur examen + topologie avancée | Arbitrer capacité, agrégation et croissance | Carte d’adressage multi-sites |

Un grade ne disparaît pas après une mauvaise session. En revanche, le tableau de bord indique un état de **maintenance** lorsque la précision récente descend sous le seuil. Ce vocabulaire protège la motivation : le joueur n’a pas « perdu un niveau », il sait quelle compétence consolider.

### 3.3. Données locales et continuité de progression

Les résultats d’examen doivent être ajoutés à l’historique local, distinctement du score agrégé. Une entrée contient l’horodatage local, la durée choisie — **60 s, 90 s ou 120 s** —, le nombre de réponses, la précision, le temps moyen, le grade courant et un résumé des erreurs. La conservation peut être limitée aux cinquante dernières sessions afin de garder un historique utile sans transformer le navigateur en archive exhaustive.

Le joueur choisit la durée avant le démarrage, via trois segments temporaires. Le choix sélectionné devient orange balise, tandis que les autres restent en bleu pâle. Le temps de référence utilisé pour le calcul du rythme doit être ajusté à la durée et à la difficulté pour éviter qu’une session de 60 s soit injustement comparée à une session de 120 s.

## 4. Conception du panneau de contrôle des scores

### 4.1. Tableau de bord individuel — « Registre de maîtrise »

Le dashboard individuel est un poste de contrôle personnel, et non une page de statistiques générique. Il s’ouvre sur un **cartouche d’identité technique** : grade courant, indice de maîtrise des sept derniers jours, meilleure série et dernière session d’examen. À droite, une carte d’espace d’adressage représente les compétences sous forme de sous-réseaux conquis ; chaque territoire correspond à une famille de compétences, comme CIDR, VLSM, broadcast, diagnostic ou planification.

Les territoires stabilisés sont bleu encre plein ; ceux en consolidation utilisent un bleu-gris hachuré ; une zone à revoir est bordée d’orange, sans être remplie de rouge. Le clic sur un territoire ouvre son registre : taux de réussite, temps médian, dernière erreur, prochaine séance recommandée et accès direct à l’exercice ciblé.

| Zone du dashboard individuel | Données affichées | Forme et interaction |
| --- | --- | --- |
| Cartouche de grade | Grade, seuil suivant, état de maintenance | Fiche technique en angle, code `G–0x`, bouton « voir les conditions » |
| Carte de compétences | Maîtrise par famille de problèmes | Sous-réseaux adjacents ; clic pour explorer une zone |
| Courbe de session | Indice, précision et rythme sur les 12 dernières sessions | Trois lignes de construction fines ; un point orange sur la dernière session |
| Instrument de temps | Temps médian par type de calcul | Règle graduée horizontale avec temps de référence et marqueur personnel |
| Journal d’erreurs | Trois erreurs récurrentes et contexte | Registre mono daté, avec un lien « reprendre ce scénario » |
| Historique d’examen | Date, durée, score, réponses, notions à revoir | Tableau compact, filtrable par 60/90/120 secondes |

La carte de compétences ne doit pas suggérer une conquête militaire. Elle représente un **plan d’adressage stabilisé** : les zones deviennent cohérentes quand les automatismes sont fiables. Une légende précise que la surface est une représentation pédagogique de la maîtrise, non une mesure absolue de compétence professionnelle.

### 4.2. Tableau de bord formateur — « Poste de supervision »

Le formateur voit un groupe comme un ensemble de segments, pas comme un classement public. La vue initiale répartit les apprenants dans une matrice : lignes pour les personnes, colonnes pour les familles de compétences. Chaque cellule est une capsule de sous-réseau colorée par état : stable, en consolidation, à revoir, ou non encore observé. Les noms restent en DM Sans ; les valeurs sont en IBM Plex Mono.

Le premier objectif est l’intervention pédagogique. Une cellule orange ne signifie pas « apprenant faible » : elle signifie « notion nécessitant une séquence de reprise ». Le formateur peut filtrer par session, par durée d’examen, par grade, ou par type de scénario. Un second écran, « lecture de classe », agrège les erreurs les plus fréquentes et montre les temps médians sans exposer un palmarès inutile.

| Vue formateur | Question à laquelle elle répond | Visualisation Blueprint | Action proposée |
| --- | --- | --- | --- |
| Matrice de maîtrise | Qui a besoin d’une reprise sur quelle notion ? | Capsule par compétence et par apprenant | Créer un groupe de remédiation |
| Carte de chaleur des erreurs | Quelle règle génère le plus de confusion ? | Quadrillage bleu pâle avec frontières orange | Lancer un atelier ciblé |
| Distribution des temps | Où le raisonnement ralentit-il ? | Règles graduées avec médiane et quartiles | Ajuster la durée ou revoir une méthode |
| Santé du groupe | Le niveau progresse-t-il de façon homogène ? | Courbes de construction fines par cohorte | Comparer deux séquences pédagogiques |
| File de supervision | Qui est bloqué actuellement dans un scénario ? | Paquets en attente sur une ligne de flux | Ouvrir le dernier diagnostic, sans modifier la réponse |

Le classement individuel est volontairement absent par défaut. Si un contexte de challenge le justifie, la vue « relais » affiche uniquement les équipes ou des identifiants consentis, et privilégie l’indice de progrès de session plutôt que le score brut.

### 4.3. Modèle de données analytiques

Chaque interaction importante est enregistrée comme un événement local ou synchronisable : démarrage de session, réponse, réponse modifiée, dépassement de temps, correction VLSM, ouverture d’un diagnostic et reprise recommandée. Les données conservent le contexte nécessaire à la remédiation ; elles évitent les signaux intrusifs qui n’aident pas l’apprentissage.

| Événement | Champs indispensables | Usage analytique |
| --- | --- | --- |
| `exam_started` | durée choisie, difficulté, grade courant | Segmenter les performances par contrainte de temps |
| `answer_submitted` | type, durée de résolution, réponse, correction, nombre de changements | Calculer précision, rythme et propreté |
| `scenario_resolved` | scénario, contraintes respectées, espace résiduel | Évaluer la planification VLSM |
| `diagnostic_opened` | notion, réponse erronée, durée de lecture | Vérifier l’usage des aides de compréhension |
| `review_recommended` | notion, gravité, exercice proposé | Construire le récapitulatif personnalisé |

## 5. Récapitulatif de révision personnalisé

À la fin d’un examen, la page de résultat ne doit pas se limiter à un score. Elle produit une fiche « **Prochaine intervention** », classée par priorité. La priorité dépend de la fréquence des erreurs, de leur impact et du temps de réponse. Une erreur isolée mais lente est une notion à consolider ; une erreur répétée sur la même règle devient un objectif de reprise.

| Signal observé | Diagnostic généré | Recommandation d’interface |
| --- | --- | --- |
| Confusion /26 et /27 | Bits empruntés non stabilisés | Exercice binaire guidé avec frontière mobile |
| Broadcast régulièrement erroné | Incrément de bloc non identifié | Série de 3 blocs à parcourir sur une règle d’adresses |
| Réponse correcte mais lente | Méthode connue, automatisme insuffisant | Relais de 30 secondes sans pénalité de précision |
| Chevauchement VLSM | Allocation non ordonnée par taille | Atelier de tri puis pose de segments |
| Passage fréquent de question | Contrainte temporelle trop élevée ou notion floue | Revenir à 120 secondes avec diagnostic ouvert |

Le récapitulatif contient trois éléments maximum afin de rester actionnable : une notion prioritaire, une notion à entretenir, et un exercice recommandé. Chaque élément offre un bouton directement formulé comme une action : « Reprendre les incréments de bloc », « Stabiliser les bits empruntés », ou « Allouer trois segments sans chevauchement ».

## 6. Microcopies et feedbacks de performance

La voix reste directe, rassurante et précise. Les retours ne félicitent pas l’apprenant de manière vague : ils nomment la méthode qu’il vient de valider. Les erreurs expliquent le prochain geste sans dramatiser la réponse incorrecte.

### Réussite parfaite

| Situation | Microcopie principale | Précision secondaire |
| --- | --- | --- |
| Calcul exact, premier essai | **« Frontière posée juste. Aucun bit perdu. »** | « /26, 62 hôtes et plage cohérente : méthode validée. » |
| VLSM sans gaspillage | **« Plan stabilisé. L’espace reste exploitable. »** | « Besoins traités du plus grand au plus petit, sans chevauchement. » |
| Diagnostic réseau réparé | **« Flux rétabli. La cause était bien localisée. »** | « La passerelle appartenait à un autre sous-réseau. » |
| Examen à forte précision | **« Session nette : rythme et précision sont alignés. »** | « Consultez le registre pour conserver votre méthode de calcul. » |

### Encouragement après une erreur

| Situation | Microcopie principale | Geste suivant |
| --- | --- | --- |
| Bit emprunté mal placé | **« La frontière a glissé d’un bit. Reprenez l’octet concerné. »** | « Afficher les huit bits du dernier octet. » |
| Masque confondu | **« Le préfixe est bon, mais sa traduction décimale demande un repère. »** | « Comparer /26, /27 et /28 sur la règle. » |
| Broadcast incorrect | **« Le bloc est identifié ; sa dernière adresse reste à fermer. »** | « Visualiser l’incrément et le bloc suivant. » |
| Mauvaise allocation VLSM | **« Le besoin entre dans le plan, mais le bloc choisi est trop étroit. »** | « Reclasser les besoins par capacité. » |
| Temps écoulé | **« Le temps est terminé. La méthode reste récupérable. »** | « Ouvrir la fiche de diagnostic puis relancer à 120 s. » |

### Rapports de fin de session

> **« Session terminée : 8 réponses correctes sur 10. Votre précision est stable ; le temps de calcul du broadcast reste le principal point de friction. »**

> **« Indice de maîtrise : 78. La méthode est acquise sur les masques /24 à /27. Consolidez maintenant les incréments de bloc avant d’ouvrir le niveau VLSM suivant. »**

> **« Aucun chevauchement détecté dans votre plan. Votre prochaine marge de progrès vient de la réserve de croissance : gardez un bloc contigu disponible. »**

> **« Vous avez choisi de passer trois questions. Le diagnostic indique une contrainte de temps, pas une lacune démontrée. Essayez la même séquence en 120 secondes. »**

## 7. Priorité de mise en œuvre

La première itération peut capitaliser sur le mode examen existant : sélecteur 60/90/120 secondes, historique local de session, score de session décomposé et récapitulatif personnalisé. La deuxième itération introduit le tableau de bord individuel, les grades et les diagnostics agrégés. Les scénarios de réseau cassé et le générateur de topologie constituent une troisième itération, plus riche en manipulation, à construire après stabilisation du modèle de données.

| Itération | Livrable | Indicateur de réussite produit |
| --- | --- | --- |
| 1 | Examen configurable, historique local, synthèse de révision | Le joueur comprend la cause de sa dernière erreur et sait quoi refaire |
| 2 | Registre individuel, grades, carte de compétences | Le joueur perçoit une progression par compétence, pas seulement par score |
| 3 | Dépannage, atelier de contraintes, topologie | Le joueur manipule un système réseau complet plutôt qu’une formule isolée |
| 4 | Supervision formateur | Le formateur identifie une notion collective à reprendre sans créer de classement stigmatisant |
