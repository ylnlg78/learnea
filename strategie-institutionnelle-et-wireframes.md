# Atelier Sous-Réseaux — Plan stratégique institutionnel et wireframes Blueprint Opératoire

**Positionnement.** Atelier Sous-Réseaux est un commun numérique d’apprentissage du réseau, publiable en logiciel libre et exploitable sans compte dans son mode individuel. Sa valeur pour les institutions vient de la qualité pédagogique, de l’interopérabilité, de la souveraineté de déploiement et d’une supervision centrée sur les besoins de remédiation plutôt que sur la surveillance des personnes.

> **Décision CPO :** la gratuité ne doit pas être une version dégradée. Le cœur pédagogique, les exercices, les sessions de classe et les analyses de remédiation restent accessibles. Les institutions choisissent ensuite leur mode d’hébergement, d’intégration et de gouvernance.

## 1. Modèle d’adoption et distribution — gratuité totale & communs numériques

### 1.1. Deux expériences complémentaires

L’adoption commence sans friction par l’**Établi Individuel** : un apprenant ouvre l’outil, manipule un réseau et récupère immédiatement son historique sur son appareil. L’**Atelier Classe** ajoute une coordination temporaire et choisie par le formateur ; il ne transforme pas l’application en plateforme de collecte permanente.

| Expérience | Public | Promesse | Identité & données | Point d’entrée |
| --- | --- | --- | --- | --- |
| **Établi Individuel** | Apprenant autonome | « Calculer, visualiser, recommencer, sans demander d’autorisation. » | Aucun compte requis ; progression locale, exportable et supprimable | URL publique, QR code, package hors ligne |
| **Atelier Classe** | Enseignant + groupe | « Lancer une séquence commune, voir les frictions, intervenir au bon moment. » | Code flash, pseudonyme local et session éphémère | Code à six caractères ou QR code de séance |
| **Instance institutionnelle** | DSI, université, CFA | « Garder les données et l’intégration sous gouvernance locale. » | Authentification institutionnelle facultative ; hébergement choisi par l’établissement | LTI, SCORM, URL interne, déploiement on-premise |

L’Établi Individuel conserve les scores, grades, résultats d’examen et diagnostics dans LocalStorage. L’interface explique cette règle sans ambiguïté : **« Vos résultats restent sur cet appareil tant que vous ne les exportez pas ou ne rejoignez pas une session. »** Un panneau permet d’exporter un fichier de progression lisible et de supprimer toutes les données locales. Le stockage local est un choix de minimisation ; il ne suffit pas, à lui seul, à déclarer une conformité juridique complète.

L’Atelier Classe est activé par un formateur qui crée une session courte, par exemple deux heures. Le serveur retourne un code flash et un QR code. L’apprenant entre un pseudo de séance — généré par défaut, modifiable, non associé à un compte — et choisit explicitement de partager ses événements pédagogiques pendant la session. À la fermeture, le formateur peut conserver un agrégat anonymisé, exporter un relevé pseudonymisé ou supprimer l’ensemble.

### 1.2. Répartition des fonctionnalités

Le principe est de réserver l’espace formateur aux capacités qui demandent une orchestration de groupe ou une configuration pédagogique, non aux fonctions qui permettent réellement d’apprendre.

| Cœur ouvert pour tous | Atelier Classe / espace formateur | Motif produit |
| --- | --- | --- |
| Calculateur CIDR, VLSM, diagnostics, topologies simples, mode examen, historique local | Création de séquences, suivi de classe, groupes de remédiation, export de résultats | Besoin de coordination, pas de restriction d’apprentissage |
| Générateur de topologie avec scénarios standards | Générateur avancé avec contraintes pédagogiques, banques partagées, modes de correction | Outil d’auteur et supervision |
| Examen avec aides réglables par l’apprenant | **Examen pur** : aides neutralisées, durée imposée, fenêtre de lancement et restitution contrôlée | Cadre d’évaluation assumé et explicite |
| Dépannage de réseau cassé en solo | Diffusion d’un incident commun, gel de progression, débrief collectif | Animation de séance |
| Export de la progression personnelle | Connecteurs LTI / SCORM, agrégation de cohortes | Interopérabilité institutionnelle |

Le projet peut être distribué sous une licence libre compatible avec les objectifs de partage de code et de contribution, avec une **charte de gouvernance** distincte : comité pédagogique, règles de contribution aux banques de scénarios, documentation de déploiement et politique publique de sécurité. La marque et l’interface restent cohérentes, mais les contenus et scénarios peuvent devenir des ressources réutilisables par les enseignants.

## 2. Fonctionnalités comportementales pour les enseignants — Espace Supervision

### 2.1. Architecture fonctionnelle du portail formateur

