# lifespace-generator

Méthode pour générer l'espace personnel d'une personne (son « espace de vie ») à partir de son Drive (Google Drive ou autre), avec un agent Claude (Cowork ou Claude Code). Adaptation de `workspace-generator` à un usage personnel : pas de services ni d'équipe, mais des domaines de vie (administratif, santé, logement, voiture, voyages, animaux...) et un propriétaire unique.

L'espace généré range les documents de chaque domaine et tient un contexte personnel à jour : des fiches lisibles par le propriétaire et chargées automatiquement par les agents, avec un index, une mémoire, des leçons, des points de vigilance, une liste de tâches, un échéancier, un registre des contrats et un carnet de contacts.

## Ce que produit la méthode

```
<DOSSIER_RACINE>/
  CLAUDE.md            règles de travail, lues automatiquement par l'agent
  _INSTRUCTIONS/       index, guide, mémoire, leçons, vigilance, tâches, échéancier, contrats, contacts
  _INBOX/              seule entrée des documents bruts
  <Domaine>/
    _INSTRUCTIONS/     fiches de contexte du domaine (synthèse et détail)
    _REFERENCES/       documents figés sans dossier dédié, notes brutes, comptes rendus d'interview
    _Archives/         sujets et événements clos
    <Sujets>/          exemple : MACIF (Assurance auto), 2020 - RENAULT CLIO
    <Événements>/      exemple : 20230118 - Dégât des eaux cuisine
```

Une fois l'espace généré, le propriétaire l'alimente en langage naturel : « Traite l'inbox », « Traite ce fichier », « Interview Santé », « Fais le point ».

## Différences avec workspace-generator

- Des domaines de vie à la place des services, et un propriétaire à la place d'un responsable et d'une équipe.
- Dans chaque domaine, des dossiers de sujet (durables), d'événement (datés) et un dossier `_Archives/`.
- Trois fichiers transverses en plus : `06-echeancier.md`, `07-contrats.md`, `08-contacts.md`.
- Une génération en mode reprise : un Drive personnel est souvent déjà rangé, le tri se fait dossier par dossier et non fichier par fichier, puis les documents sont lus par priorité.
- Des protocoles propres à la vie personnelle : « Fais le point » (revue périodique) et « Relève les connecteurs ».
- Des règles sur les données sensibles : aucun mot de passe, IBAN complet ni numéro de sécurité sociale recopié dans une fiche.

## Contenu du dépôt

- `_LIFESPACE-GENERATOR/` : le dossier de la méthode, à copier tel quel dans l'espace à générer.
  - `METHODE.md` : la méthode complète (préparation, génération, conventions).
  - `PARAMETRES.md` : les paramètres du propriétaire, à remplir.
  - `templates/` : les modèles copiés lors de la génération.
  - `CLAUDE.md` : consignes pour l'agent qui lit ce dossier.
- `_prive/` : non versionné, pour garder localement un `PARAMETRES.md` rempli.

## Utilisation

1. Créer le dossier racine sur le Drive, en général `ESPACE-PRENOM`. Son nom est le paramètre `{{DOSSIER_RACINE}}` : le choisir avec soin, il est coûteux à changer une fois relié à des projets.
2. Y copier `_LIFESPACE-GENERATOR/` et remplir `_LIFESPACE-GENERATOR/PARAMETRES.md`.
3. Créer le dossier `<DOSSIER_RACINE>/_INBOX/` et y déplacer le contenu existant du Drive, en gardant une sauvegarde ailleurs.
4. Relier `<DOSSIER_RACINE>` à une session Cowork ou Claude Code et lancer :

   ```
   Lis _LIFESPACE-GENERATOR/METHODE.md puis génère l'espace
   ```

5. Valider les étapes proposées par l'agent : liste des domaines, tableau de correspondance, puis relecture des fiches.
6. Une fois la génération validée, retirer `_LIFESPACE-GENERATOR/` de l'espace.

Le détail de chaque étape est dans `_LIFESPACE-GENERATOR/METHODE.md`.

## Faire évoluer la méthode

Toute modification se fait dans les modèles génériques de `_LIFESPACE-GENERATOR/`. Rien de propre à une personne ne doit y figurer : ses valeurs vont uniquement dans son `PARAMETRES.md`, jamais versionné rempli dans ce dépôt.

Règles d'écriture : en français, jamais de tiret cadratin, dates au format `AAAA-MM-JJ`.
