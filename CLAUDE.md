# JurisOmegaAI — CLAUDE.md

> Mémoire projet lue automatiquement par Claude Code à chaque session.
> Le « comment, maintenant ». La doctrine complète vit dans le skill maître
> `.claude/skills/jurisomega-ai/SKILL.md` — le lire avant d'agir.

## IDENTITÉ DU PROJET

**JurisOmegaAI** est le **nœud juridique** du réseau de projets du fondateur. Il est le
domicile unique de la compétence juridique, appelée par les deux autres nœuds
(SwissRescue OmniMed, OSINT Oméga AI) plutôt que refaite chez eux.

**Stade : amorçage.** Le dépôt démarre vide. La doctrine est posée avant les livrables,
volontairement.

## RÈGLES INALIÉNABLES (jamais contredites)

1. **Aide à la compréhension du droit, JAMAIS un conseil juridique.** Ce projet n'est ni
   avocat, ni notaire, ni mandataire. Mention visible sur tout livrable sortant.
2. **Zéro fiction juridique.** Aucune référence d'article, d'arrêt, de jurisprudence ou
   de doctrine fabriquée — jamais, y compris « pour illustrer ». En cas de doute :
   marquer « à vérifier », ou omettre.
3. **Toute analyse porte sa juridiction** (CH / UE / autre), écrite en tête.
4. **Toute analyse porte sa date.** Le droit change.
5. **Secret professionnel** — une pièce couverte ne quitte pas le nœud sans mandat écrit
   et daté du fondateur.
6. **Jamais de secret dans le code** — ni clé, ni pièce de dossier, ni identité de partie.
7. **La prudence est le défaut** — entre deux lectures défendables, la plus restrictive,
   et on signale qu'un arbitrage humain est nécessaire.
8. **Chaque commit laisse le projet fonctionnel.**

## ORDRE DE TRAVAIL — 4 COUCHES (ne jamais sauter)

**Loi d'or : pas de couche N+1 tant que la couche N n'est pas verte.**

1. **Doctrine** — skill maître, manifeste de capacités, protocole réseau, ce fichier. *Fait.*
2. **Compétences de priorité 1** — `protection-donnees` (nLPD/RGPD), puis
   `licite-collecte` (sources ouvertes), puis `droit-sante` (statut non diagnostique).
   Une compétence = un `SKILL.md` dédié, avec sources primaires et limites explicites.
3. **Organigramme** — sur le patron `entreprise-omnimed` emprunté au nœud médical : un
   patron qui arbitre, des métiers, et **un agent paramétrable** plutôt que N fiches
   clonées.
4. **Outillage** — seulement une fois la doctrine stable. La justesse d'abord.

## MÉTHODE (résumé — détail au §3 du skill maître)

Qualifier → remonter à la source primaire → distinguer **établi** / **discuté** /
**à vérifier** → éprouver en adversaire → dater, signer la juridiction, poser la limite.

## RÉSEAU OMÉGA

Ce dépôt est un nœud d'un réseau de trois. Protocole :
`.claude/skills/reseau-omega/SKILL.md`. Points à ne jamais oublier :

- **Il n'existe aucun appel direct entre les dépôts.** Le pont N0 est une lecture ; le
  pont N1 passe par des enveloppes écrites (`docs/reseau/appels/`). Ne jamais annoncer
  une capacité sans l'avoir exercée.
- **Une compétence déclarée `planifie` n'est pas appelable.** Le silence vaut refus.
- **Zéro agression** — ce nœud n'écrit jamais dans le dépôt d'un autre.
- Point d'entrée méta : `.claude/skills/meta-competences-juridique/SKILL.md` (route selon les statuts réels).
- Tout franchissement se journalise dans `docs/reseau/JOURNAL_RESEAU.md`.

## ÉTAT DE LA DETTE

Tout est `planifie` sauf la doctrine. Le manifeste
`.claude/skills/reseau-omega/capacites.yaml` fait foi — **le lire avant d'annoncer quoi
que ce soit au fondateur, et le mettre à jour dès qu'une compétence est livrée.** Une
compétence livrée mais non déclarée n'existe pas pour le réseau.
