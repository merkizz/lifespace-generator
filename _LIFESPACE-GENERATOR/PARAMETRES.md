# Paramètres de la méthode

> **À remplir avant toute exécution.** Remplacer chaque `[À COMPLÉTER]` : la génération s'arrête tant qu'il en reste un. Pour les valeurs courtes, la valeur est la ligne entre accents graves ; le texte qui suit l'explique et n'est pas recopié. Ces valeurs remplacent les variables `{{...}}` des modèles de `templates/`. Ce fichier n'est pas copié dans l'espace généré : après la génération, toute correction se fait dans les fichiers générés (voir `METHODE.md`, section « Après la génération »).

## `{{PROPRIETAIRE}}`

`[À COMPLÉTER : Prénom NOM]`

Propriétaire de l'espace. Valide les domaines, le tri et les fiches, et signe le journal.

## `{{DOSSIER_RACINE}}`

`[À COMPLÉTER : nom du dossier racine, en général ESPACE-PRENOM]`

Nom exact du dossier racine de l'espace. Coûteux à changer une fois monté dans des projets.

## `{{PRESENTATION}}`

[À COMPLÉTER : en quelques phrases, qui est le propriétaire (situation, lieu de vie, situation professionnelle), qui compose le foyer (personnes, animaux), les biens principaux (logement, véhicule), ce qu'il attend de l'agent (ranger, suivre les échéances, préparer les démarches, préparer les voyages...) et les priorités du moment. Ce texte ouvre le `CLAUDE.md` de l'espace et s'adresse directement à l'agent (« Tu travailles avec... »). Ne mettre aucune donnée sensible (numéros, identifiants, santé détaillée).]

## `{{DOMAINES}}`

Un domaine par ligne, dans l'ordre des blocs : le premier reçoit le bloc 10, le suivant 20, etc., puis 100, 110... au-delà du neuvième (voir `METHODE.md`). Le périmètre sert de critère de tri des documents : le décrire par les sujets et types de documents qu'il couvre. Un animal, un logement ou un projet important peut être un domaine à part entière.

Exemple de liste : Administratif, Travail, Finances et patrimoine, Logement, Santé, Véhicules, Voyages, Animaux, Achats et garanties, Vie quotidienne.

| Domaine | Périmètre |
|---|---|
| [À COMPLÉTER] | [À COMPLÉTER] |
| [À COMPLÉTER] | [À COMPLÉTER] |

## `{{SOURCES}}`

`[À COMPLÉTER : messagerie, agenda, espaces clients, outils (Notion, Drive...), personnes à interroger]`

Où chercher une information manquante, et ce que « Relève les connecteurs » consulte.

## Dossiers de classement (facultatif)

Dossiers dédiés à un type de document figé dans un domaine (exemple : `Factures` dans Achats et garanties pour le type `FACTURE`, `Impôts` dans Administratif), créés dès la génération. Les autres seront proposés pendant le tri. Laisser « (aucun) » si aucun n'est prévu.

| Domaine | Dossier | Type reçu |
|---|---|---|

(aucun)

## `{{PREFERENCES}}` (facultatif)

Préférences propres au propriétaire, en plus des préférences par défaut de la méthode. Format : règle, pourquoi, `(date, auteur)`. Laisser « (aucune) » si aucune n'est prévue.

- (aucune)
