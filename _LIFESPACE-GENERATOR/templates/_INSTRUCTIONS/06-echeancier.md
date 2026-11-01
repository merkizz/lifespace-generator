---
titre: Échéancier de {{PROPRIETAIRE}}
type: meta
statut: actif
maj: {{DATE}}
---

# Échéancier : dates à venir

Toutes les dates qui appellent une action : fin d'engagement et préavis de résiliation, expiration de papiers, contrôle technique, entretien, vaccins, déclarations et paiements d'impôts, fin de garantie, rendez-vous importants. Revu par « Fais le point ». Il n'est pas modifié à la main : le demander à Claude.

Règles :

- Identifiant unique et définitif `E-001`, `E-002`...
- `Date` : la date limite d'action (pour un contrat avec préavis, la date limite de résiliation, pas la date de fin).
- `Rappel` : combien de jours avant la date le sujet doit remonter (30 par défaut).
- `Périodicité` : annuelle, mensuelle, tous les N ans, ou vide si ponctuelle. Une échéance récurrente close crée la suivante.
- Le tableau « À venir » est trié par date. Une échéance passée ou traitée part dans « Passées », avec son issue. Les échéances passées de plus d'un an partent dans `archives/echeancier-AAAA.md`.

## À venir

| ID | Date | Objet | Domaine | Action | Rappel | Périodicité | Source | Tâche |
|----|------|-------|---------|--------|--------|-------------|--------|-------|

## Passées

| ID | Date | Objet | Issue |
|----|------|-------|-------|
