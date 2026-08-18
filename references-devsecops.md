# Références DevSecOps vérifiées

- Cloudflare Pages Overview — https://developers.cloudflare.com/pages/ — Pages accepte l’intégration Git, l’envoi direct d’assets et le déploiement via CLI ; la page indique 500 déploiements mensuels pour le plan Free.
- Cloudflare Pages Limits — https://developers.cloudflare.com/pages/platform/limits/ — référence détaillée des limites du plan Free.
- Umami, Track events — https://docs.umami.is/docs/track-events — événements via attributs `data-umami-event` ou JavaScript `umami.track`, avec des propriétés filtrables ; les noms d’événements sont limités à 50 caractères.
- Umami, open source — https://github.com/umami-software/umami — logiciel open source orienté analytics respectueux de la vie privée et auto-hébergeable.
- Cloudflare, intégration continue par Direct Upload — https://developers.cloudflare.com/pages/how-to/use-direct-upload-with-continuous-integration/ — la documentation décrit l’usage de Wrangler pour déployer un build Pages depuis un CI tel que GitHub Actions.
- Cloudflare Wrangler Action — https://github.com/cloudflare/wrangler-action — l’action requiert un jeton API Cloudflare configuré dans les secrets GitHub.
