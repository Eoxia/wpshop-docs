# WPshop avec Dolibarr (Deprecated, cette documentation n'est plus à jour 30/01/2020)

**Ceci est la documentation technique pour les développeurs pour l'association et la synchronisation de données entre WPshop et Dolibarr.**

Pour gérer l'association et la synchronisation d'un produit entre WPshop et Dolibarr, nous utilisons la métadonnée "**external_id**".

Nous communiquons avec la REST API de Dolibarr et WordPress pour effectuer les associations et synchronisations.

Dolibarr contrôle les données de WPshop. Nous écrasons toujours les données de WP avec celle de Dolibarr.

Lors d'une association d'un produit de WP vers Dolibarr (ou vice versa), une synchronisation automatique s'effectue **toujours** après l'association.

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

### Produit existant sur WPshop uniquement

Pour ce cas la, nous utilisons la fonction "associate_and_synchronize" dans la classe class-doli-synchro du module "doli-synchro".

Cette fonction demande 3 paramètres:

* from: Depuis qu'elle plateforme nous voulons associer. Peut être 'wpshop', 'dolibarr'.
* wp_id: L'ID de l'entité sur WP
* entry_id: L'ID de l'entité sur Dolibarr

*Le paramètre from est utile pour la première synchronisation de donnée et permet de choisir si nous voulons écraser les données depuis WPshop ou depuis Dolibarr.*

#### Depuis Dolibarr

La fonction appel la route selon le type de l'entitée, prenons le cas d'un produit:

Récupères les données du produit sur Dolibarr par le biais de la route GET /wpshopapi/products/{id}.

Une fois les données récupérées, nous écrasons les données du produit sur WordPress comme suit:

* title: Le titre du produit depuis Dolibarr
* price: Le prix HT du produit depuis Dolibarr
* price_ttc: Le prix TTC du produit depuis Dolibarr
* tva_tx: Le % de tva du produit depuis Dolibarr
* date_last_synchro: La dernière date de synchronisation récupérer depuis la table llx_wpshop_product
* external_id: L'ID du produit depuis Dolibarr

*Rappel: l'association s'effectue grâce à external_id.*

#### Depuis WordPress

### Produit existant sur Dolibarr uniquement

Pour ce cas la, nous utilisons les fonctions suivantes dans WPshop:

* sync_third_parties
* sync_contacts
* sync_products
* sync_proposals
* sync_orders
* sync_invoices
* sync_payments

#### sync_third_parties
#### sync_contacts
#### sync_products
#### sync_proposals
#### sync_orders
#### sync_payments

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
