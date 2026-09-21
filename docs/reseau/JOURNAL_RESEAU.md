# Journal du Réseau Oméga — nœud JurisOmegaAI

> Registre **append-only** de tous les franchissements de pont vers un autre nœud.
> On ajoute, on ne réécrit jamais (loi de concaténation).
> Protocole : `.claude/skills/reseau-omega/SKILL.md` — interdit §3.8 : *un pont non
> journalisé est réputé n'avoir pas eu lieu.*

## Comment consigner

Une entrée par franchissement, dans les deux sens, en tête de la section « Entrées »
(la plus récente en premier). Ne jamais modifier une entrée existante : si une
information se révèle fausse, ajouter une entrée de rectification qui la cite.

```
### AAAA-MM-JJ — <nœud visé> — <id de la compétence> — N<0|1|2>

- **Sens** : sortant (nous appelons) | entrant (on nous appelle)
- **Question** : une phrase.
- **Ce qui a traversé** : rien (N0) | extrait pseudonymisé (N1) | donnée brute (N2).
- **Autorisation** : non requise (N0/N1) | mandat écrit du fondateur du <date> (N2).
- **Réponse obtenue** : résumé en deux lignes.
- **Vérification faite chez nous** : comment l'avis externe a été éprouvé avant d'être
  intégré (interdit §3.5 — un avis externe est une hypothèse jusqu'à vérification locale).
- **Intégré ?** : oui, où | non, pourquoi.
```

## Entrées

### 2026-09-21 — osint-omega-ai — modele-confiance — N0

- **Sens** : sortant (nous appelons).
- **Question** : le modèle entité/trouvaille/échelle de confiance que ce nœud compte
  emprunter pour bâtir `force-probante` (voir `capacites.yaml`, note_export de cette
  compétence) existe-t-il réellement chez osint-omega-ai ?
- **Ce qui a traversé** : rien (N0) — lecture du code du dépôt osint-omega-ai
  (`backend/app/domain/models.py`).
- **Autorisation** : non requise (N0).
- **Réponse obtenue** : oui, réel et implémenté — `Entity`, `Finding`, `TimelineEvent`,
  `Investigation`, `OsintResult`, `ConfidenceLevel` (`LOW`→`VERY_HIGH`).
- **Vérification faite chez nous** : lecture directe du fichier source, pas de mémoire.
- **Intégré ?** : pas encore — `force-probante` reste `planifie` ici. Le modèle est
  confirmé disponible pour quand cette compétence sera construite.
- **Effet de bord constaté** : au moment de ce pont, osint-omega-ai n'avait aucun
  `.claude/skills/reseau-omega/` — le protocole n'existait que dans ce dépôt, alors que
  `reseau.yaml` dit qu'il doit être identique dans les trois. Corrigé dans la même
  session : propagation de `reseau-omega/SKILL.md` + `reseau.yaml` + un manifeste
  `capacites.yaml` honnête vers osint-omega-ai (PR
  yannick1248/osint-omega-ai#10). Avant cette correction, ce pont N0 n'était donc
  qu'une lecture GitHub directe du dépôt, pas un appel au protocole du nœud cible —
  la nuance est consignée ici pour ne pas prétendre l'inverse plus tard.

### 2026-09-21 — swissrescue-omnimed — entreprise-omnimed / expert-associatif — N0

- **Sens** : sortant (nous appelons).
- **Question** : `capacites.yaml` (`besoins`) cite le patron `entreprise-omnimed` et
  l'agent `expert-associatif` de swissrescue-omnimed comme sources à emprunter pour
  l'organigramme (couche 3 de l'ordre de travail). Ces compétences sont-elles
  réellement atteignables ?
- **Ce qui a traversé** : rien (N0) — lecture du dépôt swissrescue-omnimed.
- **Autorisation** : non requise (N0).
- **Réponse obtenue** : **mitigée**. La branche désignée pour ce nœud dans les
  instructions de session (`claude/pensive-einstein-s50d39`) ne contient AUCUN
  `.claude/` — c'est un historique de déploiement (commits « Deploying to gh-pages
  from… »), déconnecté du code source. Les compétences citées existent bel et bien,
  mais sur une autre branche : `srom/perf-gel-modules` (celle que `reseau.yaml` déclare
  comme `branche_source` pour ce nœud, avec la note « main est figée depuis 2026-05 »).
  Sur cette branche : `.claude/skills/entreprise-omnimed/SKILL.md`,
  `.claude/agents/expert-associatif.md`, et tout l'écosystème d'agents/skills attendu,
  bien réels.
- **Vérification faite chez nous** : `git ls-tree` sur les deux branches distantes de
  swissrescue-omnimed, comparaison directe — pas de confiance sur la seule mention du
  manifeste.
- **Intégré ?** : non — l'organigramme (couche 3) reste `planifie` ici, rien n'a
  changé côté compétences juridiques.
- **À signaler au fondateur** : ce nœud n'a PAS de `.claude/skills/reseau-omega/` sur
  aucune de ses deux branches actives (ni `claude/pensive-einstein-s50d39`, ni
  `srom/perf-gel-modules` au moment du relevé) — swissrescue-omnimed est donc, comme
  osint-omega-ai l'était avant ce jour, déclaré dans `reseau.yaml` sans porter le
  protocole. Cette session n'a PAS propagé le protocole sur
  `claude/pensive-einstein-s50d39` : cette branche semble être la mauvaise base (issue
  du déploiement, pas de la source), et y écrire la doctrine réseau risquait de
  l'enraciner au mauvais endroit. Décision volontairement laissée au fondateur :
  corriger la branche de travail désignée pour ce nœud, ou faire porter la propagation
  du protocole par `srom/perf-gel-modules` directement.
