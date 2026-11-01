---
titre: Index du contexte de {{PROPRIETAIRE}}
type: meta
statut: actif
maj: {{DATE}}
---

# Index du contexte de {{PROPRIETAIRE}}

> Point d'entrée obligatoire. Lire ce fichier en premier, puis charger uniquement les fiches utiles à la tâche. Conventions : `01-guide.md`. Règles de travail : `CLAUDE.md` à la racine.

## Fichiers transverses (`_INSTRUCTIONS/` à la racine)

| N° | Fichier | Contenu | Statut |
|----|---------|---------|--------|
|  | `CLAUDE.md` (racine) | Instructions de travail, lues automatiquement | actif |
| 00 | `00-index.md` | Carte du contexte, point d'entrée | actif |
| 01 | `01-guide.md` | Conventions et alimentation du contexte | actif |
| 02 | `02-memoire.md` | Journal daté des mises à jour, dernière revue, dernière relève | actif |
| 03 | `03-lecons.md` | Règles apprises, à respecter partout | actif |
| 04 | `04-points-de-vigilance.md` | Contradictions ouvertes entre sources | actif |
| 05 | `05-todo.md` | Tâches | actif |
| 06 | `06-echeancier.md` | Dates à venir et rappels | actif |
| 07 | `07-contrats.md` | Registre des contrats et abonnements | actif |
| 08 | `08-contacts.md` | Interlocuteurs utiles | actif |
|  | `modeles/` | Modèles de fiche de synthèse et de détail | actif |
|  | `archives/` | Tâches et échéances closes, tableau de reprise initiale | actif |

## Domaines

Le périmètre sert de critère pour ranger les documents (« Traite l'inbox »). La colonne « Dossiers » liste les sujets et événements en cours et les dossiers de classement (avec le type reçu, par exemple `Factures (FACTURE)`). Les éléments clos sont dans le `_ARCHIVES/` du dossier qui les contenait (domaine ou dossier de regroupement) et ne sont pas listés ici.

| Bloc | Domaine | Dossier | Périmètre | Dossiers |
|------|---------|---------|-----------|----------|
| 00-09 | Transverse | `_INSTRUCTIONS/` | fichiers transverses | |
| {{BLOC}} | {{Domaine}} | `{{Domaine}}/` | {{Périmètre}} | {{Dossiers}} |

Blocs attribués dans l'ordre (10, 20... 90, puis 100, 110...), jamais réutilisés. Prochain bloc libre : {{BLOC_LIBRE}}. Un bloc d'extension se déclare comme une ligne « Domaine (suite) ».

## Fiches

| N° | Fichier | Domaine | Type | Contenu | Statut |
|----|---------|---------|------|---------|--------|
| {{X0}} | `{{Domaine}}/_INSTRUCTIONS/{{X0}}-{{domaine}}.md` | {{Domaine}} | synthese | Synthèse du domaine {{Domaine}} | vide |

Types : `meta`, `synthese`, `detail`. Statuts des fiches : `vide`, `brouillon`, `valide` ; `actif` est réservé aux fichiers transverses.

## Dossiers spéciaux

- `_INBOX/` : dépôt de tout document brut. Traité sur demande (« Traite l'inbox »), voir `CLAUDE.md`.
- `<Domaine>/_REFERENCES/` : documents figés sans dossier dédié, notes brutes et comptes rendus d'interview.
- `<Domaine>/_ARCHIVES/` : sujets et événements clos, avec leur arborescence ; créé au premier archivage. Un dossier de regroupement a son propre `_ARCHIVES/` (`<Domaine>/<Regroupement>/_ARCHIVES/`).
