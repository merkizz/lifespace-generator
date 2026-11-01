---
titre: Guide du contexte de {{PROPRIETAIRE}}
type: meta
statut: actif
maj: {{DATE}}
---

# Guide du contexte de {{PROPRIETAIRE}}

Ce dossier est l'espace personnel et la source de vérité de {{PROPRIETAIRE}}. Il est lu par son propriétaire et chargé comme contexte par Claude (Cowork, Claude Code, claude.ai). Les règles de travail sont dans `CLAUDE.md` à la racine ; ce guide fixe les conventions.

## Utiliser le contexte depuis un autre projet

Si le dossier n'est pas le dossier de travail du projet, ajouter dans ses instructions :

```
Avant toute tâche, lis CLAUDE.md à la racine du dossier « {{DOSSIER_RACINE}} » et applique-le.
```

Ne pas relier ce dossier à un projet partagé avec d'autres personnes : il contient des données personnelles.

## Arborescence et nommage des dossiers

- Un domaine = un bloc de dizaines (plan dans `00-index.md`). Ses fiches vivent dans `<Domaine>/_INSTRUCTIONS/`.
- Les blocs forment une seule suite, attribuée dans l'ordre : 10, 20... 90, puis 100, 110... Un bloc attribué ne change jamais et n'est jamais réutilisé.
- Dans un bloc, X0 est la fiche de synthèse, X1 à X9 les fiches de détail (en général une par sujet important).
- Un nouveau domaine reçoit le prochain bloc libre, après accord de {{PROPRIETAIRE}}. Au-delà de 9 fiches de détail, un domaine reçoit un bloc d'extension (« Santé (suite) »).
- Dans un domaine, trois sortes de dossiers, en plus des dossiers protégés :
  - **sujet**, durable : `Organisme (Objet)` pour un contrat ou un organisme (`ASSUREUR (Assurance auto)`), `AAAA - Nom` pour un sujet daté par son début (`2019 - VOITURE`, `2016 - EMPLOYEUR`), ou un nom simple (`Chien`). Un sujet peut contenir des sous-dossiers par année ou par type (`Bulletins de paie/2024`) ;
  - **événement**, daté : `AAAAMMJJ - Titre`, avec la date de début (`20220905 - Dégât des eaux salle de bain`, `20240712 - LISBONNE`). Un événement peut aussi vivre dans un sujet (un sinistre dans le dossier du logement) ;
  - **classement**, par type de document figé, quand aucun sujet ne s'impose (`Factures`, `Impôts`, avec des sous-dossiers par année si besoin).
- `_ARCHIVES/` : un sujet ou un événement clos y est déplacé tel quel, avec son nom, dans le `_ARCHIVES/` du dossier qui le contenait : celui du domaine, ou celui du dossier de regroupement (exemple : `<Domaine>/Assurances/_ARCHIVES/`). Un dossier de regroupement (nom en écriture normale, exemple : `Assurances`) réunit des sujets de même nature et crée son `_ARCHIVES/` au premier archivage. Un contrat résilié, un ancien véhicule, un ancien employeur, un voyage passé de plus d'un an y vont, sur proposition de l'agent ou à l'initiative de {{PROPRIETAIRE}}.
- Dossiers de domaine, de sujet, d'événement et de classement : noms lisibles, majuscule initiale ou majuscules, accents autorisés.
- Fiches et fichiers transverses : `.md`, minuscules, en français, sans accents ni espaces, tirets simples (exception : `CLAUDE.md`). Nouvelle fiche : partir de `_INSTRUCTIONS/modeles/`.
- `_INSTRUCTIONS/` et `_REFERENCES/` ne sont pas modifiés à la main.

## Documents figés, documents de travail et nommage

Deux questions pour chaque document qui sort de `_INBOX/`. Un document rangé ailleurs n'est ni renommé ni déplacé : seule `_INBOX/` est un fourre-tout.

**1. Faut-il le renommer ?**

