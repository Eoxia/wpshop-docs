# Fonctionnement de la synchronisation avec Dolibarr.

Dolibarr contrôle les données

## Association

Une entitée peut être associée si celle-ci ne l'es pas déjà.

## Synchronisation

Explication de la synchronisation des données entre dolibarr et WPshop.

### Les différents moyen de synchroniser

- Cas n°1 - Synchronisation en masse: Dans la page d'une des entitées en cliquant sur le bouton "Synchroniser tous les {nom_entitée}" (Ce bouton est disponible dans les pages: Tiers, Commandes et Produits.)
- Cas n°2 - Synchronisation d'une entrée: Dans le tableau des Tiers/Commandes/Produits, en cliquant sur le bouton de synchronisation sur la ligne désirée.
- Cas n°3 - Synchronisation d'une entreé: Dans la page d'édition d'un(e) Tier/Commande/Produit, en cliquant sur le bouton de synchronisation en haut de page.

Les 3 cas ont le même fonctionnement de synchronisation, c'est seulement le type d'entitée qui intervient sur comment est géré la synchronisation en terme de donnée.

### Les données synchronisées selon les entitées

#### Tiers

Lors de la synchronisation des données d'un tier, nous synchronisons également ses contacts.

Pour voir les données synchronisées: https://github.com/Eoxia/wpshop/blob/2.0.0/modules/doli-third-parties/class/class-doli-third-parties.php

#### Commandes



#### Produits

### Déroulement d'une synchronisation d'une entitée

## Tunnel de vente

Déroulement du tunnel de vente en terme de data

Dans l'ordre:
1. Création du tier
2. Création de la propal
3. Création de la commande
4. Création de la facture

### Création du tier

1. Création du tier dans WP
2. Création du contact dans WP
3. Liaison du contact au tier (contact_ids)
4. Appel la route POST /thirdparties de dolibarr avec les données suivantes:

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

* Cette donnée provient du formulaire dans la page du tunnel de vente.



### Création de la propal
### Création de la commande
### Création de la facture

## Les cas de désynchronisation

### Re-synchroniser
