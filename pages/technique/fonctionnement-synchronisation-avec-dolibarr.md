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

Lors de la synchronisation des données d'un tier, nous synchronisons également ses contacts/adresses.

Pour voir les données synchronisées: https://github.com/Eoxia/wpshop/blob/2.0.0/modules/doli-third-parties/class/class-doli-third-parties.php




#### Commandes



#### Produits

### Déroulement d'une synchronisation d'une entitée

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

### Création tier et contact/adresse associé

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
