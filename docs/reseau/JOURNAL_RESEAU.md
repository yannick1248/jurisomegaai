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

### 2026-08-31 — swissrescue-omnimed — expert-associatif (volet juriste) — N0

- **Sens** : sortant (nous empruntons).
- **Question** : l'outil JurisOméga peut-il traiter les dossiers privés du titulaire sur
  l'infrastructure de l'association sans compromettre les conditions de l'exonération
  (exclusivité, désintéressement, cercle ouvert) ?
- **Ce qui a traversé** : rien (N0) — lecture de la note
  `claude/AFFECTATION_module_juridique_SwissRescue.md` du 26.08.2026, produite côté nœud
  médical et sourcée sur la circulaire AFC n° 12 du 8.7.1994. Aucune donnée de dossier
  dans un sens ni dans l'autre.
- **Autorisation** : non requise (N0).
- **Réponse obtenue** : un outil traitant les dossiers privés d'un fondateur sur
  l'infrastructure associative est un retour au fondateur en nature — rupture simultanée
  de l'exclusivité, du désintéressement et du cercle ouvert, qu'aucune clause ne rattrape.
- **Vérification faite chez nous** : lecture la plus restrictive retenue (invariant n° 7
  du skill maître — la prudence est le défaut) ; cohérence vérifiée avec le rattachement
  décidé le 26.08.2026 (activité de l'association, art. 60 ss CC). La circulaire AFC n° 12
  elle-même n'a pas été relue dans ce nœud : sa citation reste portée par la note —
  **à vérifier** lors de la revue trimestrielle du corpus.
- **Intégré ?** : oui — `docs/ARCHITECTURE.md` §0 et §4, `ETAT_PROJET.md`
  (correction v1.1) ; la lecture du 26.08.2026 est journalisée ici le 31.08.2026, à
  l'intégration dans ce dépôt (interdit §3.8).