- **Document figé** : qu'on ne modifiera plus, en général reçu ou signé (facture, contrat, avenant, avis d'échéance, avis d'imposition, attestation, ordonnance, compte rendu médical, bulletin de paie, réservation, courrier officiel). Il est renommé.
- **Document de travail** : tout le reste, ce qu'on fait évoluer ou réutilise (tableur de dépenses, brouillon de courrier, liste, photo, plan). Il garde son nom.
- **Note brute** : texte sans valeur propre une fois son contenu intégré aux fiches (note rapide, texte collé, transcription, compte rendu d'interview). Elle est traitée comme un document figé, avec le type `NOTE` ou `INTERVIEW`.
- **En cas de doute : travail**, sans renommage.

**2. Où le ranger ?**

- Dans le dossier du sujet ou de l'événement auquel il se rattache.
- Sinon, document figé : dans le dossier de classement de son type s'il existe, sinon dans `_REFERENCES/` du domaine.
- Note brute : toujours dans `_REFERENCES/` du domaine.
- Un nouveau sujet, événement ou dossier de classement est créé sur demande, ou proposé par l'agent.

**Format des documents figés**

`AAAAMMJJ[_TYPE][_ID][_DESCRIPTION][_ORGANISME].ext`

- `AAAAMMJJ` : date du document (émission, signature, rédaction), jamais la date de rangement. À défaut, date de modification du fichier, signalée pour correction. Obligatoire, avec au moins un autre champ.
- `TYPE` : en majuscules, seulement si le document en a un (`FACTURE`, `CONTRAT`, `AVENANT`, `DEVIS`, `AVIS`, `ATTESTATION`, `ORDONNANCE`, `BULLETIN`, `RESERVATION`, `NOTE`, `INTERVIEW`...).
- `ID` : seulement avec un TYPE, la référence du document (n° de facture, de contrat). Jamais un numéro sensible (sécurité sociale, IBAN, pièce d'identité).
- `DESCRIPTION` : écrite comme une phrase, majuscule initiale, noms propres conservés.
- `ORGANISME` : en majuscules, l'émetteur ou le destinataire.
- Sans accents ni espaces ; `_` entre les champs, `-` à l'intérieur d'une valeur.
- Exemples : `20230415_FACTURE_F-2023-0412_VETERINAIRE.pdf`, `20220110_AVIS_Echeance-2022_ASSUREUR.pdf`, `20240601_RESERVATION_123456789_HOTEL.pdf`, `20250310_INTERVIEW_Sante.md`.

Un document déjà conforme garde son nom. Un document de travail garde toujours son nom.

Dates : `AAAAMMJJ` dans les noms de fichiers et de dossiers, `AAAA-MM-JJ` dans les textes.

## Synthèse et détail : la règle de non-perte

1. La fiche de synthèse (X0) est chargée par défaut.
2. Chaque fiche de détail commence par une section « L'essentiel » (10 lignes max) : c'est la seule partie que la synthèse a le droit de reformuler.
3. On ne supprime jamais une information en synthétisant : on la déplace dans une fiche de détail et on laisse un pointeur explicite dans la synthèse (« détail : 61-voiture.md, section Entretien »).
4. Les documents sources sont cités dans la section « Sources » de la fiche. Chaîne complète : synthèse, puis détail, puis document source.
5. Un sujet archivé garde sa fiche de détail, marquée « clos » dans « L'essentiel », avec le nouveau chemin de son dossier.

## Registres transverses

- `06-echeancier.md`, `07-contrats.md`, `08-contacts.md` donnent la vue d'ensemble ; ils pointent vers les fiches et les dossiers, sans dupliquer leur contenu.
- Identifiants uniques et définitifs : `E-001` (échéances), `C-001` (contrats), `T-001` (tâches), `V-001` (points de vigilance).

## Frontmatter

```yaml
---
titre: Titre de la fiche
bloc: 60 Véhicules
type: meta | synthese | detail
statut: vide | brouillon | valide | actif
maj: AAAA-MM-JJ
sources: [chemins ou liens vers les documents d'origine]
details: [fiches de détail rattachées, pour les synthèses]
---
```

- `valide` : contenu relu par {{PROPRIETAIRE}}. Une modification d'une fiche `valide` est soumise à validation dans la session, passage par passage (voir `CLAUDE.md`) ; sans validation, la fiche repasse en `brouillon`. `02-memoire.md` garde ce qui a changé.
- `actif` : réservé aux fichiers transverses (`type: meta`).

## Alimenter le contexte : 6 canaux

Règle simple : si Claude doit connaître un document, passer par `_INBOX/` ou dire « Traite ce fichier ». Sinon, le ranger où l'on veut, sans rien dire.

1. `_INBOX/` : déposer n'importe quel document, puis demander « Traite l'inbox ».
2. Sur place : ranger soi-même le document, puis demander « Traite ce fichier ».
3. Connecteurs : Claude va chercher dans les outils déclarés ({{SOURCES}}).
4. Relève : « Relève les connecteurs », Claude cherche les nouveaux documents depuis la dernière relève et les fait entrer par `_INBOX/`.
5. Interview guidée : « Interview Santé », Claude pose ses questions sur un domaine puis rédige ses fiches.
6. Chat direct : coller du texte ou joindre des fichiers.

Revue périodique : « Fais le point ». Protocoles détaillés dans `CLAUDE.md`.

## Règles d'écriture des fiches

- Factuel, daté quand c'est pertinent.
- Phrases courtes, sans remplissage : ces fichiers sont du contexte, pas de la communication.
- Aucune donnée sensible (voir `CLAUDE.md`, section « Données sensibles ») : pointer vers le document.