Le portail est pensé comme un **poste de supervision**, pas comme une console de surveillance. Sa navigation suit quatre zones : séance, activité, frictions et restitution. Le système cible une classe de trente apprenants ou plus grâce à une matrice dense mais lisible, filtrable et accessible au clavier.

| Module | Fonction | Signal clé | Action du formateur |
| --- | --- | --- | --- |
| **Préparer** | Composer une séquence, choisir difficultés, activer ou non les aides | Contraintes et objectifs de la séance | Publier le code flash |
| **Observer** | Voir l’avancement et l’état de réponse sans lire inutilement chaque donnée | Flux d’activité par notion | Identifier les groupes bloqués |
| **Intervenir** | Déclencher une aide contextuelle ou ouvrir une micro-séquence | Friction persistante | Envoyer une règle, un exemple ou une reprise |
| **Restituer** | Débriefer le groupe et exporter une synthèse | Carte de compétences consolidée | Préparer la séance suivante |

La session temps réel doit manipuler des événements pédagogiques minimisés : type de question, temps de réponse, résultat, tentative, notion et demande d’aide. Les noms réels ne sont nécessaires que si l’institution les apporte via son système d’identité ; ils restent facultatifs dans l’interface de supervision elle-même.

### 2.2. Matrice d’activité en temps réel

La matrice évite le piège d’un leaderboard. Les lignes représentent les participants ou des pseudonymes, les colonnes les compétences. Chaque cellule est une capsule : pleine si la notion est stabilisée, hachurée si elle est en cours, orange bordée si une friction justifie une intervention, gris clair si aucune observation n’est disponible.

```text
┌──────────────────────────────────────────────────────────────────────────────────────────┐
│ ATELIER CLASSE / SÉANCE #6K2P · 27 connectés · 42 min restantes                           │
│ [VLSM guidé] [Examen pur OFF] [Aides: 1 indice]   |  FILTRE : [Tous les groupes ▾]        │
├───────────────────────┬────────┬────────┬───────────┬───────────┬───────────────────────┤
│ APPRENANT / PSEUDO     │ CIDR   │ MASQUE │ BROADCAST │ VLSM      │ ÉTAT ACTUEL           │
├───────────────────────┼────────┼────────┼───────────┼───────────┼───────────────────────┤
│ noah-r17              │ ████   │ ████   │ ▧▧▧▧      │ ░░░░      │ alloue le segment 02  │
│ amina-q09             │ ████   │ ▧▧▧▧   │ ░░░░      │ ░░░░      │ pause / indice lu    │
│ loup-m31              │ ████   │ ████   │ ████      │ ████      │ scénario validé      │
│ groupe B (agrégé)     │ ████   │ ████   │ ▧▧▧▧  !   │ ░░░░      │ friction broadcast   │
├───────────────────────┴────────┴────────┴───────────┴───────────┴───────────────────────┤
│ LÉGENDE : █ stabilisé · ▧ en cours · ! à revoir · ░ non observé                           │
└──────────────────────────────────────────────────────────────────────────────────────────┘
```

Les cellules ne sont jamais rouge vif par défaut : l’orange est une **priorité d’intervention**, pas une note d’échec. Un clic ouvre le dernier diagnostic de la compétence ; le formateur voit la forme de l’erreur, non le détail des réponses précédentes sans nécessité pédagogique.

### 2.3. Détecteur de friction

Le détecteur agrège trois signaux : hausse anormale du temps de réponse, répétition de la même erreur et multiplication des demandes d’indice. Il ne produit pas un diagnostic définitif ; il génère une hypothèse explicite : « Le groupe B semble bloquer sur l’incrément /29 : 11 apprenants concernés, temps médian +48 s. »

```text
┌──────────────────────────────────────────────────────────────────────┐
│ DÉTECTEUR DE FRICTION / DERNIÈRES 10 MINUTES                          │
├──────────────────────────────────────────────────────────────────────┤
│  [ /24 ]────[ /25 ]────[ /26 ]────[ /27 ]────[ /28 ]────[ /29 ! ]    │
│                                   ^                  ^                │
│  temps moyen                  18 s               66 s                 │
│  erreurs de bloc               2                 14                   │
├──────────────────────────────────────────────────────────────────────┤
│ HYPOTHÈSE : incrément de bloc non stabilisé sur le dernier octet.     │
│ ACTIONS : [Projeter une règle] [Lancer 3 exercices ciblés] [Ignorer]  │
└──────────────────────────────────────────────────────────────────────┘
```

Les visualisations utilisent des lignes fines, des valeurs mono et des frontières orange. Elles restent accompagnées d’un tableau de données et d’un texte de synthèse pour ne pas dépendre exclusivement de la couleur ou de la position.

## 3. Wireframes du dashboard individuel et du générateur topologique

### 3.1. Registre de maîtrise individuel

