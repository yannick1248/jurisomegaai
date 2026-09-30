---
name: meta-competences-juridique
description: >
  Méta-skill de JurisOmegaAI — point d'entrée réseau du nœud juridique. Route une tâche
  vers la bonne compétence juridique (selon son statut réel), et vers les autres nœuds
  (médical, renseignement) sous bac à sable. Subordonné au skill maître `jurisomega-ai`,
  qui l'emporte en cas de contradiction. Déclenche sur : « méta », « toutes les
  compétences », « appelle le médical », « appelle l'OSINT », « réseau », « compétence
  externe ».
---

# Méta-compétences — JurisOmegaAI

Patron réplicable : un méta-skill par projet. Il ne crée aucune compétence : il route.
Doctrine : `jurisomega-ai`. Protocole : `reseau-omega`. Vérité des statuts :
`.claude/skills/reseau-omega/capacites.yaml` (le lire avant d'annoncer quoi que ce soit).

## 1. Carte — selon le statut réel

Implémentées : `jurisomega-ai` (doctrine), `reseau-omega` (protocole), ce méta-skill.
**Toutes les compétences de droit sont `planifie`** (`protection-donnees`, `licite-collecte`,
`droit-sante`, `droit-associations`, `propriete-intellectuelle`, `contrats-partenariats`,
`force-probante`). Face à une question de droit : appliquer la méthode du skill maître §3
(qualifier → source primaire → établi/discuté/à vérifier → adversaire → dater), sans
prétendre qu'une compétence dédiée existe. Ordre de construction : couche 2, priorité 1.

## 2. Emprunts sortants (N0, lecture seule)

- `swissrescue-omnimed` : patron d'organigramme, sourçage, posture adversaire.
- `osint-omega-ai` : `modele-confiance` (backend/app/domain/models.py) pour `force-probante`.
Ne pas copier : on lit et on transpose (zéro doublon).

## 3. Appels entrants

Aucune compétence n'est mobilisable tant qu'elle est `planifie` — répondre par le refus
motivé, pas par une réponse improvisée. Toute analyse fournie porte juridiction, date et
la mention « aide à la compréhension du droit, pas un conseil juridique ».

## 4. Bac à sable

Secret professionnel : rien de couvert ne sort sans mandat écrit et daté (N2). Pièces et
identités de parties jamais dans le dépôt. Ce nœud n'écrit jamais chez un autre.
Tout franchissement → `docs/reseau/JOURNAL_RESEAU.md`.
