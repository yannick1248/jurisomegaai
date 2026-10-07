---
name: reseau-omega
description: >
  RÉSEAU OMÉGA — intrication inter-projets des compétences du fondateur. Relie en un seul
  réseau neuronal gouverné les trois nœuds : SwissRescue OmniMed (médical), JurisOmegaAI
  (juridique) et OSINT Oméga AI (renseignement en sources ouvertes). Permet à une session
  ouverte sur UN dépôt de découvrir, puis d'appeler sous bac à sable, les compétences
  (skills + agents + modules) d'un AUTRE dépôt — sans jamais dupliquer une compétence, ni
  laisser fuiter une donnée hors de son nœud d'origine. À charger dès qu'une tâche déborde
  du domaine du dépôt courant : une question juridique dans le médical, un besoin de
  vérification de sources dans le juridique, la licéité d'une collecte dans l'OSINT.
  Déclenche aussi sur : « réseau », « inter-projets », « les autres projets », « appelle
  le juridique », « appelle le médical », « appelle l'OSINT », « compétence externe »,
  « bac à sable », « fédération », « intrication », « mes projets ».
---

# Réseau Oméga — un réseau de neurones entre les projets, avec bac à sable

> Demande fondatrice (dictée) : « il faudrait que toutes les compétences de chacun des
> projets puissent être appelées ou liées comme des réseaux de neurones, mais avec
> évidemment bac à sable dans certains points de vue. »

Ce skill est le **protocole** de cette intrication. Il ne remplace aucun skill maître :
chaque nœud reste souverain chez lui. Il dit **qui peut appeler quoi, à quel niveau
d'isolement, et par quel pont réellement atteignable.**

---

## 0. Loi zéro — ne jamais confondre « connu » et « atteignable »

Reprise directe de `symbiose-surfaces` §0, et elle prime ici.

**Il n'existe AUCUN appel de fonction en direct entre les trois dépôts.** Aucun RPC,
aucun serveur commun, aucune mémoire partagée. Une session Claude Code est ouverte sur
UN dépôt à la fois. Toute affirmation contraire est une hallucination.

Ce qui est réellement atteignable est listé au §4, et rien d'autre. Avant d'annoncer
qu'une compétence externe est mobilisable : **l'exercer une fois et montrer la sortie.**

---

## 1. Les trois nœuds

| Nœud | Dépôt | Domaine | Confiance | Classes de données produites |
|---|---|---|---|---|
| **OmniMed** | `yannick1248/swissrescue-omnimed` | médical, urgence, clinique | `confidentiel` | `phi`, `clinique`, `geo`, `media` |
| **JurisOmega** | `yannick1248/jurisomegaai` | juridique, conformité, gouvernance | `confidentiel` | `secret-pro`, `dossier`, `reference-juridique` |
| **OSINT Oméga** | `yannick1248/osint-omega-ai` | renseignement en sources ouvertes | `restreint` | `source-ouverte`, `donnee-personnelle-collectee` |

Chaque nœud publie son inventaire dans `.claude/skills/reseau-omega/capacites.yaml`.
**Ce fichier est la seule déclaration qui fait foi.** Il n'est jamais rédigé de mémoire :
il est vérifié contre le dépôt (§5).

---

## 2. Les trois niveaux de bac à sable

C'est le cœur du « mais avec évidemment bac à sable ». Un appel inter-nœuds porte
TOUJOURS un niveau explicite. En cas de doute : **le niveau le plus bas.**

### N0 — Référence (la méthode traverse, jamais la donnée)

On emprunte **le savoir-faire** d'un autre nœud : sa méthode, sa grille de lecture, ses
invariants, la structure d'un livrable. Aucune donnée du dossier courant ne sort.

> *Exemple* : le nœud médical lit la méthode de qualification nLPD publiée par
> JurisOmega et l'applique lui-même à son propre cas, chez lui.

**Toujours autorisé, entre tous les nœuds, dans les deux sens.** C'est le niveau par défaut.

### N1 — Requête pseudonymisée (une donnée abstraite traverse)

On envoie une **question** accompagnée d'un extrait **pseudonymisé** : identités,
dates précises, identifiants et localisations fines retirés ou généralisés. Le nœud
appelé répond sans jamais connaître le sujet réel.

Exige : une carte de pseudonymisation conservée **uniquement** dans le nœud appelant,
et la mention `niveau: N1` dans l'enveloppe.

