# FAQ

## Les factures restent impayées

Vous devez configurer une banque sur Dolibarr.

## Les paiements stripe ne passent pas la commande en payée et aucune facture n'est créée

Vous devez configurer le webhook depuis stripe vers la page <votresite.com>/wp-json/wpshop/v2/wps_gateway_stripe avec l'évènement: checkout.session.completed

