---
titre: Registre des contrats de {{PROPRIETAIRE}}
type: meta
statut: actif
maj: {{DATE}}
---

# Registre des contrats et abonnements

Vue d'ensemble de tous les contrats : banques, assurances, crédits, énergie, télécoms, abonnements, épargne. Le détail vit dans les fiches et les dossiers de sujet des domaines. Il n'est pas modifié à la main : le demander à Claude.

Règles :

- Identifiant unique et définitif `C-001`, `C-002`...
- `Référence` : partielle (`...4130`), jamais un IBAN, un numéro de carte ou un identifiant de connexion.
- `Échéance` : date de fin ou de renouvellement ; `Préavis` : délai de résiliation. Chaque échéance utile a une ligne dans `06-echeancier.md`.
- `Coût` : montant et périodicité (`12,99 EUR/mois`), d'après le dernier document connu, cité en source.
- `Dossier` : chemin du dossier de sujet.
- À la résiliation, la ligne passe dans « Résiliés » avec sa date de fin.

## En cours

| ID | Organisme | Objet | Domaine | Référence | Début | Échéance | Préavis | Coût | Dossier | Source |
|----|-----------|-------|---------|-----------|-------|----------|---------|------|---------|--------|

## Résiliés

| ID | Organisme | Objet | Domaine | Fin | Dossier |
|----|-----------|-------|---------|-----|---------|