```text
┌──────────────────────────────────────────────────────────────────────────────────────────┐
│ [◫] ATELIER SOUS-RÉSEAUX / REGISTRE DE MAÎTRISE                     [Exporter] [Effacer] │
├──────────────────────────────────────────────────────────────────────────────────────────┤
│ G–03 · PLANIFICATEUR DE SEGMENTS        INDICE 78      PRÉCISION 84 %   SÉRIE 6           │
│ ──────────────────────────────────────────────────────────────────────────────────────── │
│ PROCHAINE CONDITION : 2 scénarios VLSM sans chevauchement                               │
├───────────────────────────────────┬──────────────────────────────────────────────────────┤
│ CARTE DE COMPÉTENCES              │ 12 DERNIÈRES SESSIONS                                │
│                                   │   100 ─┈┈╲╱╲────                                     │
│    [ CIDR ████ ]──[ MASQUE ████ ] │    75 ─────╲──●─                                     │
│            │                      │    50 ─────────────────                              │
│    [ BCAST ▧▧ ! ]─[ VLSM ████ ]   │          s1 s2 s3 ... s12                            │
│            │                      │                                                      │
│    [ DIAG ░░░░ ]──[ TOPO ░░░░ ]   │ Légende : bleu = précision · orange = dernière séance│
├───────────────────────────────────┴──────────────────────────────────────────────────────┤
│ PROCHAINE INTERVENTION                                                               [→]  │
│ « Reprendre les incréments de bloc : /29 reste lent et erroné dans 3 sessions. »         │
└──────────────────────────────────────────────────────────────────────────────────────────┘
```

### 3.2. Générateur topologique — mode apprenant / auteur

```text
┌──────────────────────────────────────────────────────────────────────────────────────────┐
│ GÉNÉRATEUR TOPOLOGIQUE / PLAN D’ADRESSAGE                         [Nouveau plan] [Valider]│
├───────────────────────┬──────────────────────────────────────────────────────────────────┤
│ CONTRAINTES           │ CANEVAS D’ADRESSAGE                                                │
│                       │                                                                  │
│ Plage : 10.40.0.0/22  │    ┌───────────────┐      ┌───────────────┐                       │
│ Sites : [ 3 ▾ ]       │    │ SITE A        │──────│ SITE B        │                       │
│ VLAN / site : [ 2 ▾ ] │    │ 10.40.0.0/24  │      │ 10.40.1.0/25  │                       │
│ Croissance : [20% ▾ ] │    └──────┬────────┘      └───────────────┘                       │
│                       │           │  /30                                                  │
│ BESOINS À POSER       │    ┌──────┴────────┐      ┌───────────────┐                       │
│ [120 hôtes]  [poser]  │    │ ROUTEUR CŒUR  │──────│ SITE C        │                       │
│ [ 50 hôtes]  [poser]  │    │ 10.40.3.0/30  │      │ espace libre  │                       │
│ [ 12 hôtes]  [poser]  │    └───────────────┘      └───────────────┘                       │
├───────────────────────┴──────────────────────────────────────────────────────────────────┤
│ ARBITRAGES : [✓ aucun chevauchement] [✓ 18 % de réserve] [! agrégation à revoir]         │
└──────────────────────────────────────────────────────────────────────────────────────────┘
```

Le geste est volontairement spatial : l’utilisateur trie les besoins, pose les blocs, verrouille un site et observe les routes que le système peut agréger. Chaque manipulation dispose d’un équivalent clavier, d’une étiquette textuelle et d’un diagnostic non coloriel.

## 4. Sécurité, intégration et conformité institutionnelle

### 4.1. Interopérabilité LMS

LTI 1.3 doit être le mode d’intégration privilégié pour l’expérience connectée. La spécification vise l’intégration standardisée d’un outil distant dans un LMS et s’appuie sur un cadre de sécurité ; LTI Advantage couvre notamment le retour de notes, les rôles et le deep linking. [1]

| Niveau | Mécanisme | Données minimales échangées | Cas d’usage |
| --- | --- | --- | --- |
| **LTI 1.3 Core** | Lancement sécurisé de l’outil | Identifiant technique de contexte, rôle, lien de ressource | Ouvrir un atelier depuis Moodle ou Canvas |
| **LTI Assignment & Grade Services** | Colonne et retour de note | Score normalisé, statut, lien de revue | Remonter un examen validé, sans journal détaillé par défaut |
| **LTI NRPS** | Rôles et liste de contexte, activés uniquement si nécessaires | Rôle enseignant/apprenant ; identifiants pseudonymisés | Répartir une classe dans l’Atelier Classe |
| **LTI Deep Linking** | Sélection d’un contenu depuis l’outil | Identifiant du scénario ou de la séquence | Insérer un scénario VLSM préparé dans un cours |
| **SCORM 1.2 / 2004** | Package de contenu et API runtime | Complétion, score, progression minimale | Distribution hors LTI ou catalogue LMS legacy |

