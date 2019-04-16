# WPshop 1 vers WPshop 2

Les entitées WPshop 1 et 2 sont similaires cependant l'entité **adresse** n'est plus existantes, en résumé nous retrouvons:

|          | WPshop 1 | WPshop 2 |
| -------- | -------- | -------- |
| Entitée  |          |          |
| Tier     | Oui      | Oui      |
| Contact  | Oui      | Oui      |
| Adresse  | Oui      | Non      |
| Produit  | Oui      | Oui      |
| Commande | Oui      | Oui      |
| Facture  | Non      | Oui      |

WPshop 2 proposes uniquement la migration de **tier** ainsi que leurs **contacts**.

## Migration des tiers

Techniquement, seulement quelques méta données sur le tier doit être ajoutées:

Les méta données suivantes sont les nouvelles de WPshop 2

* _contact_ids: Les ID des contacts attachés à ce tier
* _address: L'adresse du tier
* _zip: Le code postal du tier
* _town: La ville du tier
* _country: Le pays du tier

Tableau de liaison

|            |  WPshop 1                                                            | WPshop 2  |
| ---------- | -------------------------------------------------------------------- | --------- |
| Entitée v1 |                                                                      |           |
| Address    | Donnée **address** de la méta déserialisé \_wpshop_address_metadata  | \_address |
| Address    | Donnée **postcode** de la méta déserialisé \_wpshop_address_metadata | \_address |
| Address    | Donnée **city** de la méta déserialisé \_wpshop_address_metadata     | \_address |
| Address    | Donnée **country** de la méta déserialisé \_wpshop_address_metadata  | \_address |

## Migration des contacts

Une seul méta nous intèresse sur le contact:

Les méta données suivantes sont les nouvelles de WPshop 2

* _phone: Le numéro de téléphone du contact

Tableau de liaison
