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

### Le module WPshop dans dolibarr (Module non obligatoire)

[En savoir plus sur le module WPshop dans dolibarr](https://github.com/Eoxia/wpshop-docs/blob/master/pages/dolibarr/module-wpshop.md).

#### Installation de WP OAuth Server sur votre WordPress

**Cette extension est obligatoire pour utiliser le module WPshop dans dolibarr**

* Aller dans la page "Extensions" de votre back office WordPress: https://<votrewordpress.ext>/wp-admin
* Puis cliquer sur "Ajouter" en haut de la page
* Saisir "wp oauth server" dans le champ "Rechercher des extensions...".
* Lorsque l'extension apparaît, cliquer sur "Installer" puis patienter pour que le bouton "Activer" apparaîsse.
* Cliquer sur "Activer".

#### Configuration de WP OAuth Server

* Cliquer sur OAuth Server dans le menu du backoffice de Votre WordPress
* Cliquer sur "Add New Client"

Dans cette nouvelle page seule les champs à droite sont à remplir:

* Client Name: Le nom de l'application qui vas se connecter à WordPress, par exemple: dolibarr
* Redirect URI: https://<votredolibarr.ext>/custom/wpshop/wpshopindex.php
* Client Credential assigned User: Sélectionner un utilisateur ayant pour rôle "Administrateur" sur votre WordPress.
* Puis "Create Client".

Nous avons maintenant les informations **Client ID** et **Client Secret**, garder ses informations de coté, nous allons en avoir besoin pour configurer le module WPshop sur dolibarr.

Si vous voulez en savoir plus sur la configuration, rendez vous sur [la page de l'extension](https://fr.wordpress.org/plugins/oauth2-provider/).

#### Installation du module WPshop dans dolibarr

[Description du module WPshop pour dolibarr](https://github.com/Eoxia/wpshop-docs/blob/master/pages/dolibarr/module-wpshop.md)

* Télécharger le ZIP en cliquant [ici](https://github.com/Eoxia/wpshop/archive/2.0.0.zip).
* Dézipper et envoyer le dossier wpshop dans le répertoire /custom/.
* Activer le module dans le menu Modules/Applications en pied de page sur votre Dolibarr.
* Toujours sur la même page, cliquer sur "Configuration" sur le module WPshop.

Cliquer sur "Modifier" sur la page de configuration du module, nous avons maintenant 3 champs:

* WordPress URL: https://<votrewordpress.ext>
* OAuth2 Client ID: **L'ID client** récupéré depuis WordPress
* OAuth2 Client Secret: **Le Secret Client** récupéré depuis WordPress.
