# Architecture JurisOméga — trois étages, une seule configuration licite

> **Juridiction : Suisse (CH).** État arrêté au 26.08.2026 (correction v1.1), intégré au
> dépôt le 31.08.2026. Le droit change : revue trimestrielle (corpus arrêté au 25.08.2026).
>
> **Aide à la compréhension du droit, jamais un conseil juridique.** Pour une décision
> engageante — notamment fiscale ou statutaire — un professionnel mandaté reste nécessaire.

Document de référence de l'architecture de **JurisOméga**, l'outil du nœud juridique
(v1 : délais + rappels et analyse de dossier — outil interne des fondateurs). Il fait foi
côté doctrine ; l'implémentation s'y conforme.

Fondement de la correction v1.1 : la note `claude/AFFECTATION_module_juridique_SwissRescue.md`
du 26.08.2026 (nœud médical), sourcée sur la circulaire AFC n° 12 du 8 juillet 1994 —
franchissement N0 journalisé dans `docs/reseau/JOURNAL_RESEAU.md`. Les affirmations
juridiques du présent document sont portées par cette note ; ce qui n'a pas été relu ici
est marqué comme tel.

---

## §0 — La ligne rouge, à ne jamais franchir

**Aucun dossier privé d'un fondateur, d'un organe ou d'un proche ne touche
l'infrastructure de l'association.**

Fondement — porté par la note d'affectation du 26.08.2026, sourcée sur la circulaire
AFC n° 12 du 8.7.1994, non relue dans ce nœud (**à vérifier**, cf.
`docs/reseau/JOURNAL_RESEAU.md`, entrée du 31.08.2026) : un outil traitant les
dossiers privés d'un fondateur sur l'infrastructure de l'association constitue un
**retour au fondateur en nature** — rupture simultanée de trois conditions de
l'exonération : l'**exclusivité** de l'affectation des moyens au but, le
**désintéressement**, et le **cercle ouvert** des destinataires. Aucune clause ne
rattrape ce cumul. La position stricte retenue ne dépend pas de cette relecture
(invariant n° 7 — la prudence est le défaut).

Entre deux lectures défendables, la plus restrictive est retenue (invariant n° 7 du
skill maître) : la séparation est **matérielle** — deux instances distinctes — et non
seulement contractuelle ou déclarative.

Conséquences opérationnelles :

- l'instance associative (`/juris`) ne reçoit que des dossiers de **bénéficiaires
  accompagnés par l'association** — règle d'usage à protocoler au comité (§4) ;
- les dossiers propres du titulaire vivent sur l'**instance privée**, déployée hors de
  toute infrastructure associative (§1, étage 3) ;
- aucun lien public ne mène à `/juris` (§6).

---

## §1 — Les trois étages

| Étage | Quoi | Où | Données | Statut |
|---|---|---|---|---|
| 1. **Public** | « Droits & Délais » — statique | site associatif | aucune | livré |
| 2. **Associatif** | JurisOméga sous `/juris` | site Node.js existant | dossiers de **bénéficiaires accompagnés** uniquement | à monter (Ouvert n° 2) |
| 3. **Privé** | la même application | **hors** infrastructure associative | dossiers propres du titulaire | à déployer (Ouvert n° 7) |

C'est l'étage public qui porte l'utilité publique. C'est la **seule** configuration où
les trois usages coexistent sans franchir le §0 : rattachement de l'outil à l'activité
de l'association (art. 60 ss CC, en constitution — décision du 26.08.2026), bénéficiaires
sur l'instance associative, titulaire chez lui.

---

## §2 — Montage technique : `/juris` dans le site Node.js existant

- L'offre d'hébergement annonce **un seul site Node.js**. `[NV]` — à confirmer par écrit
  auprès de l'hébergeur (Ouvert n° 1). L'application se monte donc dans le site existant,
  sans second emplacement et sans coût.
- Montage : `deploy/monter-jurisomega.js` + une ligne avant `express.static`, avec
  `JURIS_BASE=/juris`. Les deux modes — racine et monté — ont été vérifiés le 26.08.2026
  sur une réplique fidèle du site en production (voir `ETAT_PROJET.md`, § « Greffe »).
- L'instance montée garde un **magasin et une clé distincts** de ceux du site Node.js
  hôte (décision du 26.08.2026) : aucune donnée ni clé partagée avec le site médical.
- Dégradation sûre, vérifiée par la même simulation : ligne commentée, application
  absente ou variables absentes → le site médical reste intact et `/juris` répond 404,
  rien n'est monté à moitié.
- Installation : `node install.js` — vérifie Node, installe, teste, tire les clés, prend
  les comptes en saisie masquée, écrit `.env.local` et affiche les variables à coller
  dans le Manager.
