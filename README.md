# JurisOmegaAI

**Nœud juridique** du réseau de projets — domicile unique de la compétence juridique,
appelée par les autres projets plutôt que refaite dans chacun.

> ⚠️ **Aide à la compréhension du droit, jamais un conseil juridique.**
> Ce projet n'est ni avocat, ni notaire, ni mandataire. Il éclaire, structure et prépare.
> Il ne conseille pas et ne représente personne. Pour une décision engageante, un
> professionnel mandaté reste nécessaire.

## Stade

**Amorçage.** La doctrine est posée ; les compétences ne sont pas encore construites.
L'état réel de chaque compétence est déclaré dans
[`.claude/skills/reseau-omega/capacites.yaml`](.claude/skills/reseau-omega/capacites.yaml) —
`planifie` tant qu'elle n'existe pas. **Le silence vaut refus.**

## Pourquoi ce dépôt existe

Le besoin juridique naissait dans les trois projets du fondateur et était traité au coup
par coup à l'intérieur du projet médical. C'est un doublon qui coûte : la même question
de protection des données se réinstruisait dans chaque projet, avec des réponses qui
divergeaient silencieusement.

Ici, elle a un seul domicile. Les autres nœuds l'appellent.

## Domaines visés

| Compétence | Objet | Priorité |
|---|---|---|
| `protection-donnees` | nLPD (rév. 1.9.2023) et RGPD — licéité, base légale, conservation, droits | 1 |
| `licite-collecte` | licéité d'une collecte en sources ouvertes (scraping, proportionnalité) | 1 |
| `droit-sante` | logiciel de santé, responsabilité, statut d'un outil non diagnostique | 1 |
| `droit-associations` | droit suisse des associations (Art. 60 ss CC) | 2 |
| `propriete-intellectuelle` | brevets et PCT, droit d'auteur logiciel, marques, licences | 2 |
| `contrats-partenariats` | conventions institutionnelles, NDA, prestataires, hébergement | 3 |
| `force-probante` | qualification de la force probante d'une pièce | 3 |

## Méthode

Qualifier → remonter à la **source primaire** → distinguer **établi** / **discuté** /
**à vérifier** → éprouver en adversaire → dater, signer la juridiction, poser la limite.

Aucune référence fabriquée, jamais. Toute analyse porte sa juridiction et sa date.

## Réseau Oméga

Ce dépôt est un nœud d'un réseau de trois, relié par un protocole à bac à sable :
[`.claude/skills/reseau-omega/SKILL.md`](.claude/skills/reseau-omega/SKILL.md).

- **N0** — la méthode traverse, jamais la donnée (par défaut).
- **N1** — un extrait pseudonymisé traverse.
- **N2** — la donnée brute traverse ; jamais sans mandat écrit et daté.

Il n'existe **aucun appel direct** entre les dépôts : le pont N0 est une lecture, le pont
N1 passe par des enveloppes écrites sous `docs/reseau/`.

## Structure

```
.claude/skills/jurisomega-ai/    skill maître — doctrine, invariants, ordre de travail
.claude/skills/reseau-omega/     protocole inter-projets + manifeste de capacités
docs/reseau/                     enveloppes d'appel, réponses, journal des franchissements
```
