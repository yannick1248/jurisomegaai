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

### 2026-09-20 — swissrescue-omnimed — entreprise-omnimed, veille-medicale, methode-fondateur, retrospective-omnimed — N0

- **Sens** : sortant (nous appelons)
- **Question** : swissrescue-omnimed a-t-il publié un manifeste réciproque, et les
  quatre compétences empruntées en besoin (organigramme, sourçage, contre-vérification,
  intention fondateur) y sont-elles mobilisables ?
- **Ce qui a traversé** : rien — lecture de `.claude/skills/reseau-omega/capacites.yaml`
  et des `SKILL.md` du nœud médical (pont de lecture §4.1).
- **Autorisation** : non requise (N0).
- **Réponse obtenue** : oui — manifeste publié le même jour. Trois id confirmés tels
  qu'attendus (`entreprise-omnimed`, `veille-medicale`, `methode-fondateur`) ; le
  quatrième (`analyste-qualite`) n'existe pas chez eux — le rapprochement honnête qu'ils
  proposent est `retrospective-omnimed`. Les quatre sont `implemente`, export N0.
- **Vérification faite chez nous** : correction du `besoin` correspondant dans notre
  propre `capacites.yaml` pour refléter le bon id (`retrospective-omnimed` au lieu de
  `analyste-qualite`) — pas encore appliqué à un livrable, la Couche 3 (organigramme)
  n'a pas commencé.
- **Intégré ?** : non — noté comme mobilisable pour quand la Couche 3 débutera.

### 2026-09-20 — osint-omega-ai — modele-domaine-osint — N0

- **Sens** : sortant (nous appelons)
- **Question** : osint-omega-ai a-t-il publié un manifeste réciproque, et son modèle de
  confiance (attendu pour `force-probante`) y est-il mobilisable ?
- **Ce qui a traversé** : rien — lecture de
  `.claude/skills/reseau-omega/capacites.yaml` et de `osint-omega-ai/SKILL.md`.
- **Autorisation** : non requise (N0).
- **Réponse obtenue** : oui — manifeste publié le même jour, id réel
  `modele-domaine-osint` (`Entity`/`Finding`, échelle `LOW`→`VERY_HIGH`, typage
  `primary`/`secondary`/`community`), `implemente`, export N0. Ce nœud attend en retour
  notre `licite-collecte` (criticité haute) avant de câbler la moindre collecte réelle.
- **Vérification faite chez nous** : correction de la note du `besoin` correspondant
  dans notre `capacites.yaml` pour citer l'id réel.
- **Intégré ?** : non — `force-probante` (priorité 3) n'a pas encore commencé.
