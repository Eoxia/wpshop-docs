# WPshop avec Dolibarr

Pour gérer l'association et la synchronisation d'un produit entre WPshop et Dolibarr, nous utilisons la métadonnée "**external_id**".
Nous communiquons avec la REST API de Dolibarr et WordPress pour effectuer les associations et synchronisations.
Dolibarr contrôle les données de WPshop. Nous écrasons toujours les données de WP avec celle de Dolibarr.

## Les différents cas d'association

* Nouveau produit depuis WPshop
* Nouveau produit depuis Dolibarr

## Les différents cas de synchronisation

* Modification d'un produit depuis WPshop
* Modification d'un produit depuis Dolibarr

## Nouveau produit depuis WPshop

Nous nous accrochons sur le hook "save_post" de WordPress pour appeler une fonction qui vas communiquer à Dolibarr la création du nouveau produit.

Dans cette fonction, nous envoyons une requête POST à la route /wpshopapi/associate/product avec les données suivantes:

* ref: Le slug du produit
* label: Le titre du produit
* description: La description du produit
* price: Le prix HT du produit
* tva_tx: Le % de TVA du produit
* status: 1 (Produit en vente)
* status_buy: 1 (Produit en achat)
* wp_product: L'ID du produit sur WP

Cette route créer un nouveau produit dans dolibarr, et également une entrée dans la table llx_wpshop_product avec comme donnée:
* fk_product (L'ID de dolibarr)
* wp_product (L'ID de WP)
* sync_date (le timestamp de l'association)
* last_sync_date (le timestamp de la dernière synchronisation)

Cette route nous renvoies les données du nouveau produit dans dolibarr, ou une erreur si la référence (ref) est déjà existante.

### Si la route ne rencontre pas d'erreur

Mise à jour des informations des produits avec les données de dolibarr: prix HT, Taux de TVA, Prix TTC.
Met la dernière date de synchronisation récupérer depuis la table llx_wpshop_product dans la métadonnée **_date_last_syncho**.
Met l'ID du produit de dolibarr dans la métadonnée **external_id**.

### Si la route rencontre une erreur

## Nouveau produit depuis Dolibarr

## Modification d'un produit depuis WPshop

## Modification d'un produit depuis Dolibarr
