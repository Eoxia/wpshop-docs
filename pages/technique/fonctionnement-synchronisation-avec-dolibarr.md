# Fonctionnement de la synchronisation des données.

Si un ERP est présent, il pilotera les données.

## Synchronisation

Explication de la synchronisation des données entre Dolibarr qui est l'ERP natif de WPshop.

### Les différents moyen de synchroniser

- Cas n°1 - Synchronisation en masse: Dans la page d'une des entitées en cliquant sur le bouton "Synchroniser tous les {nom_entitée}" (Ce bouton est disponible dans les pages: Tiers, Commandes et Produits.)
- Cas n°2 - Synchronisation d'une entrée: Dans le tableau des Tiers/Commandes/Produits, en cliquant sur le bouton de synchronisation sur la ligne désirée.
- Cas n°3 - Synchronisation d'une entreé: Dans la page d'édition d'un(e) Tier/Commande/Produit, en cliquant sur le bouton de synchronisation en haut de page.

Les 3 cas ont le même fonctionnement de synchronisation, c'est seulement le type d'entitée qui intervient sur comment est géré la synchronisation en terme de donnée.

### Les données synchronisées selon les entitées

La cohérence au niveau des données est certifiée grâce à un sha256 généré dans les deux plateformes lors de la synchronisation.

#### Tiers et contacts/adresses

Lors de la synchronisation des données d'un tier, nous synchronisons également ses contacts/adresses.
Pour voir les données synchronisées:

https://github.com/Eoxia/wpshop/blob/5768c56e70529ac07686759d204d16e3aaf528e4/modules/doli-proposals/class/class-doli-proposals.php#L40

Les données utilisées pour le sha256 pour certifié un tier et ses contacts/adresses sont les suivantes:
https://github.com/Eoxia/wpshop/commit/0a28ce1b1a4c4146738b2583afbb8e7fa9a1c57d#diff-1d6565ce1752cb775c8c8a8387e737e0R115

#### Devis

Pour voir les données synchronisées:

https://github.com/Eoxia/wpshop/blob/2.0.0/modules/doli-third-parties/class/class-doli-third-parties.php

Les données utilisées pour le sha256 pour certifié la synchronisation du devis sont les suivantes:
https://github.com/Eoxia/wpshop/blob/5768c56e70529ac07686759d204d16e3aaf528e4/modules/doli-proposals/class/class-doli-proposals.php#L108

#### Produits

Pour voir les données synchronisées: 
https://github.com/Eoxia/wpshop/blob/2.0.0/modules/doli-products/class/class-doli-products.php#L50

Les données utilisées pour le sha256 pour certifié un produit sont les suivantes:
https://github.com/Eoxia/wpshop/blob/a62f67e5860f1f52e2f584f5150b47df27a49aa9/modules/doli-products/class/class-doli-products.php#L77

### Déroulement de la synchronisation d'une entitée

1. Comparaison du SHA256
2. Si le SHA256 est différent les donnes sont écrasées par les données de l'ERP
3. SI OK on régenère le SHA256 
4. Stockage dans WordPress (wp_postmeta) dans les métas selon l'entité (Exemple produits dans postmeta, contact/adresse dans usersmeta)
5. Stockage dans Dolibarr

## Tunnel de vente

Déroulement du tunnel de vente en terme de data

Dans l'ordre:
1. Création du tier
2. Création d'un users
3. Devis
4. Connection avec un ERP (par défaut Dolibarr)
5. Création de la proposition commerciale
6. Création de la commande
7. Création de la facture

### Création d'un tier et contact/adresse associé

WP permet seulement d'entrée les données d'un tier dans le formulaire présent sur la page du tunnel de vente puis les envoies directement à dolibarr sans contrôle. C'est dolibarr qui va vérifier les entrées utilisateurs puis confirmer à WordPress que tout est OK.

1. Création du tier dans WordPress (Table wp_posts)
2. Création du users dans WordPress (Table wp_users)
2.1. Liaison du user au tier dans WordPress (Table wp_postmeta contact_ids)

Si un erp est connecté la fonction continue (l'erp par défaut est Dolibarr) sinon Sans ERP connecté les données resteront dans WordPress.
Synchronisation et pilotage de données avec Dolibarr
2.1.1 Appel la route POST /thirdparties de Dolibarr avec les données suivantes (Création dans Dolibarr):
- (string) name: "Customer Name"*
- (string) country: "Country Name"*
- (int) country_id: 1*
- (string) address: "Address Postal"*
- (string) zip: "75000"*
- (string) state: "State Name"*
- (string) phone: "Phone number"*
- (string) town: "Town Name"*
- (int) client: 1
- (string) code_client: "auto"
2.1.2 Contact/adresse appel de la route (
 -...@todo

* Cette donnée provient du formulaire dans la page du tunnel de vente.

**Manque l'ajout de l'entrée dans la table llx_wpshop avec le sha256 afin de confirmer la synchro**

### Création devis et affichage dans le compte
### Création de la proposition commerciale
### Création de la commande
### Création de la facture
## Les cas de désynchronisation
### Re-synchroniser
