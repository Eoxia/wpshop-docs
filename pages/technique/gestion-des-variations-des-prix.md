# Gestion des variations des prix


## Public API Key

La clé publique correspond à un user dolibarr avec seulement des droits de lecture au niveau des permissions.

Pour toute les requêtes effectuées, vous devez fournir le header DOLAPIKEY avec la valeur dolibarr_public_key present dans l'objet:

scriptParams.dolibarr_public_key

## Les routes:

### Pour récupérer les attributs d'un produit variable

{product_id} = L'ID du produit dans dolibarr.

GET {dolibarr_route}/api/index.php/wpshop/product/attribute?id={product_id}

Retournes par exemple:

```json
[
    {
        "id": "1",
        "ref": "EP_VC",
        "label": "Épaisseur verre clair",
        "values": [
            {
                "id": "3",
                "fk_product_attribute": "1",
                "ref": "E4",
                "value": "4",
                "entity": 1
            },
            {
                "id": "4",
                "fk_product_attribute": "1",
                "ref": "E6",
                "value": "6",
                "entity": 1
            },
            {
                "id": "5",
                "fk_product_attribute": "1",
                "ref": "E8",
                "value": "8",
                "entity": 1
            }
        ]
    },
    {
        "id": "3",
        "ref": "FCN_VC",
        "label": "Façonnage verre clair",
        "values": [
            {
                "id": "9",
                "fk_product_attribute": "3",
                "ref": "CHF_0.00_1.00",
                "value": "Chanfrein 0-1m²",
                "entity": 1
            },
            {
                "id": "10",
                "fk_product_attribute": "3",
                "ref": "POLI_0.00_1.00",
                "value": "Bords plats poli 0-1m²",
                "entity": 1
            }
        ]
    }
]
```

### Pour récupérer le produit enfant selon les attributs:

POST {dolibarr_url}api/index.php/wpshop/object/get/child

data post
```json
{
    "product_id": "{dolibarr_product_id}",
    "attributes_data": {
        "1": 5,
        "3": 10
    }
}
```

attributes_data est un tableau contenant en clé l'ID de l'attribut de dolibarr et en valeur l'ID de la valeur de l'attribut.

Par exemple selon le retour JSON de la route précédente:

```json
"attributes_data": {
    "1": 5,
    "3": 10
}
```

La clé 1 correspond à l'attribut EP_VC
La valeur 5 correspond à la valeur E8

La clé 3 correspond à l'attribut FCN_VC
La valeur 10 correspond à la valeur POLI_0.00_1.00

Cette exemple vas retourner:

```json
{
    "id": "6",
    "fk_product_parent": "1",
    "fk_product_child": "7",
    "variation_price": "100",
    "variation_price_percentage": "0",
    "variation_weight": "0",
    "entity": 1
}
```
