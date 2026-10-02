---
name: meta-competences-juris
description: >
  Méta-skill de JurisOmegaAI — point d'entrée unique qui relie les compétences réelles du
  nœud juridique (skill maître, protocole réseau, manifeste) et sait appeler, sous bac à
  sable, les compétences des deux autres nœuds du Réseau Oméga (médical : méthode de
  sourçage, organigramme ; OSINT : modèle de confiance, vérification de sources). À charger
  dès qu'une tâche juridique déborde le dépôt ou qu'un autre nœud demande une compétence
  juridique. Déclenche aussi sur : « méta », « compétences », « réseau », « appelle le
  médical », « appelle l'OSINT », « bac à sable ».
---

# Méta-compétences JurisOmegaAI

Patron réplicable : un méta-skill par projet. Il **ne remplace pas** `jurisomega-ai`
(skill maître, invariants §0 qui priment) : il l'orchestre vers l'extérieur.
Protocole : `.claude/skills/reseau-omega/SKILL.md` · manifeste qui fait foi :
`.claude/skills/reseau-omega/capacites.yaml` (le lire avant d'annoncer quoi que ce soit).

## 1. Compétences réelles au 2026-10-02

`implemente` : `jurisomega-ai`, `reseau-omega`, `meta-competences-juris`.
Tout le reste (`protection-donnees`, `licite-collecte`, `droit-sante`, `droit-associations`,
`propriete-intellectuelle`, `contrats-partenariats`, `force-probante`) est `planifie` :
**non appelable, silence = refus.** Ordre de livraison : CLAUDE.md, couche 2.

## 2. Appeler les autres nœuds

| Besoin juridique | Nœud | Compétence | Niveau |
|---|---|---|---|
| Méthode de sourçage unitaire, contre-vérification adversaire, patron d'organigramme | OmniMed | veille-medicale, analyste-qualite, entreprise-omnimed (d'après `capacites.yaml`, à vérifier chez eux) | N0 |
| Échelle de confiance, typage des sources, chronologie | OSINT | `modele-confiance` (`planifie` chez eux) | N0 |
| Vérification de sources / de partenaires | OSINT | `verification-sources` (`planifie`) | N0 |

Geste : chercher chez soi → lire le manifeste visé → niveau le plus bas → avis = hypothèse
vérifiée localement → journaliser (`docs/reseau/JOURNAL_RESEAU.md`).

## 3. Être appelé

Les nœuds attendent surtout `protection-donnees`, `licite-collecte`, `droit-sante`,
`droit-associations` — toutes `planifie`. Répondre à une enveloppe N1 par une réponse dans
`docs/reseau/reponses/`, jamais en écrivant chez l'autre. **Une réponse ne peut citer le droit
que sourcé ; sinon « à vérifier ».** Mention « aide à la compréhension, pas un conseil
juridique », juridiction et date en tête.

## 4. Bac à sable

- Secret professionnel : une pièce couverte ne sort qu'en N2, donc jamais sans mandat écrit et daté du fondateur.
- Identité des parties, pièces de dossier : jamais dans le code ni dans une enveloppe non pseudonymisée.
- OmniMed ↔ OSINT sont séparés : le juridique ne sert jamais de passerelle de données entre eux.
- Aucun écrit dans le dépôt d'un autre nœud ; aucun conseil donné à un tiers à la place d'un professionnel.
