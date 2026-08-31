# ÉTAT DU PROJET — JurisOméga

*Fichier de continuité. À lire en premier, à mettre à jour en dernier.*

## Correction v1.1 — alignement sur la note d'affectation (26.08.2026)

La note `claude/AFFECTATION_module_juridique_SwissRescue.md`, produite le même jour et mieux sourcée
(circulaire AFC n° 12 du 8.7.1994), pose une ligne rouge que la première version de l'architecture
n'avait pas tenue : **un outil traitant les dossiers privés d'un fondateur sur l'infrastructure de
l'association est un retour au fondateur en nature** — rupture simultanée de l'exclusivité, du
désintéressement et du cercle ouvert, qu'aucune clause ne rattrape. L'architecture s'aligne sur la
position stricte.

**Trois étages, une seule configuration licite :**

1. **Public** — « Droits & Délais », statique, sans donnée, sur le site associatif. C'est lui qui
   porte l'utilité publique. Déjà livré.
2. **Associatif** — JurisOméga **monté sous `/juris` dans le site Node.js existant**, réservé aux
   dossiers des **bénéficiaires accompagnés par l'association**.
3. **Privé** — la même application, déployée **hors** infrastructure associative, pour les dossiers
   propres du titulaire.

Verrou technique levé : l'offre annonce **un seul site Node.js**. `[NV]` — à confirmer par écrit
auprès de l'hébergeur. L'application se monte donc dans le site existant (`JURIS_BASE=/juris`), sans
second emplacement et sans coût. Les deux modes — racine et monté — sont vérifiés.

Couplage à maintenir : « Droits & Délais » doit lire la **même** table de délais que JurisOméga
(`server/lib/catalogue.js`), sinon les deux étages divergeront en silence.

---

## Relevé serveur — vérifié dans le Manager le 26.08.2026

| Élément | Valeur |
|---|---|
| Hébergement | swissrescueomnimed.ch — Web, mutualisé, échéance 29.04.2027 |
| Sites | **1 / 21** (vingt emplacements libres) · stockage 148 Mo / 250 Go |
| Site Node.js existant | Node **24**, actif ; emplacement `/sites/swissrescueomnimed.ch` |
| Commande d'exécution | `npm run server:prod` · build `npm install && npm run server:build` |
| Port d'écoute | **5000** |
| Domaines du site | principal, `www`, hôte de prévisualisation (un 4ᵉ peut être ajouté) |
| SSH | 1 utilisateur, console disponible depuis le Manager |
| Bases de données | aucune |
| **Sauvegarde** | **AUCUNE** — à activer avant toute intervention |

Non vérifié : le nombre de sites **Node.js** autorisés. Sans objet pour l'architecture retenue,
puisque JurisOméga se monte dans le site existant.

## Décisions arrêtées (26.08.2026)

- Rattachement : **activité de l'association SwissRescue OmniMed** (art. 60 ss CC, en constitution).
- v1 : **outil interne** (fondateurs Yannick et Zeliha). L'ouverture publique est une v2, décidée séparément.
- Noyau v1 : **délais + rappels ET analyse de dossier** (pièces, bordereau, chronologie), livrés ensemble.
- Hébergement : **même hébergement Web Infomaniak** que `swissrescueomnimed.ch`, **monté sous
  `/juris` dans le site Node.js existant** (pas de second emplacement Node.js), magasin et clé distincts.