- Aucune dépendance native côté serveur (écarté : compilation aléatoire sur hébergement
  mutualisé).

---

## §3 — Hébergement (relevé Manager du 26.08.2026)

Hébergement Web mutualisé de `swissrescueomnimed.ch` (échéance 29.04.2027) ; site
Node.js existant en Node 24, port 5000, commande `npm run server:prod`, build
`npm install && npm run server:build` ; 1 utilisateur SSH, aucune base de données.
Relevé complet dans `ETAT_PROJET.md`.

**Sauvegarde : AUCUNE au relevé — à activer avant toute intervention (Ouvert n° 0,
priorité absolue).**

---

## §4 — Périmètres de données et règle d'usage

- **`/juris` (étage associatif)** : dossiers de bénéficiaires accompagnés par
  l'association, **exclusivement**. Règle d'usage à protocoler au comité (Ouvert n° 3).
  Accès authentifié, non indexé.
- **Instance privée (étage 3)** : dossiers propres du titulaire, hors périmètre
  associatif. Magasin et clé **distincts** de l'instance associative.
- **Pseudonymisation à la saisie** ; aucune donnée sensible hors du périmètre
  Suisse / UE / AELE / RU.
- **Chiffrement au repos** : magasin en fichiers `.enc`, mode 0600, illisibles sans la
  clé (vérifié le 26.08.2026). Selon la note du 26.08.2026, ce magasin sert la condition
  de protection de l'art. 143 CP ; pas de base de données externe pour deux utilisateurs.
- **AIPD (art. 22 LPD) et registre (art. 12 LPD)** : à conduire pour l'étage associatif
  (Ouvert n° 5).
- **Secret professionnel** : une pièce couverte ne quitte le nœud qu'avec mandat écrit
  et daté du fondateur (invariant n° 5 du skill maître).

---

## §5 — Couplage du corpus : une seule table de délais

« Droits & Délais » (étage public) doit lire la **même** table de délais que JurisOméga
(`server/lib/catalogue.js`) — source unique du corpus, sinon les deux étages divergent
en silence (Ouvert n° 6). Revue trimestrielle du corpus, arrêté au 25.08.2026
(Ouvert n° 9).

---

## §6 — Déploiement, liens, indexation

- Déploiement par la voie « tirage », identique au site médical : git fetch + gates +
  preuve live + retour arrière. **Aucun secret ne quitte le serveur** — pas de GitHub
  Actions avec secrets de déploiement (écarté).
- Lien depuis le site médical : vers **« Droits & Délais »** uniquement, dès l'adoption
  des clauses statutaires (rattachement + exclusion de retour, Ouvert n° 4) —
  **jamais** vers `/juris`.
- `/juris` reste authentifié et non indexé. Le sondage du site public (26.08.2026) :
  `/juris` libre (404), en-têtes de sécurité stricts côté hôte, `x-robots-tag: noai`.

---

## §7 — Options écartées, et pourquoi

| Option | Raison de l'écarter |
|---|---|
| Second site Node.js sur l'hébergement | l'offre en annonce un seul `[NV]` ; montée en gamme payante, sans moyens |
| Sous-domaine `juris.swissrescueomnimed.ch` dédié | remplacé par le montage sous `/juris` |
| Dossiers privés du titulaire sur l'infrastructure associative | **ligne rouge, §0** |
| Entité juridique distincte pour la v1 | l'hébergement devrait alors être refacturé au prix du marché |
| Application native / magasin d'applications **pour la v1** | la PWA couvre web et mobile avec une seule base de code |
| Dépendance native côté serveur | compilation aléatoire sur hébergement mutualisé |
| Base de données externe | le magasin chiffré suffit pour deux utilisateurs |
| GitHub Actions avec secrets de déploiement | aucun secret ne quitte le serveur |

---

## §8 — Où vit le code

À la date d'intégration (31.08.2026), ce dépôt porte la **doctrine** ; les artefacts
d'implémentation cités ici (`server/lib/catalogue.js`, `deploy/monter-jurisomega.js`,
`install.js`, les 25 tests) vivent dans l'espace de travail où la v1 a été construite
et prouvée le 26.08.2026 — ils ne sont pas versionnés ici. Écart signalé dans
`ETAT_PROJET.md` (§ « Intégration au dépôt ») : rapatrier ou référencer la base de code
v1 dans un dépôt versionné est le point **Ouvert n° 10**, ajouté le 31.08.2026 dans
cette même section. Tant que ce n'est pas fait, ce document
fait foi pour l'architecture, et `ETAT_PROJET.md` pour l'état des preuves.
