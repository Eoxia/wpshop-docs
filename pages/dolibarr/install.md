# Installer WPshop 2

## Télécharger et activer l'extension

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

## Utilisation avec Dolibarr

Pour utiliser Dolibarr avec WPshop veuillez vous rendre dans la page "Configurer" de le sous menu WPshop dans le back office.
Dans cette page deux champs sont obligatoires:
* Dolibarr URL: L'url de votre dolibarr https://<votredolibarr.ext>/
* Dolibarr Secret: Le token de sécurité.

### Comment récupérer le dolibarr secret

* Dans votre dolibarr, aller dans l'onglet Super Admin.
* Faites modifier.
* Cliquer sur la flèche à droite du champ "Clé pour l'API".
* Copier cette clé dans le champ Dolibarr Secret sur votre WordPress.

### Les modules et configurations obligatoires

Activer les modules de Dolibarr :
* Tiers
* Propositions commerciales
* Commandes client
* Factures et avoirs
* Produits
* API/Web Services (serveur REST)
* Paypal

Dans l'onglet Configuration -> Divers, ajouter une ligne avec, comme données :
Nom : PRODUCT_PRICE_UNIQ
Valeur : 1

### Installer le module WPshop dans dolibarr

(Description du module WPshop pour dolibarr)[https://github.com/Eoxia/wpshop-docs/blob/master/pages/dolibarr/module-wpshop.md]

* Télécharger le ZIP en cliquant (ici)[https://github.com/Eoxia/wpshop/archive/2.0.0.zip].
* Dézipper et envoyer le dossier wpshop dans le répertoire /custom/.
* Activer le module dans le menu Modules/Applications en pied de page sur votre Dolibarr.
* Toujours sur la même page, cliquer sur "Configuration" sur le module WPshop.
