# lifespace-generator

Méthode pour créer l'espace personnel d'une personne. Elle transforme son Drive (Google Drive ou autre) en espace rangé et suivi : les documents de chaque domaine de sa vie, et un contexte personnel lisible par le propriétaire et chargé par les agents LLM (Cowork, Claude Code, claude.ai). Elle s'applique à toute personne : tout ce qui lui est propre est déclaré dans `PARAMETRES.md`, à remplir avant toute exécution.

## Principe

- Un fichier `CLAUDE.md` à la racine, lu automatiquement par l'agent. Il fixe l'ordre de lecture, les règles anti-invention, la protection des données sensibles, la gestion des tâches et des échéances, et le protocole de mise à jour.
- Un dossier par domaine de vie (Administratif, Santé, Véhicules...). Chaque domaine contient :
  - des dossiers de sujet, durables : un contrat, un organisme, un bien, un employeur (`ASSUREUR (Assurance auto)`, `2019 - VOITURE`) ;
  - des dossiers d'événement, datés : un sinistre, un épisode de santé, un voyage, une démarche (`20220905 - Dégât des eaux salle de bain`) ;
  - des dossiers de classement facultatifs, dédiés à un type de document figé (`Factures`, `Impôts`) ;
  - des dossiers de regroupement facultatifs, en écriture normale, qui réunissent des sujets de même nature (`Assurances`) et ont leur propre `_ARCHIVES/`, créé de la même façon ;
  - trois dossiers protégés : `_INSTRUCTIONS/` (les fiches du domaine), `_REFERENCES/` (documents figés sans dossier dédié, notes brutes, comptes rendus d'interview) et `_ARCHIVES/` (sujets et événements clos, créé au premier archivage).
- Un dossier `_INSTRUCTIONS/` à la racine pour les fichiers transverses : index, guide, mémoire, leçons, points de vigilance, tâches, échéancier, registre des contrats, contacts.
- Une seule entrée pour les documents bruts : `_INBOX/` à la racine.

Les dossiers `_INSTRUCTIONS/` et `_REFERENCES/` ne sont jamais modifiés à la main : le propriétaire demande à l'agent, qui modifie et journalise. Le propriétaire peut en revanche déplacer lui-même un sujet ou un événement clos dans le `_ARCHIVES/` du dossier qui le contenait (en le créant s'il n'existe pas), puis le signaler à l'agent. Le préfixe `_` place ces dossiers en tête et les distingue des dossiers de sujet.

## Préparation (par le propriétaire)

1. Remplir `PARAMETRES.md`.
2. Créer le dossier racine `{{DOSSIER_RACINE}}` sur le Drive.
3. Y placer le dossier de la méthode, nommé `_LIFESPACE-GENERATOR/`.
4. Créer le dossier `{{DOSSIER_RACINE}}/_INBOX/` et y déplacer tout le contenu existant à reprendre : dossiers et fichiers actuels du Drive, avec leur arborescence.
5. Garder ailleurs une copie de sauvegarde, ou au moins vérifier que la corbeille du Drive est active : la reprise déplace des fichiers.
6. Relier `{{DOSSIER_RACINE}}` à la session Cowork ou Claude Code et lancer : « Lis _LIFESPACE-GENERATOR/METHODE.md puis génère l'espace ».

## Générer l'espace (par l'agent)

La génération se fait en plusieurs sessions : structure et reprise d'abord (étapes 1 à 8), puis alimentation des fiches domaine par domaine (étape 9). Chaque étape restante est suivie dans `05-todo.md`, pour reprendre dans une nouvelle session sans rien perdre.

1. Vérifier que `PARAMETRES.md` est entièrement rempli (aucun [À COMPLÉTER]) : propriétaire, dossier racine, présentation, domaines et périmètres, sources. Les dossiers de classement et les préférences sont facultatifs. Sinon, s'arrêter et demander les valeurs manquantes.
2. Faire valider la liste des domaines par le propriétaire. Étape bloquante : elle conditionne toute l'arborescence.
3. Vérifier que l'agent travaille bien dans `{{DOSSIER_RACINE}}`, puis y copier `templates/CLAUDE.md`, `templates/_INSTRUCTIONS/` (avec `modeles/`, et un dossier `archives/` vide) et `templates/_INBOX/00-depot.md`.
4. Remplacer les variables `{{...}}` par les valeurs des paramètres. `{{DATE}}` est la date de génération. Les variables de domaine (`{{Domaine}}`, `{{domaine}}` en minuscules sans accents ni espaces, `{{BLOC}}`, `{{X0}}`, `{{Périmètre}}`) se déclinent en une ligne ou un fichier par domaine, d'après la table `{{DOMAINES}}` : le premier domaine reçoit le bloc 10, le suivant 20, etc., puis 100, 110... au-delà du neuvième. `{{Dossiers}}` est renseigné plus tard, à l'étape 7. `{{BLOC_LIBRE}}` est le bloc qui suit celui du dernier domaine. Dans les protocoles, `<Domaine>` désigne n'importe quel domaine : ce n'est pas une variable, il reste tel quel. Vérifier qu'il ne reste aucune variable `{{...}}` hors `{{Dossiers}}`.
5. Créer, pour chaque domaine, son dossier, ses sous-dossiers `_INSTRUCTIONS/` et `_REFERENCES/`, les dossiers de classement déclarés dans les paramètres, et sa fiche de synthèse X0 au statut `vide`, à partir de `_INSTRUCTIONS/modeles/fiche-synthese.md` (remplacer les repères `[...]`). Ne pas créer `_ARCHIVES/` : il est créé au premier archivage, dans le domaine ou dans le dossier de regroupement concerné.
6. Reprendre le contenu de `_INBOX/` (sauf `00-depot.md`) en mode reprise : un Drive personnel est en général déjà rangé, et son volume rend le tri fichier par fichier impraticable.
   - **Inventaire** : lister l'arborescence (noms, tailles, dates) sans ouvrir les fichiers. Les fichiers disponibles seulement en ligne ne sont pas téléchargés à cette étape.
   - **Tableau de correspondance au niveau des dossiers** : pour chaque dossier d'origine, proposer le domaine, l'emplacement cible (sujet, événement, classement, `_ARCHIVES/` ou `_REFERENCES/`), le nom cible du dossier, l'action (déplacer tel quel, renommer le dossier, éclater), une justification et un niveau de certitude. Un dossier qui reste cohérent est déplacé en bloc, avec son contenu et ses sous-dossiers.
   - **Dossiers rangés par type à éclater** : un dossier qui regroupe des documents de plusieurs domaines d'après leur type (exemple : `Contrats`, `Factures`, `Divers`) est éclaté. Chaque contrat rejoint le domaine de son objet, sous forme de sujet `Organisme (Objet)` (l'assurance auto va dans Véhicules, l'assurance habitation dans Logement) ; les contrats résiliés vont dans le `_ARCHIVES/` du dossier qui les contenait (domaine ou dossier de regroupement). Une facture d'achat va dans le domaine qui suit les achats et garanties, sauf si elle se rattache clairement à un sujet (une facture vétérinaire va chez l'animal).
   - **Dossiers clos** : un sujet ou un événement clos va dans le `_ARCHIVES/` du dossier qui le contenait : celui du domaine, ou celui d'un dossier de regroupement (exemple : `<Domaine>/Assurances/_ARCHIVES/`). Ce `_ARCHIVES/` est créé à ce moment-là s'il n'existe pas.
   - **Exceptions au niveau des fichiers** : seuls les fichiers en vrac à la racine d'un dossier, ceux dont le contenu ne correspond pas à leur dossier et les cas douteux sont détaillés fichier par fichier, avec les mêmes colonnes.
   - **Noms** : les fichiers gardent leur nom. Les dossiers de sujet et d'événement sont renommés seulement pour suivre les conventions (`Organisme (Objet)`, `AAAA - Nom`, `AAAAMMJJ - Titre`). Le nombre de documents figés dont le nom n'est pas conforme est indiqué, avec une proposition de renommage en lot facultative, faite plus tard et seulement à la demande du propriétaire.
   - **Données sensibles** : signaler les fichiers qui contiennent manifestement des identifiants ou mots de passe (d'après leur nom), et proposer au propriétaire de les sortir du Drive vers un gestionnaire de mots de passe.
   - Présenter le tout, en tête : nombre de dossiers et de fichiers, nombre de dossiers éclatés, nombre d'exceptions. Poser une question pour chaque cas douteux, et ne rien déplacer avant la validation du tableau par le propriétaire.
   - Après validation, créer les dossiers retenus, puis déplacer exactement comme dans le tableau validé, sans toucher au contenu des fichiers.
   - Un dossier ou fichier sans domaine correspondant reste dans `_INBOX/`, avec une proposition de nouveau domaine. Les dossiers d'origine vidés sont signalés, jamais supprimés sans accord.
7. Déclarer chaque domaine, sujet, événement en cours et dossier de classement dans `00-index.md`.
8. Enregistrer le tableau de correspondance validé dans `_INSTRUCTIONS/archives/reprise-initiale-AAAAMMJJ.md`, puis journaliser la création et la reprise dans `02-memoire.md` en citant ce fichier. Créer dans `05-todo.md` une tâche d'alimentation par domaine.
9. Alimenter les fiches, domaine par domaine (une session par domaine si le volume l'exige), par ordre de priorité :
   - **Priorité 1, l'actif** : contrats en cours, sujets actifs, documents des 24 derniers mois. Lus en entier.
   - **Priorité 2, les événements récents et les documents de référence** (identité, titres de propriété, diplômes, carte grise...). Lus en entier ou survolés selon leur utilité.
   - **Priorité 3, les archives** : indexées d'après leurs noms et dossiers, sans être ouvertes. La fiche l'indique (« archives non lues, inventoriées d'après les noms »).
   - Les sources structurées hors du Drive déclarées dans les paramètres (bases Notion, tableurs de suivi) sont lues avec les connecteurs et reprises dans les fiches et les registres, en les citant comme source. Elles complètent souvent le Drive (contrats, achats, voyages qui n'y ont pas de document).
   - Un fichier illisible en local (fichier Google natif `.gdoc`, `.gsheet`, fichier seulement en ligne, fichier protégé) est lu par le connecteur Google Drive s'il est disponible ; sinon, il est décrit d'après son nom avec une certitude faible.
   - Pour chaque domaine : synthèse et fiches de détail en `brouillon` (une fiche de détail par sujet important), règle de non-perte, sources citées par leur nouveau chemin. Chaque contrat en cours entre dans `07-contrats.md`, chaque date à venir dans `06-echeancier.md`, chaque interlocuteur utile dans `08-contacts.md`. Déclarer les fiches dans `00-index.md`, reporter les contradictions dans `04-points-de-vigilance.md` et les actions dans `05-todo.md`, journaliser dans `02-memoire.md`.
10. Faire relire les fiches par le propriétaire, qui les passe en `valide`. Proposer une interview par domaine pour combler les trous.
11. Une fois la génération validée, proposer de sortir `_LIFESPACE-GENERATOR/` de l'espace : ses modèles et son `CLAUDE.md` ne doivent pas être confondus avec le vrai contexte. Pour chaque source structurée reprise (base Notion, tableur), faire décider au propriétaire si elle devient une archive consultable, sans nouvelle mise à jour, ou si elle reste tenue à jour ; dans ce second cas, noter dans `03-lecons.md` laquelle fait foi, sujet par sujet. Deux listes tenues en parallèle finissent par diverger.
12. Proposer une tâche planifiée mensuelle « Fais le point » (voir `CLAUDE.md`), et rappeler comment utiliser l'espace dans d'autres projets : relier `{{DOSSIER_RACINE}}` comme dossier de travail. Si `CLAUDE.md` n'est pas lu spontanément, ajouter dans les instructions du projet : « Lis CLAUDE.md à la racine du dossier de travail et applique-le ». Ne jamais copier son contenu dans les instructions du projet.

## Après la génération

`PARAMETRES.md` ne fait pas partie de l'espace généré : ses valeurs sont recopiées dans les fichiers générés, qui deviennent la seule référence.

| Paramètre | Fichier généré qui le porte |
|---|---|
| `{{PROPRIETAIRE}}` | tous les fichiers |
| `{{DOSSIER_RACINE}}` | le nom du dossier racine, `_INSTRUCTIONS/01-guide.md` |
| `{{PRESENTATION}}` | `CLAUDE.md` |
| `{{SOURCES}}` | `CLAUDE.md`, `_INSTRUCTIONS/01-guide.md` |
| `{{PREFERENCES}}` | `_INSTRUCTIONS/03-lecons.md` |
| `{{DOMAINES}}` (périmètres) | `_INSTRUCTIONS/00-index.md` et les dossiers de domaine |
| Dossiers de classement | `_INSTRUCTIONS/00-index.md` et les dossiers de domaine |

Un oubli ou un changement après la génération se corrige directement dans le fichier généré concerné, en suivant le protocole de mise à jour de `CLAUDE.md` (journalisé dans `02-memoire.md`). Ajouter un domaine après coup se fait avec l'accord du propriétaire : il prend le prochain bloc libre (mis à jour dans `00-index.md`) et suit les étapes 5, 7 et 9 pour ce seul domaine. Seul le nom du dossier racine est coûteux à changer, car il est mémorisé dans les projets qui le montent.

## Arborescence générée

```
{{DOSSIER_RACINE}}/
  CLAUDE.md
  _INSTRUCTIONS/
    00-index.md
    01-guide.md
    02-memoire.md
    03-lecons.md
    04-points-de-vigilance.md
    05-todo.md
    06-echeancier.md
    07-contrats.md
    08-contacts.md
    modeles/            fiche-synthese.md, fiche-detail.md
    archives/           tâches et échéances closes, tableau de reprise initiale
  _INBOX/
    00-depot.md
  {{Domaine}}/
    _INSTRUCTIONS/      X0-{{domaine}}.md (synthèse), X1 à X9 (détail)
    _REFERENCES/        AAAAMMJJ[_TYPE][_ID][_DESCRIPTION][_ORGANISME].ext
    _ARCHIVES/          créé au besoin : sujets et événements clos
    Organisme (Objet)/  sujet durable (exemple : ASSUREUR (Assurance auto))
    AAAA - Nom/         sujet daté par son début (exemple : 2019 - VOITURE)
    AAAAMMJJ - Titre/   événement (exemple : 20240712 - LISBONNE)
    Factures/           dossier de classement facultatif
    Assurances/         dossier de regroupement facultatif (sujets de même nature)
      Assureur (Auto)/  sujet regroupé
      _ARCHIVES/        créé au besoin : sujets clos du regroupement
```

## Les piliers

### 1. CLAUDE.md : le contrat de travail

Lu en premier, automatiquement. Il réunit les consignes de lecture du contexte et les règles de travail au quotidien. Modèle : `templates/CLAUDE.md`.

### 2. L'index : la carte

`_INSTRUCTIONS/00-index.md` liste les domaines, leur bloc, leurs sujets et événements en cours, leurs dossiers de classement et chaque fiche avec son statut. Règle absolue : l'index reflète toujours l'état réel du dossier. Une fiche absente de l'index n'existe pas pour les agents. Les sujets et événements archivés n'y figurent pas un par un : les dossiers `_ARCHIVES/` suffisent.

### 3. Les domaines, les blocs et la règle de non-perte

- Une seule suite de blocs de dizaines, attribués dans l'ordre et sans limite : 10, 20... 90, puis 100, 110... Le bloc 00-09 est réservé aux fichiers transverses. Un bloc attribué ne change jamais et n'est jamais réutilisé, même si son domaine disparaît.
- Un domaine = un bloc. Dans chaque bloc : X0 = fiche de synthèse (1 à 3 pages, chargée par défaut), X1 à X9 = fiches de détail, en général une par sujet important (le véhicule actuel, le logement, le contrat de travail, l'animal).
- Chaque fiche de détail commence par une section « L'essentiel » (10 lignes max) : c'est la seule partie que la synthèse a le droit de reformuler.
- Règle de non-perte : on ne supprime jamais une information en synthétisant. On la déplace en fiche de détail et on laisse un pointeur explicite. Chaîne complète : synthèse, puis détail, puis document source cité par la fiche. Un sujet archivé garde sa fiche de détail, marquée « clos » dans « L'essentiel ».
- Un nouveau domaine reçoit le prochain bloc libre de la suite.
- Si un domaine dépasse 9 fiches de détail, il reçoit lui aussi le prochain bloc libre, déclaré dans l'index comme extension (« Santé (suite) »). Ce bloc ne contient que des fiches de détail, de X0 à X9 ; la synthèse reste la X0 du bloc principal et pointe vers elles.

### 4. La mémoire en fichiers plats

- `02-memoire.md` : journal daté de tout changement du contexte (action, source, auteur), les plus récents en haut. Il garde aussi la date de la dernière revue (« Fais le point ») et de la dernière relève des connecteurs.
- `03-lecons.md` : les préférences du propriétaire et les règles apprises en cours de route, chacune avec son pourquoi et sa provenance `(date, auteur)`.
- `04-points-de-vigilance.md` : les contradictions ouvertes entre sources, non tranchées.
- `05-todo.md` : les tâches, avec identifiant et statut. Une tâche correspond à un travail qui prend du temps ; une petite demande devient une note datée d'une tâche existante, ou rien. Les tâches clôturées depuis plus de 30 jours partent dans `archives/`.

### 5. Le suivi dans le temps : échéancier, contrats, contacts

- `06-echeancier.md` : toutes les dates à venir (fin d'engagement et préavis de résiliation, renouvellement de papiers d'identité, contrôle technique, vaccins, impôts, fin de garantie, rendez-vous). Chaque échéance a un identifiant `E-001`, une date, un rappel (combien de jours avant) et, si elle revient, sa périodicité. Une échéance passée est close, et la suivante créée si elle est récurrente.
- `07-contrats.md` : le registre de tous les contrats et abonnements en cours (identifiant `C-001`, organisme, objet, domaine, référence partielle, début, échéance, préavis, coût, dossier). Les contrats résiliés passent dans la section « Résiliés » avec leur date de fin.
- `08-contacts.md` : les interlocuteurs utiles (médecins, vétérinaire, conseiller, syndic, assureurs, garagiste), avec le domaine et le canal de contact professionnel. Pas de contacts privés de proches.

Ces trois fichiers donnent la vue transverse ; le détail reste dans les fiches et les dossiers des domaines.

### 6. Les données sensibles

L'espace contient des données de santé, d'identité, bancaires et fiscales. Règles incluses dans `CLAUDE.md` :

- Aucun mot de passe, code, identifiant de connexion, IBAN ou numéro de carte complet, numéro de sécurité sociale ou de pièce d'identité complet n'est recopié dans une fiche : la fiche pointe vers le document. Une référence de contrat est notée partiellement si elle suffit à identifier le contrat.
- Les informations de santé sont factuelles et sobres : pas d'interprétation médicale.
- Rien n'est envoyé, partagé ni publié sans validation explicite.
- Ne pas relier l'espace à un projet partagé avec d'autres personnes.

### 7. L'alimentation : 6 canaux, une inbox

1. `_INBOX/` : on y dépose tout document brut, puis on demande « Traite l'inbox ».
2. Sur place : on range soi-même un document, puis on demande « Traite ce fichier ». Un fichier rangé à la main sans être traité n'alimente pas le contexte : c'est un choix.
3. Connecteurs : l'agent va chercher lui-même (messagerie, agenda, Drive...).
4. Relève : « Relève les connecteurs », l'agent cherche dans les sources déclarées les documents arrivés depuis la dernière relève (factures, confirmations, avis, attestations) et les fait entrer par `_INBOX/`.
5. Interview guidée : « Interview Santé », l'agent pose ses questions sur un domaine, enregistre un compte rendu dans `_REFERENCES/` et rédige ses fiches.
6. Chat direct : coller du texte ou joindre des fichiers.

### 8. La revue : « Fais le point »

Une revue périodique (mensuelle par défaut, idéalement en tâche planifiée) : échéances des 60 prochains jours, contrats arrivant à échéance ou à renégocier, tâches en retard, inbox en attente, fiches en `brouillon` anciennes, points de vigilance ouverts. Protocole dans `CLAUDE.md`.

## Cycle de vie d'une information

Entrée (inbox, fichier traité sur place, connecteur, relève, interview, chat), puis intégration dans une fiche en `brouillon` et, si besoin, dans l'échéancier, le registre des contrats ou les contacts, puis relecture par le propriétaire qui la passe en `valide`. Toute évolution met à jour le champ `maj` et ajoute une ligne à `02-memoire.md`. Un sujet ou un événement clos part dans le `_ARCHIVES/` du dossier qui le contenait (domaine ou dossier de regroupement), créé au premier archivage.

## Conventions

- Fichiers de contexte : `.md`, minuscules, en français, sans accents ni espaces, tirets simples. Seule exception : `CLAUDE.md`.
- Dossiers de domaine et de classement : noms lisibles, avec majuscule initiale et accents (`Études et formation`).
- Dossiers de sujet : `Organisme (Objet)` pour un contrat ou un organisme (`ASSUREUR (Assurance habitation)`), `AAAA - Nom` pour un sujet daté par son début (`2016 - EMPLOYEUR`, `2019 - VOITURE`), ou un nom simple (`Chien`).
- Dossiers d'événement : `AAAAMMJJ - Titre`, la date étant celle du début de l'événement (`20190528 - Entorse cheville gauche`).
- Documents : seuls les documents figés (facture, contrat signé, avis, attestation...) sont renommés, au format `AAAAMMJJ[_TYPE][_ID][_DESCRIPTION][_ORGANISME].ext`. Les notes brutes (type `NOTE` ou `INTERVIEW`) suivent le même format et vont dans `_REFERENCES/`. Les documents de travail (tableurs, brouillons, photos) gardent leur nom. Règles complètes : `templates/_INSTRUCTIONS/01-guide.md`.
- Dates : `AAAA-MM-JJ` dans les textes (ou `AAAA-MM` pour un mois), `AAAAMMJJ` dans les noms de fichiers et de dossiers.
- Frontmatter : voir `templates/_INSTRUCTIONS/01-guide.md`.

## Préférences par défaut

Elles sont incluses dans le modèle `CLAUDE.md` : inutile de les redéclarer.

- Jamais de tiret cadratin, ni dans les réponses, ni dans les livrables, ni dans les fichiers.
- Travail en français par défaut.
- Aucun fait inventé : une information absente est « non documentée ».
- Toute action engageante (suppression, envoi, paiement, résiliation, démarche administrative, santé, juridique) est validée explicitement par le propriétaire.
- Aucune donnée sensible recopiée dans les fiches (voir « Les données sensibles »).

Les préférences propres au propriétaire s'ajoutent dans `PARAMETRES.md`.

## Bonnes pratiques et pièges connus

- Un email cité (objet, expéditeur, date) suffit comme source : ne l'exporter en PDF que s'il peut servir de preuve (engagement, réclamation, litige).
- Quand une fiche `valide` est modifiée, la faire valider dans la session en listant les passages changés : rouvrir chaque fiche pour retrouver les changements est trop lourd.
- Une information vit à un seul endroit ; les autres fiches pointent vers elle. Le registre des contrats et l'échéancier pointent vers les fiches et les dossiers, sans les dupliquer.
- L'index est le premier point de contrôle à chaque modification.
- Les agents signalent quand ils s'appuient sur une fiche `brouillon`.
- Un Drive personnel contient beaucoup de fichiers seulement en ligne : les lire les télécharge. Lire par priorité, pas tout d'un coup.
- Ne jamais renommer ni déplacer un document rangé hors de `_INBOX/`, ni créer un domaine sans l'accord du propriétaire. Seul l'archivage d'un sujet clos est proposé par l'agent, et fait après accord.
