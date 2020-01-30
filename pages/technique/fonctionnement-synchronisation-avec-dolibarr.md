# Fonctionnement de la synchronisation avec Dolibarr.

Dolibarr contrôle les données

## Association

Une entitée peut être associée si celle-ci ne l'es pas déjà.

## Synchronisation

Explication de la synchronisation des données entre dolibarr et WPshop.
Chaque entitée peut être synchroniser depuis WP vers Dolibarr ou vice versa.

### Les différents moyen de synchroniser

- Cas n°1 - Synchronisation en masse: Dans la page d'une des entitées en cliquant sur le bouton "Synchroniser tous les {nom_entitée}" (Ce bouton est disponible dans les pages: Tiers, Commandes et Produits.)
- Cas n°2 - Synchronisation d'une entrée: Dans le tableau des Tiers/Commandes/Produits, en cliquant sur le bouton de synchronisation sur la ligne désirée.
- Cas n°3 - Synchronisation d'une entreé: Dans la page d'édition d'un(e) Tier/Commande/Produit, en cliquant sur le bouton de synchronisation en haut de page.

Les 3 cas on le même fonctionnement de synchronisation, c'est seulement le type d'entitée qui intervient sur comment est géré la synchronisation en terme de donnée.

### Les données synchronisées selon les entitées

#### Tiers

Lors de la synchronisation des données d'un tier, nous synchronisons également ses contacts. (**Excepté dans la direction WP => Doli, la synchronisation des contacts ne s'applique pas**)

Pour voir les données synchronisées: https://github.com/Eoxia/wpshop/blob/2.0.0/modules/doli-third-parties/class/class-doli-third-parties.php

#### Commandes



#### Produits

### Déroulement d'une synchronisation d'une entitée

## Tunnel de vente

## Les cas de désynchronisation

### Re-synchroniser
