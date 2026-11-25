# Houssix

**Un pentest en boîte blanche, mené par ton agent de code, sur ton abonnement Claude.** Pas de clé API, pas de Docker, pas de cloud.

Houssix est un *skill* pour agents de code (Claude Code, Cursor, Codex… tout ce qui lit un `SKILL.md`). Il empaquette une méthode de revue de sécurité : l'agent lit le code source, reconstruit le modèle d'authentification et d'isolation entre clients, répartit des sous-agents pour chercher les failles (contrôle d'accès cassé / IDOR, injections, contournement d'auth, mass assignment, SSRF, secrets dans le code, fichiers, XSS), **revérifie** chaque faille grave, et écrit un rapport classé par gravité, avec le fichier et la ligne, et le correctif.

Il **lit**, il n'attaque pas : rien n'est exécuté depuis le code cible, aucune requête n'est envoyée vers un serveur en ligne.

## En quoi c'est différent de Strix

| | Strix (open source) | Houssix |
|---|---|---|
| Moteur | binaire + sandbox Docker | ton agent de code |
| Modèle IA | clé API payée à l'usage | ton abonnement (via l'agent) |
| Docker | requis | non |
| Validation Anthropic « cyber » | requise | non (revue par lecture, pas d'exploitation) |
| Preuve | exploit rejoué (PoC) | faille prouvée dans le code |

Houssix ne rejoue pas d'exploit : il prouve la faille en lisant. En contrepartie, il ne touche jamais un serveur et ne coûte rien de plus que ton abonnement.

## Installation

```bash
npx skills add houssematia1/Houssix
```

ou, à la main, copie `skills/security-review/` dans le dossier des skills de ton agent.

## Usage

Dans ton agent, sur le dépôt à auditer :

> Audite ce code avec le skill security-review.

L'agent produit un fichier `rapport-securite.md` dans le projet.

## Règles

- N'audite qu'une cible que tu as le droit d'auditer (ton code, celui de ton employeur, ou celui d'un client avec son accord).
- Les secrets trouvés ne sont jamais recopiés : noms de clés et emplacement seulement.
- Le rapport reste local. Ne le publie pas sans l'accord du propriétaire du code.

## Licence

MIT.
