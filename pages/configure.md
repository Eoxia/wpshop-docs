# Configurer WPshop

Sur cette page, nous allons parler de toutes les configurations disponibles sur votre WPshop. Nous retrouverons des configurations telles que la connexion avec Dolibarr, les pages de votre boutique, les emails, les méthodes de paiement et les frais de livraison.

## Général

* **Dolibarr URL & Dolibarr Secret** permet la connexion vers votre ERP Dolibarr pour gérer la synchronisation automatique des données.
* **Email de la boutique** contient votre adresse email de votre boutique WPshop. Tous les mails entrant/sortant reliée à WPshop telles que "Une nouvelle commande dans votre boutique", "Nouveau client inscrit dans votre boutique", "Commande complétée" sont traités par cette adresse email. 
* **Taille miniature largeur & Taille miniature hauteur** permet de gérer la taille des images gérées par WPshop.

## Pages

WPShop doit connaître les pages pour envoyer les utilisateurs selon les actions effecutées par celui-ci:

* **Boutique**: cette page affiches les produits de la boutique.
* **Panier**: cette page affiches les produits dans le panier du client.
* **Tunnel de vente**: cette page permet l'utilisateur de passer sa commande.
* **Mon compte**: cette page permet à l'utilisateur connecté de voir ses commandes, devis, factures et produits téléchargables.
* **Validation**: cette page permet l'affichage de la validation d'une commande ou d'un devis.
* **Condition générales de vente**: cette page permet de visualiser les conditions générales de vente.

Chaque élément ci-dessus sont accompagnés d'une liste déroulante qui liste toutes vos pages WordPress. Vous pouvez très bien choisir une page différente de celle par défaut.

A savoir: WPshop créer des pages par défaut pour chaque élément cité ci-dessus lors de la première activation du plugin.

## Emails

### Tableau des mails disponibles

Dans cette interface, nous retrouvons un tableau regroupant tous les emails disponibles dans WPshop par défaut.

### Modifier un modèle d'email

En cliquant sur "Gérer" nous pouvons modifier le contenu d'un mail par défaut.

Le contenu du mail est géré dans un fichier, tous ces fichiers "modèle" sont disponibles dans /wpshop/modules/emails/view/.

Par défault le contenu du mail est vérrouillé. Nous devons créer notre propre modèle pour pouvoir en modifier son contenu.

Nous avons deux méthodes pour créer notre propre modèle afin de modifier le modèle par défaut:

#### Méthode 1 

Prenons le cas de "Nouvelle commande payée", le fichier qui nous intéresse est "/wpshop/modules/emails/view/admin-new-order.php", nous allons le copier et le coller dans notre thème "/mon-theme/wpshop/emails/admin-new-order.php.

#### Méthode 2

Cliquer sur le bouton "Copié le modèle".

### Modifier le contenu du mail

Une fois le contenu "déverouiller", nous pouvons modifier son contenant puis cliquer sur "Enregister les modifications".

## Moyen de paiement

### Tableau des méthodes de paiement disponibles

Dans cette interface, nous retrouvons un tableau regroupant toutes les méthodes de paiement disponibles dans WPshop par défaut.

#### Modifier une méthode de paiement

En cliquant sur "Configurer" nous arrivons sur une nouvelle interface qui contient un formulaire. Pour chaque méthode de paiement l'interface est similaire, nous retrouvons:

* Le titre
* L'état
* La description

Cliquer sur "Enregistrer les modifications" pour valider vos modifications.

#### Configurer PayPal

[Cliquer ici pour avoir plus de détails sur la mise en place de PayPal](https://github.com)

Ce formulaire est similaire que l'interface "Modifier une méthode de paiement" avec 2 champs supplémentaires:

* Email PayPal
* PayPal Sandbox

Cliquer sur "Enregistrer les modifications" pour valider vos modifications.

#### Configurer Stripe

[Cliquer ici pour avoir plus de détails sur la mise en place de Stripe](https://github.com)

Ce formulaire est similaire que l'interface "Modifier une méthode de paiement" avec 3 champs supplémentaires:

* Clé publique
* Clé secrète
* Stripe Sandbox

Cliquer sur "Enregistrer les modifications" pour valider vos modifications.

## Frais de livraison
