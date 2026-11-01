# lifespace-generator

Ce dossier contient une méthode pour générer l'espace personnel d'une personne. Ce n'est pas le contexte lui-même : n'utilise aucun fichier d'ici comme source de faits sur une personne.

- `METHODE.md` : la méthode, à lire en premier.
- `PARAMETRES.md` : les paramètres du propriétaire, à remplir entièrement avant toute exécution.
- `templates/` : les modèles copiés lors de la génération, avec des variables `{{...}}`. `templates/CLAUDE.md` est le futur `CLAUDE.md` de l'espace : ne l'applique pas ici.

Pendant la génération, ce dossier est placé dans l'espace à générer sous le nom `_LIFESPACE-GENERATOR/`, puis retiré une fois la génération validée. N'exécute la méthode que sur demande explicite. Toute modification de la méthode se fait dans les modèles génériques ; ce qui est propre à une personne va dans `PARAMETRES.md`.

Règles d'écriture : jamais de tiret cadratin, dates au format `AAAA-MM-JJ`, conventions de nommage de `METHODE.md`.
