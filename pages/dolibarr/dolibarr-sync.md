
# WPshop avec Dolibarr

**Ceci est la documentation utilisateur pour l'association et la synchronisation de données entre WPshop et Dolibarr.**

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

**Suivre la procédure pour créer un produit sur WPshop.**

Après la création du produit, la création et l'association du produit vers dolibarr se fait automatiquement.

*Voir le chapitre "Vérifier l'association et la synchronisation d'un produit*

### Nouveau produit depuis Dolibarr

Après la création d'un produit sur Dolibarr, la création et l'association du produit vers WPshop se fait automatiquement.

*Voir le chapitre "Vérifier l'association et la synchronisation d'un produit*

### Produit existant sur WPshop uniquement

Depuis l'interface du listing des produits, nous pouvons associer un produit déjà existant sur WPshop à un produit Dolibarr.

![](https://github.com/Eoxia/wpshop-docs/blob/master/images/wpshop-button-sync-product.png)

Pour ce faire, il faut cliquer sur le bouton d'association et de synchronisation puis sélectionner le produit Dolibarr que nous voulons associer à notre produit WPshop puis cliquer sur Synchroniser. Enfin, il faut choisir la version que nous voulons garder entre la version du produit sur WPshop et celle de Dolibarr.

**Voir l'interface de synchronisation** pour plus de détails.

*Voir le chapitre "Vérifier l'association et la synchronisation d'un produit*

### Produit existant sur Dolibarr uniquement

Nous ne pouvons associer un produit Dolibarr vers WPshop pour le moment.

Cependant, un bouton est disponible sur WPshop pour synchroniser toutes les données de Dolibarr vers WPshop. Celà permet de récupérer les produits existants dans Dolibarr vers WPshop.

Attention, celà synchronise toutes les données Dolibarr: produit, commande, facture...
Avant d'utiliser le bouton de "Synchronisation en masse", il est important de lire et comprendre ce chapitre "Préparer la synchronisation en masse"
Le bouton de "Synchronisation en masse" de toutes les donnnées se trouvent dans le Tableau de bord dans le menu WPshop.

![](https://github.com/Eoxia/wpshop-docs/blob/master/images/sync-button.png)

## Synchronisation

### Modification d'un produit depuis WPshop

### Modification d'un produit depuis Dolibarr

## Vérifier l'association et la synchronisation d'un produit

Dans le listing des produits sur WPshop, nous pouvons vérifier si le produit est bien associer et synchroniser grâce à deux informations:

![](https://github.com/Eoxia/wpshop-docs/blob/master/images/wpshop-sync-product.png)

* #Doli: 68 est l'ID du produit dans dolibarr.
* Le rond vert signifie que l'association et la synchronisation est bien effectué et à jour.

## Les status de synchronisation

* Vert: Synchroniser (Les deux produits contiennent les mêmes données)
* Orange: Désynchroniser (Les deux produits contiennents des données différentes)
* Rouge: Non associer et non synchroniser.

## Synchronisation en masse

La synchronisation en masse récupères **toutes les données de dolibarr** et écrase les données des entitées liée avec celle de WPshop. Si l'entité n'a pas de liaison avec WPshop, celle-ci est créé dans WPshop.

### Préparer la synchronisation

#### Données de base 

WPSHOP            DOLIBARR
Produit A    !=   Produit A
Produit B    !=   -
Produit C    !=   Produit C
-            !=   Produit D

#### Etape création

Cette étape consiste à créer tous les produits WPshop inexistants sur Dolibarr.

Produit A    !=   Produit A
Produit B    !=   Produit B
Produit C    !=   Produit C
-            !=   Produit D

#### Étape association

Cette étape consiste à associer les produits non associé entre eux depuis l'interface du listing des produits sur WPshop.

Produit A    =   Produit A
Produit B    =   Produit B
Produit C    =   Produit C
-           !=   Produit D

#### Étape synchronisation en masse

Cette étape consiste à cliquer sur le bouton "Synchronisation en masse" dans le menu Tableau de bord sur WPshop.

WPSHOP            DOLIBARR
Produit A    =    Produit A
Produit B    =    Produit B
Produit C    =    Produit C
Produit D    =    Produit D


