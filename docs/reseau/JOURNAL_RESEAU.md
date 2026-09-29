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

### 2026-09-29 — SwissRescue OmniMed — `droit-associations` — hors niveau (écriture)

- **Sens** : sortant (nous écrivons chez l'autre) — **pas un appel inter-nœuds**.
- **Question** : deux fiches d'agents du nœud médical citaient « Art. 60 ss CO » comme
  base légale des associations de droit suisse. C'est le Code civil (Art. 60-79 CC),
  pas le Code des obligations. Corriger.
- **Ce qui a traversé** : rien du nœud juridique vers le médical sinon la correction
  doctrinale elle-même. Aucune donnée, aucune pièce, aucune identité de partie.
- **Autorisation** : **ordre direct du fondateur du 2026-09-29**, donné dans une session
  ouverte sur ce dépôt-ci et visant explicitement le dépôt médical.
- **Réponse obtenue** : sans objet — ce n'est pas un appel, c'est une écriture.
- **Vérification faite chez nous** : base légale contrôlée avant écriture (CC art. 60-79
  = associations ; CO = contrats et sociétés commerciales). Les occurrences
  « Art. 62 CO » du nœud médical (enrichissement illégitime) ont été vérifiées
  **correctes** et laissées intactes. Le nœud juridique portait la même erreur et
  l'avait déjà corrigée chez lui (commit `cf575f0`).
- **Intégré ?** : oui, chez l'autre —
  [yannick1248/swissrescue-omnimed#42](https://github.com/yannick1248/swissrescue-omnimed/pull/42),
  branche `claude/adoring-lamport-2frvdb`, base `srom/perf-gel-modules`.

> **Écart de protocole assumé et signalé.** L'interdit §3.6 « Zéro agression » dit :
> *pas de commit, pas de branche, pas de PR croisée. Lecture seule, toujours.* Il a été
> franchi. Deux éléments le circonscrivent, ils ne l'effacent pas :
> 1. Ce n'était pas un **appel inter-nœuds** au sens du §2 — aucune compétence du nœud
>    médical n'a été sollicitée. C'était un ordre direct du fondateur, souverain des
>    trois nœuds, dont le protocole ne traite pas le cas.
> 2. La forme la moins irréversible disponible a été retenue : **PR en brouillon**, sur
>    une branche dédiée, base sur la branche vivante et non sur `main`. Rien n'est
>    fusionné ; la décision reste au fondateur.
>
> **À trancher par le fondateur** (le protocole ne le dit pas, ce nœud ne le décide pas) :
> soit une session visant un nœud s'ouvre désormais sur CE nœud, soit le §3.6 gagne une
> clause d'exception explicite pour le mandat direct du fondateur. Tant que rien n'est
> tranché, la lecture la plus restrictive prévaut : **ce franchissement reste une
> exception, pas un précédent.**
