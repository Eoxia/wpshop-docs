# WPshop avec Dolibarr

Pour gérer l'association et la synchronisation d'un produit entre WPshop et Dolibarr, nous utilisons la métadonnée "**external_id**".
Nous communiquons avec la REST API de Dolibarr et WordPress pour effectuer les associations et synchronisations.
Dolibarr contrôle les données de WPshop. Nous écrasons toujours les données de WP avec celle de Dolibarr.

## Les différents cas d'association

* Nouveau produit depuis WPshop
* Nouveau produit depuis Dolibarr
* Produit existant dans WPshop uniquement
* Produit existant dans Dolibarr uniquement

## Les différents cas de synchronisation

* Modification d'un produit depuis WPshop
* Modification d'un produit depuis Dolibarr
* Resynchroniser après une désynchronisation

## Association

### Nouveau produit depuis WPshop

Nous nous accrochons sur le hook "save_post" de WordPress pour appeler une fonction qui vas communiquer à Dolibarr la création d'un nouveau produit.

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

#### Si la route ne rencontre pas d'erreur

Mise à jour des informations du produit dans WordPress avec les données de dolibarr: prix HT, Taux de TVA, Prix TTC.
Met la dernière date de synchronisation récupérer depuis la table llx_wpshop_product dans la métadonnée **_date_last_synchro**.
Met l'ID du produit de dolibarr dans la métadonnée **external_id**.

#### Si la route rencontre une erreur

### Nouveau produit depuis Dolibarr

Nous nous accrochons sur le hook "PRODUCT_CREATE" de Dolibarr pour appeler une fonction qui vas communiquer à WordPress la création d'un nouveau produit.

Dans cette fonction, nous envoyons une requête POST à la route /wp-json/wpshop/v1/product avec les données suivantes:

* title: Le titre du produit
* price: Le prix HT du produit
* price_ttc: Le prix TTC du produit
* tva_tx: Le % de tva du produit
* date_last_synchro: La dernière date de synchronisation récupérer depuis la table llx_wpshop_product.
* external_id: L'ID du produit dans Dolibarr

Cette route nous renvoies les données du nouveau produit dans WordPress.

Après la réponse de la route, nous ajoutons dans la table llx_wpshop_product une nouvel entrée pour ajouter les informations d'association de ce produit avec comme donnée:

* wp_product: L'ID du produit dans WordPress
* fk_product: L'ID du produit dans Dolibarr
* sync_date: La date d'association
* last_sync_date: La dernière date de synchronisation

## Synchronisation

### Modification d'un produit depuis WPshop

Nous nous accrochons sur le hook "save_post" de WordPress pour appeler une fonction qui vas communiquer à Dolibarr la modification d'un produit.

Dans cette fonction, nous envoyons une requête PUT à la route /wpshopapi/update/product/{id} avec les données suivantes:

* label: Le titre du produit
* description: La description du produit
* price: Le prix HT du produit
* tva_tx: Le % de TVA du produit
* fk_product: L'ID du produit dans Dolibarr
* wp_product: L'ID du produit sur WP

Cette route modifie le produit {id} dans dolibarr, et modifie également l'entrée **last_sync_date** dans la table llx_wpshop_product correspondant à fk_product et wp_product avec le timestamp actuel.

Une fois que la requête nous renvoies une réponse, nous mettons à jour les informations du produit avec les données de dolibarr: prix HT, Taux de TVA, Prix TTC.

Puis met la dernière date de synchronisation récupérer depuis la table llx_wpshop_product dans la métadonnée **_date_last_synchro**.

### Modification d'un produit depuis Dolibarr

Nous nous accrochons sur le hook "PRODUCT_MODIFY" de Dolibarr pour appeler une fonction qui vas communiquer à WordPress la modification d'un produit.

Dans cette fonction, nous mettons à jour la donnée **last_sync_date** avec le timestamp actuel dans la table llx_wpshop_product correspondant à fk_product (L'ID du produit dans dolibarr).

nous envoyons une requête POST à la route /wp-json/wpshop/v1/product/{id} avec les données suivantes:

* title: Le titre du produit
* price: Le prix HT du produit
* price_ttc: Le prix TTC du produit
* tva_tx: Le % de tva du produit
* date_last_synchro: La dernière date de synchronisation récupérée depuis la table llx_wpshop_product.

WordPress de son coté met à jour le produit dans la base de donnée ainsi que la dernière date de synchronisation.