### N2 — Délégation complète (la donnée brute traverse)

Le nœud appelé reçoit la matière réelle. **Interdit par défaut.** N'est ouvert que si
les trois conditions sont réunies :

1. autorisation **explicite, écrite et datée** du fondateur, pour CETTE tâche ;
2. les deux nœuds sont de confiance `confidentiel` ;
3. aucun interdit du §3 n'est franchi.

Une autorisation vaut pour sa tâche, jamais pour la suivante.

---

## 3. Interdits absolus du réseau (jamais franchis, aucun niveau)

1. **Aucune donnée de santé identifiante (`phi`) ne quitte le nœud médical.** Prolonge
   l'invariant de souveraineté suisse du skill maître `swissrescue-omnimed` (corpus 0.3) :
   les données de santé ne transitent pas hors de Suisse/UE, et *a fortiori* pas vers un
   nœud de renseignement. Vers OSINT : **N0 uniquement, sans exception.**
2. **Aucune capacité offensive n'existe ni ne s'appelle.** Le nœud OSINT est en sources
   ouvertes et défensif. Aucun autre nœud ne peut lui demander un scan, une intrusion,
   un contournement, ni le ciblage d'une personne privée.
3. **Un résultat OSINT n'alimente jamais un raisonnement diagnostique.** Il entre dans le
   nœud médical estampillé `non-clinique`, et ne peut apparaître ni dans un rapport
   clinique, ni dans un différentiel, ni dans une alerte médicamenteuse.
4. **Le secret professionnel ne traverse pas.** Une pièce couverte par le secret
   (juridique ou médical) ne sort de son nœud qu'en N2, donc jamais sans mandat écrit.
5. **Non-propagation d'erreur.** Reprise de `liaison-code-projet` §3 : rien de non vérifié
   ne franchit un pont. Une compétence externe donne un **avis**, jamais une vérité ; le
   nœud appelant reste responsable de ce qu'il intègre, et le vérifie chez lui.
6. **Zéro agression.** Un appel inter-nœuds ne modifie JAMAIS le dépôt d'un autre nœud :
   pas de commit, pas de branche, pas de PR croisée. Lecture seule, toujours.
7. **Zéro doublon.** Si une compétence existe déjà dans un autre nœud, on l'appelle — on
   ne la recopie pas. Une compétence a un seul domicile.
8. **Traçabilité.** Tout franchissement se journalise (§4.3). Un pont non journalisé est
   réputé n'avoir pas eu lieu.

### Matrice des niveaux maximaux

| appelant ↓ / appelé → | OmniMed | JurisOmega | OSINT Oméga |
|---|---|---|---|
| **OmniMed** | — | **N1** | **N0** (interdit §3.1) |
| **JurisOmega** | **N1** | — | **N1** |
| **OSINT Oméga** | **N0** | **N1** | — |

N2 n'apparaît nulle part : il ne s'ouvre que ponctuellement, par mandat écrit (§2).

---

## 4. Les ponts réellement atteignables

### 4.1 Pont de lecture (N0) — disponible aujourd'hui

Une session Claude Code dont le périmètre GitHub couvre les trois dépôts peut **lire**
les manifestes et les skills des autres nœuds. C'est le pont normal, et il suffit à
la grande majorité des besoins.

Geste : lire `.claude/skills/reseau-omega/capacites.yaml` du nœud visé, puis le
`SKILL.md` de la compétence retenue, et appliquer la méthode **chez soi**.

> Si le périmètre GitHub de la session ne couvre pas le dépôt visé, l'appel échoue —
> le dire, ne pas inventer la réponse à la place du nœud absent.

### 4.2 Pont d'enveloppes (N1) — asynchrone, par le dépôt

Il n'y a pas de canal direct : le **dépôt est le seul point commun**. Un appel N1
s'écrit donc, et se répond plus tard, dans une autre session.

- L'appelant écrit `docs/reseau/appels/<horodatage>-<noeud-cible>.md`.
- Une session ouverte sur le nœud cible traite l'enveloppe et écrit la réponse dans
  `docs/reseau/reponses/` **de son propre dépôt**, puis le fondateur la rapatrie.
- Aucun nœud n'écrit dans le dépôt d'un autre (interdit §3.6).

Enveloppe minimale :

