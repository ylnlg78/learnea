# Atelier Sous-Réseaux — Guides DevSecOps gratuits

**Auteur : Manus AI**  
**Cible :** une application React/Tailwind ouverte aux établissements, sans traqueur commercial ni collecte d’identité.

> **Décision d’architecture.** Utiliser **Cloudflare Pages** pour le frontal statique, car son plan gratuit couvre les déploiements Git/directs, les domaines personnalisés et les requêtes statiques ; la documentation annonce notamment 500 déploiements mensuels au plan Free.[1] [2] Les sessions flash actuellement servies par tRPC ne peuvent toutefois pas rester sur un hébergement purement statique : elles doivent être migrées vers Pages Functions/Workers + D1 ou rester sur une instance institutionnelle. Le présent guide sépare donc le **déploiement de l’interface React** du **service de sessions**.

| Brique | Choix de référence | Données traitées | Coût d’entrée |
|---|---|---:|---:|
| Interface React | Cloudflare Pages | Aucun profil utilisateur | 0 € dans les limites Free |
| Sessions flash | Worker/Pages Functions + D1, ou serveur de l’établissement | Jetons éphémères pseudonymes et états pédagogiques | 0 € dans les limites, à surveiller |
| Mesure d’usage | Umami Community auto-hébergé | Événements agrégés et minimisés | Logiciel libre ; hébergement à fournir |
| CI/CD | GitHub Actions + Wrangler | Artefacts de build et secret de déploiement | 0 € pour dépôt public et dans les limites GitHub |

## 1. Hébergement cloud à coût nul

### Pourquoi Cloudflare Pages

Cloudflare Pages accepte une connexion au dépôt Git, un envoi direct de build et une utilisation par CLI ; les Assets statiques sont ensuite servis depuis le réseau Cloudflare.[1] Pour Atelier Sous-Réseaux, ce choix est plus cohérent que GitHub Pages dès lors que l’on envisage Workers/Pages Functions pour les codes flash et des en-têtes de sécurité. Le plan gratuit est adapté à un pilote scolaire, mais son périmètre doit être surveillé : une offre « gratuite à 100 % » n’est jamais une garantie contractuelle perpétuelle d’un fournisseur. La stratégie souveraine consiste à conserver le code, les exports anonymisés et un plan de repli auto-hébergeable dans le dépôt de l’école.

### Mise en route en moins de deux minutes

La procédure suivante déploie le **frontal** actuellement construit par `pnpm build` dans `dist/public`.

| Étape | Action |
|---|---|
| 1 | Créer un compte Cloudflare et un projet Pages nommé `atelier-sous-reseaux`. |
| 2 | Dans Cloudflare, créer un jeton API limité au compte et au déploiement Pages ; ne pas réutiliser un jeton global. |
| 3 | Dans GitHub, ouvrir `Settings → Secrets and variables → Actions` et ajouter `CLOUDFLARE_API_TOKEN` et `CLOUDFLARE_ACCOUNT_ID`. |
| 4 | Ajouter le workflow de la section 3, puis pousser sur `main`. |
| 5 | Vérifier l’URL `*.pages.dev`, configurer ensuite le domaine de l’établissement et activer les protections DNS proposées par Cloudflare. |

Avant le premier déploiement, le contrôle local minimal reste le suivant :

```bash
corepack enable
pnpm install --frozen-lockfile
pnpm test
pnpm build
# le dossier attendu par le workflow est dist/public
```

> **Point de vigilance full-stack.** Le build Pages ne publie pas `server/_core/index.ts`. Pour conserver les sessions flash réelles, extraire les routes `flash.*` vers une Pages Function/Worker et stocker uniquement `code`, `expiration`, `jeton pseudonyme`, `notion`, `statut`, `horodatage`. Ne jamais transmettre une adresse IP, une adresse e-mail, le contenu libre d’une réponse ou le nom de l’apprenant.

### Configuration de sécurité recommandée

Placer ces en-têtes dans la configuration Pages/Worker afin de limiter les surfaces d’attaque. La politique devra être ajustée si l’instance Umami est ajoutée.

