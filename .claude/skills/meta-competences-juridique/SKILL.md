---
name: meta-competences-juridique
description: >
  Méta-prompt du nœud JurisOmegaAI : point d'entrée unique qui inventorie TOUTES les
  compétences juridiques du projet avec leur statut réel, et sait appeler celles des
  deux autres nœuds (médical, renseignement) via le Réseau Oméga, sous bac à sable.
  À charger au début de toute session sur ce dépôt et dès qu'une tâche déborde du droit
  (méthode multi-agents, échelle de confiance des sources). Déclenche aussi sur :
  « mes compétences », « appelle le médical », « appelle l'OSINT », « bac à sable ».
---

# Méta-compétences — JurisOmegaAI

Patron réplicable : un méta-skill par nœud. Il ne contient aucune compétence, il **route**.
Doctrine : `jurisomega-ai` (skill maître, à lire avant d'agir). Capacités : `.claude/skills/reseau-omega/capacites.yaml`
(fait foi). Protocole N0/N1/N2 : `.claude/skills/reseau-omega/SKILL.md`.

## Séquence obligatoire

1. Lire `CLAUDE.md`, le skill maître, puis `capacites.yaml` (statuts réels, jamais de mémoire).
2. Une compétence `planifie` n'est pas appelable ni annonçable : le silence vaut refus.
3. Tâche hors droit : identifier le nœud (tableau), lire son manifeste (N0, lecture seule), appliquer la méthode chez soi.
4. Niveau le plus bas qui répond. N1 = enveloppe pseudonymisée dans `docs/reseau/appels/`. N2 = mandat écrit et daté du fondateur, par tâche.
5. Journaliser dans `docs/reseau/JOURNAL_RESEAU.md`. Avis externe = hypothèse à vérifier ici.

## Carte des neurones

**Chez nous (priorité de construction, ordre des couches du CLAUDE.md) :**
`protection-donnees` (1) → `licite-collecte` (1) → `droit-sante` (1) → `droit-associations`, `propriete-intellectuelle` (2) → `contrats-partenariats`, `force-probante` (3). Tous `planifie` au 2026-10-08.

**Chez les autres :**

| Besoin | Nœud | Compétence | Niveau max |
|---|---|---|---|
| Patron d'organigramme, sourçage unitaire, contre-vérification adversaire | SwissRescue OmniMed | voir son manifeste | N0 |
| Modèle entité/trouvaille/chronologie, échelle de confiance | OSINT Oméga AI | `modele-confiance` (`partiel`) | N0 |

## Bac à sable propre à ce nœud

- Le secret professionnel ne quitte pas le nœud sans mandat écrit (N2). Ce que nous offrons aux autres est la **méthode** (N0), jamais un dossier.
- Entrant : toute demande exige juridiction, date, et la mention « aide à la compréhension, pas conseil juridique ».
- Zéro fiction juridique : si une compétence n'est pas livrée, répondre « à vérifier » et escalader à un humain, ne pas improviser.
- Aucune écriture dans un autre dépôt. Lecture seule.