SCORM reste un format de distribution complémentaire : son runtime organise le lancement du contenu et la communication de progression avec le LMS dans la session navigateur du SCO. [2] Le package SCORM doit donc privilégier une expérience mono-activité, avec le score final, le statut de complétion et un identifiant de séquence, plutôt que la supervision temps réel.

### 4.2. Souveraineté et protection des données

La trajectoire institutionnelle doit proposer trois options : service local-first sans serveur, instance mutualisée opérée par une structure de confiance, et **auto-hébergement / on-premise**. L’option on-premise comprend un guide d’installation, des variables de configuration documentées, des sauvegardes sous contrôle de l’établissement et une liste d’intégrations désactivables.

Le produit applique la minimisation par défaut : pas de traceur tiers, pas de publicité, pas de profilage comportemental, pas de collecte de géolocalisation, ni d’outil externe de replay. Les statistiques d’usage sont désactivées par défaut dans l’Établi Individuel. En session de classe, les événements sont limités à ceux requis pour le feedback pédagogique et une durée de conservation est visible dans la création de séance.

Le RGPD impose notamment une logique de protection des données dès la conception et par défaut ; les lignes directrices de l’EDPB doivent être traduites en exigences de produit, d’architecture et de gouvernance. [3] Cette stratégie prépare une démarche de conformité, mais une validation juridique, une analyse des traitements et une analyse de risques adaptée à chaque institution restent nécessaires avant tout engagement de conformité.

### 4.3. Accessibilité intégrée à Blueprint Opératoire

La palette bleu encre/orange balise doit rester fonctionnelle sans exclure : l’orange ne peut jamais être le seul porteur de l’état ; toute frontière, erreur ou priorité reçoit une icône, un libellé et une forme. WCAG 2.2 structure les attentes autour de contenus perceptibles, utilisables, compréhensibles et robustes ; la charte se traduit donc par des règles testables. [4]

| Règle d’interface | Application dans Atelier Sous-Réseaux | Vérification |
| --- | --- | --- |
| Couleur non exclusive | État « à revoir » = bordure orange + icône + texte | Test avec styles forcés et lecteur d’écran |
| Contraste et états de focus | Bleu/orange vérifiés sur les fonds minéraux ; focus visible non supprimé | Audit des contrastes et navigation clavier |
| Temps ajustable | Examen 60/90/120 s, pause ou prolongation hors mode d’évaluation contrôlé | Parcours clavier et utilisateur sans contrainte temporelle |
| Structure sémantique | Tableaux, cartes, matrices et diagnostics ont titres, légendes et alternatives textuelles | Lecteur d’écran et inspection DOM |
| Mouvement maîtrisé | Animations de validation courtes, désactivables avec `prefers-reduced-motion` | Test système de réduction des animations |

Pour la France, l’audit doit s’appuyer sur le RGAA et ses critères/tests ; le référentiel fournit une méthode technique à intégrer au processus de recette. [5] L’accessibilité devient une définition de terminé : chaque nouveau scénario, visualisation de sous-réseau ou tableau de supervision est livré avec sa lecture clavier, son équivalent textuel et ses cas de test.

## 5. Feuille de route stratégique

| Horizon | Objectif | Livrables | Décision de succès |
| --- | --- | --- | --- |
| **0–3 mois** | Adoption sans friction | Local-first, export/import, 60/90/120 s, historique d’examen, topologie simple | Un enseignant peut lancer une séance sans créer de comptes apprenants |
| **3–6 mois** | Atelier Classe | Codes flash, matrice, détecteur de friction, export agrégé | Le formateur identifie une notion collective à reprendre en moins d’une minute |
| **6–9 mois** | Interopérabilité | LTI 1.3, AGS, SCORM, guide Moodle/Canvas, paquet on-premise | Une DSI peut intégrer l’outil sans développement propriétaire |
| **9–12 mois** | Commun et gouvernance | Banque de scénarios, contributions documentées, comité pédagogique, audits | Les établissements contribuent à des exercices réutilisables et accessibles |

## Références

[1] [1EdTech — Learning Tools Interoperability](https://www.1edtech.org/standards/lti)

[2] [SCORM — Run-Time Environment](https://scorm.com/scorm-explained/technical-scorm/run-time/)

[3] [European Data Protection Board — Guidelines 4/2019, Article 25](https://www.edpb.europa.eu/documents/guideline/guidelines-42019-on-article-25-data-protection-by-design-and-by-default_en)

[4] [W3C — Web Content Accessibility Guidelines 2.2](https://www.w3.org/TR/WCAG22/)

[5] [DINUM — Référentiel général d’amélioration de l’accessibilité](https://accessibilite.numerique.gouv.fr/)