```text
Content-Security-Policy: default-src 'self'; script-src 'self' https://analytics.ecole.example; connect-src 'self' https://analytics.ecole.example; img-src 'self' data: https:; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; font-src 'self' https://fonts.gstatic.com; base-uri 'self'; frame-ancestors 'none'
Referrer-Policy: strict-origin-when-cross-origin
X-Content-Type-Options: nosniff
Permissions-Policy: camera=(), microphone=(), geolocation=()
```

## 2. Surveillance et télémétrie sans traqueur commercial

### Solution retenue : Umami Community auto-hébergé

Umami est un projet open source, auto-hébergeable, conçu pour l’analytics respectueux de la vie privée.[3] Il permet d’enregistrer des événements via attributs HTML ou JavaScript et de filtrer leurs propriétés dans son tableau de bord.[4] Pour préserver la souveraineté, l’instance doit être exécutée sur une infrastructure maîtrisée par l’établissement ou un consortium académique. Le service Umami Cloud n’est pas la cible « coût nul » de cette architecture ; il est préférable de ne pas le présenter comme tel.

La télémétrie doit répondre à une question pédagogique précise : **où le parcours devient-il difficile ?** Elle ne doit pas reconstruire une identité ni produire une relecture invasive de l’écran. L’enregistrement de session, les heatmaps de déplacement et les empreintes de navigateur sont exclus du socle par défaut.

| Événement | Propriétés autorisées | Usage pédagogique |
|---|---|---|
| `cidr_prefix_changed` | `from_prefix`, `to_prefix` | Identifier les plages de préfixes explorées. |
| `exercise_answered` | `concept`, `result`, `elapsed_s`, `difficulty` | Mesurer précision et temps sans enregistrer la réponse textuelle. |
| `bit_boundary_error` | `concept`, `prefix`, `error_family` | Repérer une confusion réseau/hôte ou masque/préfixe. |
| `flash_session_joined` | `session_age_bucket` | Dimensionner les séances sans identifier les postes. |

Les propriétés sont **catégorielles ou numériques bornées**. Ne pas envoyer l’IP analysée, le code flash, le jeton participant, un `userId`, un e-mail, un nom, une URL contenant des paramètres d’identité, ni une durée de session brute si elle peut devenir corrélable à un individu.

### Intégration Umami minimale

Ajouter le script pointant vers l’instance de l’établissement dans `client/index.html`. L’identifiant de site n’est pas un secret, mais l’URL doit rester sous un domaine contrôlé par l’institution.

```html
<script
  defer
  src="https://analytics.ecole.example/script.js"
  data-website-id="REMPLACER_PAR_L_ID_DU_SITE">
</script>
```

Créer ensuite `client/src/lib/telemetry.ts` :

```ts
type TelemetryValue = string | number | boolean;
type TelemetryData = Record<string, TelemetryValue>;

declare global {
  interface Window {
    umami?: { track: (name: string, data?: TelemetryData) => void };
  }
}

export function trackLearningEvent(name: string, data: TelemetryData) {
  // Garde-fou : aucun appel ne doit bloquer l’exercice si l’analytics est absent.
  if (typeof window === "undefined" || !window.umami) return;
  window.umami.track(name.slice(0, 50), data);
}
```

Exemple dans un composant React lors d’une confusion sur la frontière de bits :

```tsx
import { trackLearningEvent } from "@/lib/telemetry";

function onBitBoundaryMistake(prefix: number, elapsedSeconds: number) {
  trackLearningEvent("bit_boundary_error", {
    concept: "network_host_boundary",
    prefix,
    elapsed_s: Math.min(Math.round(elapsedSeconds), 600),
    error_family: "borrowed_bit",
  });
}
```

> **Gouvernance RGPD.** Cette minimisation facilite une analyse de conformité, mais ne constitue pas à elle seule une garantie juridique. Documenter la finalité pédagogique, la durée de conservation, les destinataires, les mesures de sécurité et la procédure d’exercice des droits avec le DPO de l’établissement.

### Supervision de classe : source interne gratuite

