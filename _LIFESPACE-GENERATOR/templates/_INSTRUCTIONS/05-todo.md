---
titre: Tâches de {{PROPRIETAIRE}}
type: meta
statut: actif
maj: {{DATE}}
---

# Tâches de {{PROPRIETAIRE}}

Tableau de bord des tâches. Lu au début de chaque session (voir `CLAUDE.md`). Il n'est pas modifié à la main : pour ajouter, mettre à jour ou clore une tâche, le demander à Claude.

Statuts : à planifier, à faire, en cours, terminé, annulé. Chaque tâche a un identifiant unique et définitif (`T-001`, `T-002`...), jamais réutilisé. Une tâche change de section quand son statut change. Une tâche datée a aussi une ligne dans `06-echeancier.md`. Les tâches terminées ou annulées depuis plus de 30 jours sont déplacées dans `archives/todo-AAAA.md`.

Modèle d'une tâche :

```
### T-000 Titre court
- Domaine : Véhicules
- Créée : AAAA-MM-JJ
- Échéance : AAAA-MM-JJ (E-000), si datée
- Notes :
  - AAAA-MM-JJ : avancement, décision, blocage
- Revue (à la clôture) : livrables, décisions, points ouverts
```

## En cours

## À faire

## À planifier

## Terminé

## Annulé