```yaml
appel: reseau-omega/1
de: swissrescue-omnimed
vers: jurisomegaai
niveau: N1
competence: <id dans capacites.yaml du nœud cible>
question: <une question, une seule>
extrait_pseudonymise: |
  <matière abstraite — aucune identité, aucune date précise, aucun identifiant>
pseudonymisation_conservee_chez: swissrescue-omnimed
autorisation_fondateur: non-requise-en-N1
```

### 4.3 Journal

Tout franchissement, dans les deux sens, s'ajoute (append-only, jamais réécrit — loi de
concaténation de `synergie-omnimed` §2) à `docs/reseau/JOURNAL_RESEAU.md` du nœud
appelant : date, nœud visé, compétence, niveau, ce qui a traversé, ce qui a été intégré
et **après quelle vérification**.

---

## 5. Tenir son manifeste honnête

`capacites.yaml` déclare, pour chaque compétence : son `id`, son `type`
(`skill` | `agent` | `module`), son `statut` (`implemente` | `partiel` | `planifie`),
les classes de données qu'elle touche, et son `export` (`N0` | `N1` | `N2` | `interdit`).

Trois règles, non négociables :

- **`statut` dit la vérité du dépôt, pas l'intention.** Une capacité déclarée dans un
  catalogue mais sans implémentation est `planifie`. Mentir ici contamine tout le réseau.
- **Une compétence non déclarée n'est pas appelable.** Le silence vaut refus.
- **`export: interdit` prime sur la matrice du §3.** Le nœud propriétaire a toujours le
  dernier mot sur ce qui sort de chez lui.

---

## 6. Le geste, en cinq temps

1. **Reconnaître le débordement.** La tâche sort du domaine du dépôt courant.
2. **Chercher chez soi d'abord.** Le nœud courant a-t-il déjà la compétence ? Si oui,
   ne pas traverser (interdit §3.7 en miroir : on ne mendie pas ce qu'on possède).
3. **Lire le manifeste du nœud visé**, retenir une compétence par son `id`.
4. **Choisir le niveau le plus bas qui répond** — presque toujours N0.
5. **Intégrer sous vérification, et journaliser.** L'avis externe est une hypothèse
   jusqu'à ce que le nœud appelant l'ait éprouvée chez lui (interdit §3.5).

---

## 7. Ce que ce skill ne fait pas

- Il n'exécute rien à distance et n'ouvre aucune session sur un autre dépôt.
- Il ne fusionne pas les projets : un seul nom vers l'extérieur par nœud, toujours.
- Il ne remplace pas les skills maîtres (`swissrescue-omnimed`, `jurisomega-ai`,
  `osint-omega-ai`) : il s'y subordonne. En cas de contradiction, **le skill maître du
  nœud courant l'emporte**, et le désaccord se journalise.

---

## 8. Un méta-skill par nœud — le point d'entrée du réseau

Chaque nœud a **un seul** skill d'entrée (le « méta-prompt ») qui recense **toutes** ses
compétences réelles, dit quand les réveiller, et renvoie vers ce protocole dès qu'une tâche
déborde. C'est lui que la session charge en premier ; il ne réécrit rien, il **route**.

| Nœud | Skill d'entrée | Où il vit |
|---|---|---|
| OmniMed | `meta-competences-swissrescue` | `swissrescue-omnimed/.claude/skills/` |
| JurisOmega | `jurisomega-ai` (maître = méta) | `jurisomegaai/.claude/skills/` |
| OSINT Oméga | `osint-omega-ai` (maître = méta) | `osint-omega-ai/.claude/skills/` |

Contrat commun d'un méta-skill :

1. **Carte vérifiée** — il ne liste que ce qui existe dans le dépôt (skill, agent, module) ;
   une doctrine n'est pas un skill, un projet de skill n'est pas un skill.
2. **Miroir du manifeste** — sa carte et `capacites.yaml` disent la même chose ; en cas
   d'écart, le manifeste fait foi et l'écart se corrige le jour même.
3. **Sas réseau** — toute compétence externe passe par §6 (cinq temps) et la matrice §3.
4. **Bac à sable explicite** — il rappelle les interdits propres à son nœud, opposables
   à tout appelant (champ `invariants_opposables` du manifeste).
5. **Patron réplicable** — un nouveau projet du fondateur reçoit : un méta-skill, un
   manifeste, un journal. Rien d'autre n'est requis pour entrer dans le réseau.
