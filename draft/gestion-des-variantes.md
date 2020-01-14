# Gestion des variantes


## Public API Key

La clé publique correspond tout simplement à un user dolibarr avec seulement des droits de lecture.

Pour toute les requêtes effectuer, vous devez fournir le header DOLAPIKEY avec la valeur dolibarr_public_key present dans l'objet:

scriptParams.dolibarr_public_key

## Les routes:

Pour récupérer les attributs d'un produit variable:

{product_id} = L'ID du produit dans dolibarr.

{dolibarr_route}/api/index.php/wpshop/product/attribute?id={product_id}

Retournes par exemple:

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

