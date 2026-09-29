---
name: meta-prompt
description: >
  MÉTA-PROMPT du nœud jurisomegaai (juridique). Point d'entrée unique qui charge TOUTES les compétences
  du projet à partir du manifeste vérifié, route chaque tâche vers la compétence locale
  compétente, et — si la tâche déborde — vers un autre nœud du Réseau Oméga sous bac à
  sable (N0/N1/N2). À charger en début de session ou dès qu'une tâche touche plusieurs
  domaines. Compétences visées : protection des données, licéité de collecte, droit de la santé, associations, PI, contrats, force probante (voir manifeste pour leur statut réel). Déclenche aussi sur : « toutes les compétences », « méta-prompt »,
  « inventaire », « que sait faire ce projet », « appelle un autre projet », « réseau ».
---

# Méta-prompt — nœud jurisomegaai

Ce skill ne contient **aucune compétence** : il les *découvre*, les *route* et les
*borne*. Une compétence a un seul domicile (réseau §3.7).

## 1. Charger (toujours dans cet ordre)

1. `CLAUDE.md` du dépôt — règles inaliénables, elles priment sur tout.
2. `.claude/skills/reseau-omega/capacites.yaml` — **seule déclaration qui fait foi**.
   N'est appelable que ce qui est `implemente` ou `partiel`. `planifie` = non appelable ;
   le silence vaut refus.
3. Les `SKILL.md` des compétences retenues pour la tâche — pas plus (lecture à la demande).
4. `.claude/skills/reseau-omega/SKILL.md` seulement si la tâche déborde du nœud.

## 2. Router

Pour chaque tâche : (a) nommer le domaine ; (b) chercher la compétence locale dans le
manifeste ; (c) si elle existe et est appelable, l'appliquer ; (d) sinon, débordement → §3 ;
(e) si aucun nœud ne la déclare, le dire au fondateur — ne jamais improviser une
compétence absente.

## 3. Déborder vers un autre nœud (bac à sable)

Niveau **le plus bas** qui répond, et jamais au-delà de la matrice réseau §3 :

| Niveau | Ce qui traverse | Usage |
|---|---|---|
| **N0** | la méthode, jamais la donnée (lecture du manifeste et du SKILL.md de l'autre nœud, application chez soi) | défaut |
| **N1** | une question + extrait pseudonymisé, par enveloppe dans `docs/reseau/appels/` | ponctuel |
| **N2** | donnée brute | interdit sauf mandat écrit et daté du fondateur, pour cette tâche |

Lecture seule chez l'autre (zéro agression). Tout franchissement est consigné dans
`docs/reseau/JOURNAL_RESEAU.md`. Un avis externe est une hypothèse jusqu'à vérification locale.

## 4. Tenir l'inventaire honnête

Dès qu'une compétence est livrée : mettre à jour `capacites.yaml` **dans le même commit**.
Une compétence livrée mais non déclarée n'existe pas pour le réseau ; une compétence
déclarée mais absente contamine le réseau. Vérifier par lecture directe du fichier
(`ls`, `grep`), pas de mémoire.

## 5. Limites

Aucun appel direct entre dépôts ; ce skill n'exécute rien à distance. Il ne remplace pas
les règles de `CLAUDE.md`, qui l'emportent en cas de contradiction.
