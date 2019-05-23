# Extension WPshop pour Dolibarr

## Pourquoi ?

## fonctionnalité

L'extension WPshop pour dolibarr ajoutes la gestion des dates lors de la synchronisation entre WPShop et Dolibarr.

Chaque synchronisation depuis une des deux plateformes permet d'ajouter une date de synchronisation dans la base de donnée de Dolibarr lié à l'ID du produit dans WP et dans Dolibarr.

Voici un tableau représentant les données enregistrées pour un produit dans dolibarr:

- rowid: ID de la ligne
- fk_product: ID du produit dans dolibarr
- wp_product: ID du produit dans WPshop
- row_date: Date de la création de la ligne (Format MySQL)
- sync_date: Date de la dernière synchronisation (Format MySQL)

| rowid | fk_product | wp_product | row_date            | sync_date           |
| ----- | ---------- | ---------- | ------------------- | ------------------- |
| 1     | 1          | 1          | 2019-05-23 12:00:00 | 2019-05-23 12:00:00 |
| 2     | 3          | 4          | 2019-05-23 12:12:12 | 2019-05-23 18:10:01 |