Le **dashboard formateur ne dépend pas de l’API Umami**. Il agrège directement les événements éphémères et pseudonymisés des sessions flash : `code` de séance, jeton participant non identifiant, notion, statut pédagogique et horodatage. Il peut donc afficher le nombre de postes actifs, la réussite, les frictions et l’activité par notion même si Umami est désactivé, refusé par l’apprenant ou indisponible.

| Fonction | Source de données | Finalité | Statut de coût |
|---|---|---|---|
| Matrice formateur | Événements flash internes | Accompagner une séance en cours | Inclus dans le service de sessions |
| Indicateurs de rythme et friction | Agrégat des événements internes | Repérer une notion à reprendre | Inclus dans le service de sessions |
| Export CSV pseudonymisé | Agrégat de session | Préparer un bilan de classe | Inclus dans le service de sessions |
| Umami | Événements d’audience après consentement | Comprendre l’usage global du produit | Optionnel ; auto-hébergement recommandé |

> **Règle d’exploitation.** Ne pas mélanger les objectifs. La supervision a une durée de vie courte et sert la classe présente ; Umami est une mesure d’audience facultative, soumise au consentement local et sans rôle dans la matrice formateur.

## 3. Pipeline CI/CD GitHub Actions

Le workflow ci-dessous exécute les tests, le contrôle TypeScript, le build et le déploiement Pages à chaque `push` sur `main`. Cloudflare documente l’usage de Wrangler pour les déploiements Pages en intégration continue ; l’action Wrangler lit le jeton API depuis les secrets GitHub.[5] [6]

Créer le fichier **`.github/workflows/deploy.yml`** :

```yaml
name: Vérifier et déployer Atelier Sous-Réseaux

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read

concurrency:
  group: atelier-pages-production
  cancel-in-progress: true

jobs:
  verify:
    name: Tests et build
    runs-on: ubuntu-latest
    steps:
      - name: Récupérer le dépôt
        uses: actions/checkout@v4

      - name: Installer Node
        uses: actions/setup-node@v4
        with:
          node-version: 22
          cache: pnpm

      - name: Activer pnpm
        run: corepack enable

      - name: Installer les dépendances verrouillées
        run: pnpm install --frozen-lockfile

      - name: Exécuter les tests
        run: pnpm test

      - name: Vérifier TypeScript
        run: pnpm check

      - name: Construire le frontal
        run: pnpm build

      - name: Publier le build statique sur Cloudflare Pages
        uses: cloudflare/wrangler-action@v3
        with:
          apiToken: ${{ secrets.CLOUDFLARE_API_TOKEN }}
          accountId: ${{ secrets.CLOUDFLARE_ACCOUNT_ID }}
          command: pages deploy dist/public --project-name=atelier-sous-reseaux --branch=main
```

Le jeton Cloudflare doit être créé avec le minimum de privilèges nécessaire au déploiement Pages, limité au compte de l’établissement. Il ne doit jamais apparaître dans `wrangler.toml`, un fichier `.env`, le frontend, les logs ou une issue GitHub. Les secrets CI/CD doivent être renouvelés si un membre quitte l’équipe de maintenance.

## Check-list d’exploitation

| Rythme | Contrôle |
|---|---|
| À chaque livraison | Tests, `pnpm check`, build et déploiement automatisé. |
| Mensuel | Vérifier les quotas Pages/Workers, les événements Umami et les dépendances critiques. |
| Trimestriel | Revue des secrets, test de restauration de la sauvegarde chiffrée et vérification de la politique CSP. |
| Annuel | Revue avec le DPO, examen de l’accessibilité et exercice de repli auto-hébergé. |

## Références

[1] [Cloudflare Pages — Overview](https://developers.cloudflare.com/pages/)  
[2] [Cloudflare Pages — Limits](https://developers.cloudflare.com/pages/platform/limits/)  
[3] [Umami — dépôt open source](https://github.com/umami-software/umami)  
[4] [Umami — Track events](https://docs.umami.is/docs/track-events)  
[5] [Cloudflare Pages — Direct Upload with CI](https://developers.cloudflare.com/pages/how-to/use-direct-upload-with-continuous-integration/)  
[6] [Cloudflare Wrangler Action](https://github.com/cloudflare/wrangler-action)
