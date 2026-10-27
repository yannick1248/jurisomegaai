---
name: meta-competences-juris
description: >
  Méta-skill de JurisOmegaAI — point d'entrée qui réveille et enchaîne TOUTES les
  compétences réelles du nœud juridique, et sait appeler celles des deux autres nœuds
  (médical, OSINT) sous bac à sable via Réseau Oméga. À charger au début de toute tâche
  juridique ou multi-domaine. Déclenche sur : « toutes les compétences », « méta »,
  « synthèse », « symbiose », « appelle les autres projets ».
---

# Méta-compétences JurisOmegaAI

Règle de vérité : on n'agrège que du réel. La source de vérité des compétences est
`.claude/skills/reseau-omega/capacites.yaml` — le lire d'abord. Une compétence `planifie`
n'est pas appelable : le dire, ne pas la simuler.

## 1. Carte locale (état au 2026-10-27)
- Implémentés : `jurisomega-ai` (maître, invariants), `reseau-omega` (protocole), ce méta-skill.
- Planifiés (priorité 1 → 3) : `protection-donnees`, `licite-collecte`, `droit-sante`, puis
  `droit-associations`, `propriete-intellectuelle`, `contrats-partenariats`, `force-probante`.
- Ordre de travail : 4 couches de CLAUDE.md, pas de couche N+1 tant que N n'est pas verte.

## 2. Appel sortant (lecture N0 par défaut)
| Besoin | Nœud | Ce qu'on emprunte |
|---|---|---|
| Patron d'organigramme, sourçage unitaire, contre-vérification | swissrescue-omnimed | méthode seulement |
| Modèle entité/trouvaille/chronologie, échelle de confiance | osint-omega-ai | méthode seulement (`modele-confiance`) |
Lire le manifeste du nœud visé, puis son SKILL.md, appliquer chez soi, journaliser.

## 3. Appel entrant (ce que ce nœud sert)
Seules les offres déclarées `implemente` sont servies. Aujourd'hui : aucune offre juridique
n'est mobilisable. Répondre « planifié » plutôt que d'improviser un avis.

## 4. Bac à sable
- Secret professionnel : pièce couverte = N2 uniquement, mandat écrit et daté du fondateur.
- Aucune écriture dans le dépôt d'un autre nœud. Aucune donnée `phi` reçue.
- Tout avis externe est une hypothèse vérifiée chez soi avant intégration.
- Toute sortie : juridiction, date, mention « aide à la compréhension, pas un conseil ».

## 5. Patron réplicable
Un méta-skill par nœud (`meta-competences-omnimed`, `-juris`, `-osint`), tous adossés au même
protocole `reseau-omega` et à un manifeste honnête. Mettre le manifeste à jour dès qu'une
compétence est livrée.
