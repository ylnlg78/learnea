# Présentation DevSecOps — Atelier Sous-Réseaux

## Cover

**Atelier Sous-Réseaux**

Déploiement gratuit, télémétrie souveraine et CI/CD pour l’éducation

## Slide 1

### Un atelier ouvert, sans compromis pédagogique

L’expérience reste locale par défaut : progression chiffrée, aucune identité requise et continuité hors compte.

La supervision flash transmet uniquement des signaux pseudonymes, temporaires et utiles au formateur.

La stratégie sépare l’interface publique, le service de session et la mesure d’usage pour préserver la réversibilité.

## Slide 2

### Une architecture gratuite par couches

Cloudflare Pages sert le frontend React statique et les actifs pédagogiques depuis le dépôt.

Les sessions flash sont isolées dans un service minimal, migrable vers Workers + D1 ou l’infrastructure de l’établissement.

Umami Community est auto-hébergé sous un domaine institutionnel pour garder la gouvernance des mesures.

## Slide 3

### Pages est le point d’entrée du déploiement

Le build produit `dist/public`, publié à chaque validation sur la branche `main`.

Le plan Free Pages est adapté au pilote : intégration Git, déploiement CLI et limite documentée de 500 déploiements mensuels.

Un domaine académique et des en-têtes CSP limitent l’exposition du frontal.

## Slide 4

### Mesurer les gestes, pas les personnes

Les événements suivent les changements de préfixe, les réponses d’exercice, les erreurs de frontière et le temps borné de résolution.

Les IP manipulées, codes flash, tokens, e-mails et identifiants d’appareil sont exclus du contrat de données.

Le service Umami est opt-in par configuration : sans variables d’environnement ou service disponible, l’atelier continue normalement.

## Slide 5

### Le contrat Umami est minimal et testable

Le client charge le script uniquement si `VITE_UMAMI_URL` et `VITE_UMAMI_WEBSITE_ID` sont définis.

`trackLearningEvent` valide les noms, borne les valeurs et absorbe toute erreur de télémétrie.

Les composants émettent des événements `practice_answered`, `exam_answered` et `vlsm_answered` sans réponse brute ni donnée personnelle.

## Slide 6

### GitHub Actions sécurise chaque livraison

Chaque push `main` installe les dépendances verrouillées, lance les tests, vérifie TypeScript et construit le frontend.

Wrangler publie ensuite `dist/public` vers Cloudflare Pages avec deux secrets GitHub et un jeton API à privilèges minimaux.

La concurrence du workflow annule les déploiements obsolètes pour limiter les erreurs de publication.

## Slide 7

### Les garde-fous sont intégrés au flux

Les secrets ne sont jamais placés dans le client ni les fichiers versionnés.

La CSP, la minimisation des événements et l’absence de cookies marketing réduisent le périmètre de conformité à examiner avec le DPO.

La réversibilité est maintenue : code ouvert, exports locaux et possibilité d’auto-héberger les services.

## Slide 8

### Un pilote scolaire déployable dès maintenant

1. Créer le projet Pages et les deux secrets GitHub.

2. Configurer une instance Umami institutionnelle et les variables Vite.

3. Déployer sur `main`, puis valider les quotas, la CSP et les événements avec l’équipe pédagogique.

### Sources

Cloudflare Pages, Umami Events et Wrangler Action — documentation officielle.
