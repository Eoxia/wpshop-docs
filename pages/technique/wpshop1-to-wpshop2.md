# WPshop 1 vers WPshop 2

Les entitées de WPshop 1 et 2 ne sont pas exactement similaires, c'est pourquoi nous faisons une migration, en résumé nous retrouvons:

|              | WPshop 1      | WPshop 2      |
| --------     | ------------- | ------------- |
| **Entitée**  |               |               |
| Tier         | Existante     | Existante     |
| Contact      | Existante     | Existante     |
| Adresse      | Existante     | Non Existante |
| Produit      | Existante     | Existante     |
| Commande     | Existante     | Existante     |
| Facture      | Non Existante | Existante     |

WPshop 2 proposes uniquement la migration de **tier** ainsi que leurs **contacts**.

## Migration des tiers

Il est important de savoir que les **tier** dans WPshop sont des (Custom Post Types)[https://codex.wordpress.org/Post_Types]. La différence entre WPshop 1 et 2 est le nom du **post_type** ainsi que les noms des métadonnées.

Pour le post_type, nous l'avons renommé de **wpshop_customers** en **wps_customer**.

Faire seulement un changement de post_type permet de garder le même ID sur les tiers, et de ce fait, de garder **les mêmes éléments enfants associés** à celui-ci.

Pour les métadonnées, veuillez voir les chapitres suivants.

### Les métadonnées

Techniquement, seulement quelques méta données sur le tier doit être ajoutées:

Les méta données suivantes sont les nouvelles de WPshop 2

* _contact_ids: Les ID des contacts attachés à ce tier
* _address: L'adresse du tier
* _zip: Le code postal du tier
* _town: La ville du tier
* _country: Le pays du tier

### Tableau de liaison des métadonnées

|            |  WPshop 1                                                            | WPshop 2       |
| ---------- | -------------------------------------------------------------------- | -------------- |
| Entitée v1 |                                                                      |                |
| Address    | Donnée **address** de la méta déserialisé \_wpshop_address_metadata  | \_address      |
| Address    | Donnée **postcode** de la méta déserialisé \_wpshop_address_metadata | \_postcode     |
| Address    | Donnée **city** de la méta déserialisé \_wpshop_address_metadata     | \_city         |
| Address    | Donnée **country** de la méta déserialisé \_wpshop_address_metadata  | \_country      |
| Tier       | Donnée **\_wpscrm_associated_user**                                  | \_contacts_ids |



## Migration des contacts

Une seul méta nous intèresse sur le contact:

Les méta données suivantes sont les nouvelles de WPshop 2

* _phone: Le numéro de téléphone du contact

Tableau de liaison
