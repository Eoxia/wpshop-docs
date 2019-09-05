# Installer WPshop 2 & Commencer à vendre

## Installer WPshop 2

### Méthode 1: Par la page Extensions de votre back office WordPress (Méthode indisponible pour le moment)

* Aller dans la page "Extensions" de votre back office WordPress: https://<votrewordpress.ext>/wp-admin
* Puis cliquer sur "Ajouter" en haut de la page
* Saisir "wpshop" dans le champ "Rechercher des extensions...".
* Lorsque l'extension apparaît, cliquer sur "Installer" puis patienter pour que le bouton Activer apparaîsse.
* Cliquer sur "Activer".

### Méthode 2: En téléchargeant le ZIP

* Télécharger le ZIP en cliquant [ici](https://github.com/Eoxia/wpshop/archive/2.0.0.zip).
* Dézipper et envoyer le dossier wpshop dans le répertoire /wp-content/plugins/
* Activer le plugin dans le menu Extensions de votre back office WordPress.

## Commencer à vendre

Avant de pouvoir vendre vos produits, vous devez configurer votre boutique en ligne.

Pour ce faire rendons nous dans l'administration.

Les éléments obligatoires pour le bon fonctionnement sont les suivants:

* Ajouter les pages de WPshop dans un menu WordPress:
  * Boutique
  * Panier
  * Mon compte

* Créer des produits ([Comment créer des produits ?](https://github.com/Eoxia/wpshop-docs/blob/master/pages/product.md))

## Tester votre boutique

* Rendez vous sur votre boutique puis sur la page "Boutique"
* Ajouter un ou plusieurs produits dans le panier
* Rendez vous dans la page "Panier"
* Cliquer sur "Procéder au paiement"
* Remplissez vos informations personnelles et d'expédition
* Choisisez votre Moyen de paiement (Par défaut: Chèque ou Paiement en boutique. [Comment configurer les méthodes de paiement](https://github.com/Eoxia/wpshop-docs/blob/master/pages/configure.md))
* Cocher la case "J'accepte les conditions générales de vente et la politique de confidentialité".
* Cliquer sur "Demander un devis".

Avec les éléments ci-dessus, vos clients ont la possibilités de faire des demandes de devis selon leur panier.

Seulement des devis ? Comment faire pour que le client puisse payer directement sur ma boutique en ligne ? 
Très bonne question, nous allons voir comment accepter des paiements directement depuis votre boutique en ligne dans le chapitre suivant grâce à Dolibarr.

## La fusion avec Dolibarr

Nous utilisons Dolibarr pour contrôller les données telle que les commandes, factures.
Dolibarr permet d'assurer que votre boutique en ligne est conforme au norme RGPD.

Rendez vous sur [cette page](https://www.dolibarr.fr/) pour installer dolibarr.

Une fois l'installation effectué, nous allons devoir ajouter un module à Dolibarr afin de gérer la synchronisation automatique des données entre les deux plateformes respectives: WordPress et Dolibarr.

Pour effectuer cette synchronisation nous avons besoin de "token", ce sont des sortes de code secret permettant aux plateformes d'autoriser la communication entre elles.

### Générer le token sur WordPress

* Rendez vous dans l'administration de WordPress
* Aller sur votre profil utilisateur (https://<votrewordpress.ext/profile.php)
* Dans la section WPshopAPI nous retrouvons le champ API Key.
* Cliquer sur l'icone: ![](https://github.com/Eoxia/wpshop-docs/blob/master/images/generate-api-key.PNG)
* Le token apparaît dans le champ vide auparavant.

### Générer le token sur Dolibarr

* Rendez vous dans l'administration de Dolibarr
* Cliquez sur le bouton "Super Admin" tout en au à droite de l'application
* Puis le bouton "Modifier"
* Cherchez le champ "Clé pour l'API" puis cliquer sur l'icone: ![](https://github.com/Eoxia/wpshop-docs/blob/master/images/generate-api-key-doli.PNG)
* Le token apparaît dans le champ vide auparavant.

### Installation du module WPshop pour Dolibarr

[Description du module WPshop pour dolibarr](https://github.com/Eoxia/wpshop-docs/blob/master/pages/dolibarr/module-wpshop.md)

Télécharger le ZIP en cliquant [ici](https://github.com/Eoxia/doli-wpshop/archive/master.zip).
* Dézipper et envoyer le dossier wpshop dans le répertoire /custom/.	
* Activer le module dans le menu Modules/Applications en pied de page sur votre Dolibarr.	
* Toujours sur la même page, cliquer sur "Configuration" sur le module WPshop.

### Configuration des tokens

Maintenant nous allons pouvoir configurer les deux plateformes afin qu'il communique entre eux

Toujours sur Dolibarr, cliquer sur "Modifier" sur la page de configuration du module, nous avons maintenant 3 champs:

* WordPress URL: <https://<votrewordpress.ext>
* WordPress sercret: **Le token** récupéré depuis WordPress

Du coté de WPshop, rendez vous dans "WPshop -> Réglages" puis completer les 2 champs suivants:

* Dolibarr URL: https://<votrewordpress.ext>
* Dolibarr sercret: **Le token** récupéré depuis Dolibarr

## Votre boutique est fonctionnelle!

A partir de ce point, votre boutique est 100% fonctionelles:

Vos clients peuvent:

* Faire des demandes de devis
* Passer des commandes
* Visualiser leur facture

Pour completer votre boutique vous pouvez:

* [Voir les réglages avancées comme: "Ajouter des méthodes de paiement comme PayPal, Stripe"](https://github.com/Eoxia/wpshop-docs/blob/master/pages/configure.md)
* [Gérer vos produits](https://github.com/Eoxia/wpshop-docs/blob/master/pages/product.md)
* [Gérer vos commandes](https://github.com/Eoxia/wpshop-docs/blob/master/pages/order.md)
* [Gérer vos clients](https://github.com/Eoxia/wpshop-docs/blob/master/pages/third-party.md)
* [Visualiser votre tableau de bord](https://github.com/Eoxia/wpshop-docs/blob/master/pages/dashboard.md)
* [Apprendre à maitriser la puissance de Dolibarr](https://wiki.dolibarr.org/index.php/Documentation_utilisateur)
