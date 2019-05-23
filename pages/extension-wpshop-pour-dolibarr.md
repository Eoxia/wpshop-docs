# Extension WPshop pour Dolibarr

## Pourquoi ?

Nous avons besoin d'une cohérence des données entre les deux plateformes sans faute. 
Si la date de modification des deux plateformes sont équivalentes, celà veut dire que les données sont en cohérentes.

Le module Évènements/Agenda de Dolibarr permet d'ajouter une date lors de certains évènements:

| Évènement          | Description                         |
| ------------------ | ----------------------------------- |
| COMPANY_CREATE     | Tiers créé                          |
| COMPANY_SENTBYMAIL | Email envoyé depuis la fiche Tiers  |
| COMPANY_DELETE     | Third party deleted                 |
| PRODUCT_CREATE     | Product or service created          |
| PRODUCT_MODIFY     | Product or service modified         |

*Voir la liste complet des évènements*

Le problème vient de certains évènements manquants qui sont obligatoires pour notre synchronisation telles que:

- COMPANY_MODIFY
- CONTACT_CREATE
- CONTACT_MODIFY
- CONTACT_DELETE

L'extension WPshop pour dolibarr permet d'ajouter ses hooks afin de mêttre à jour les données lors de ces évènements sur WordPress.

## Fonctionnalité

Permet de synchroniser automatiquement les données d'une entitée dolibarr vers WPshop, lors de l'ajout, modification ou suppression de celle-ci.