- Forme : **PWA** installable — une base de code pour le web et le mobile. Pas de magasin d'applications.
- Déploiement : **voie « tirage »**, identique au site médical (git fetch + gates + preuve live + retour arrière).
- Lien depuis le site médical : vers **« Droits & Délais »** (dès l'adoption des clauses statutaires) ;
  **jamais** vers `/juris`, qui reste authentifié et non indexé.

## Écarté

- Second site Node.js sur l'hébergement (l'offre en annonce un seul ; montée en gamme payante, sans moyens).
- Sous-domaine `juris.swissrescueomnimed.ch` en site Node.js dédié — remplacé par le montage sous `/juris`.
- Traitement des dossiers privés du titulaire sur l'infrastructure associative (ligne rouge).
- Entité juridique distincte pour la v1 (l'hébergement devrait alors être refacturé au prix du marché).
- Application native / magasin d'applications pour la v1.
- Toute dépendance native côté serveur (compilation aléatoire sur hébergement mutualisé).
- Base de données externe : le magasin chiffré suffit pour deux utilisateurs et sert la condition CP 143.
- GitHub Actions avec secrets de déploiement : aucun secret ne quitte le serveur.

## Ligne rouge, à ne jamais franchir

Aucun dossier privé d'un fondateur, d'un organe ou d'un proche ne touche l'infrastructure de
l'association. L'instance `/juris` ne reçoit que des dossiers de **bénéficiaires accompagnés par
l'association** — règle d'usage à protocoler au comité. Les dossiers propres du titulaire vivent sur
l'instance privée, hors périmètre associatif. Voir `docs/ARCHITECTURE.md` §0 et §4.

## Greffe — prouvée le 26.08.2026

`deploy/monter-jurisomega.js` + une ligne avant `express.static`. Vérifié sur une réplique fidèle
du site en production (express.static à la racine, mêmes en-têtes de sécurité, port 5000) :

| Scénario | Site médical | `/juris` |
|---|---|---|
| Nominal | intact | auth, 45 délais, calcul LP correct, dossier + pièce + bordereau, données chiffrées |
| Ligne commentée | intact | 404 |
| JurisOméga absent | intact | 404 + message clair |
| Variables absentes | intact | 404 + message clair, rien monté à moitié |

Deux défauts trouvés et corrigés par cette simulation : `module.exports = app` écrasait
`module.exports.routeur` (le montage recevait `undefined`), et les parseurs de corps étaient
posés sur l'app au lieu du routeur (les requêtes POST arrivaient sans corps en mode greffé).
Une écoute de port parasite en mode greffé a aussi été supprimée.

`node install.js` : une commande qui vérifie Node, installe, teste, tire les clés, prend les
comptes en saisie masquée, écrit `.env.local` et affiche les variables à coller dans le Manager.

## État technique

- 25 tests de régression du moteur de délais : **verts**. `npm test`.
- Parcours de bout en bout vérifié : connexion → dossier → délai rattaché → pièce → bordereau → `.ics`.
- Chiffrement au repos vérifié (fichiers `.enc`, mode 0600, illisibles sans la clé).
- Accès non authentifié aux API : **401**.
- Rendu vérifié en 1440 px et en 390 px (tableaux transformés en fiches sous 700 px).
- Site public sondé : `/juris` libre (404), service statique confirmé (etag + last-modified),
  en-têtes de sécurité déjà stricts côté hôte, `x-robots-tag: noai` en place.

## Ouvert

0. **Activer une sauvegarde de l'hébergement** — le Manager indique « aucune sauvegarde ». Priorité absolue, avant toute modification.
1. Faire préciser par écrit le nombre de sites Node.js inclus (utile, plus bloquant).
2. Monter JurisOméga sous `/juris` (`JURIS_BASE=/juris`) et déposer les trois variables d'environnement.
3. Protocoler au comité la règle d'usage : `/juris` ne reçoit que des dossiers de bénéficiaires.
4. Adopter les deux clauses statutaires (rattachement + exclusion de retour) en AG.
5. Conduire l'AIPD (art. 22 LPD) et ouvrir l'entrée au registre pour l'étage associatif (art. 12 LPD).
6. Faire lire à « Droits & Délais » la table `server/lib/catalogue.js` — source unique du corpus.
7. Déployer l'instance privée hors infrastructure associative.
8. Lier « Droits & Délais » depuis le site médical ; jamais `/juris`.
9. Revue trimestrielle du corpus (arrêté au 25.08.2026).

## Contraintes à respecter

- Charte graphique v1.0 : marine `#1B2440`, bleu `#2F3C7E`, rouge `#990011`. Registre institutionnel, jamais ludique.
- Marque blanche : ne pas citer les technologies ni les fournisseurs dans les supports publics.
- Pseudonymisation à la saisie ; aucune donnée sensible hors du périmètre Suisse / UE / AELE / RU.
- Non-régression : ne jamais perdre ni contredire un résultat acquis — signaler l'écart.

---

## Intégration au dépôt — relevé du 31.08.2026

*Section ajoutée lors de l'intégration de ce fichier dans le dépôt `jurisomegaai`
(branche `claude/jurisomega-v1-alignment-5m7t55`). Rien au-dessus de cette ligne n'a été
modifié — loi de concaténation.*

**Ce que le dépôt contient à ce jour** : la doctrine seule (skill maître, protocole
réseau, manifeste de capacités, journal). Les livrables décrits plus haut —
`server/lib/catalogue.js`, `deploy/monter-jurisomega.js`, `install.js`, les 25 tests —
ne sont **pas** versionnés dans ce dépôt : ils vivent dans l'espace de travail où la v1
a été construite et prouvée le 26.08.2026. Écart signalé (règle de non-régression) :
les résultats relevés plus haut restent acquis tels que datés, mais ce dépôt ne peut
pas les rejouer. **Une preuve non versionnée ne survit pas à la machine qui la porte. Ouvert n° 10
(ajouté le 31.08.2026) : rapatrier ou référencer la base de code v1 (`server/`,
`deploy/monter-jurisomega.js`, `install.js`, les 25 tests) dans un dépôt versionné.**

**Aligné dans ce dépôt le 31.08.2026 :**

- `docs/ARCHITECTURE.md` — établi ici, d'après la présente note, pour porter le §0
  (ligne rouge) et le §4 (périmètres et règle d'usage) cités plus haut. Il fait foi
  côté doctrine ; l'implémentation s'y conforme. Si une version antérieure existe à
  côté du code v1, la fusionner à la prochaine synchronisation.
- `docs/reseau/JOURNAL_RESEAU.md` — le franchissement N0 vers le nœud médical
  (lecture de la note d'affectation du 26.08.2026) est journalisé, comme l'exige
  l'interdit réseau §3.8 : un pont non journalisé est réputé n'avoir pas eu lieu.
- `CLAUDE.md` et `README.md` — pointeurs vers ce fichier et vers la ligne rouge.
- **Rectification** : « art. 60 ss CO » → « art. 60 ss CC » dans `README.md`, le
  skill maître et le manifeste de capacités. Le droit suisse des associations relève
  du Code civil (art. 60 ss CC), comme le cite correctement la présente note ; la
  citation « CO » du commit d'amorçage était erronée.

**Statuts non modifiés, à dessein** : dans `capacites.yaml`, toutes les compétences
réseau restent `planifie` (le `statut` dit la vérité du dépôt, pas l'intention,
protocole §5) ; la seule retouche du fichier est la rectification « CO » → « CC »
signalée ci-dessus. L'outil JurisOméga v1 n'est pas une compétence appelable par le
réseau et n'y est donc pas déclaré.
