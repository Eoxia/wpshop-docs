# Installer Dolibarr

Dolibarr est un ERP open source permettant toute la gestion de votre infrastructure. Grâce à l'association entre WPshop et Dolibarr, nous assurons la conformité aux normes RGPD françaises.

## Téléchargement de Dolibarr

* [Télécharger Dolibarr](https://www.dolibarr.fr/telechargements)
* [Installer Dolibarr](https://wiki.dolibarr.org/index.php/Installation_-_Mise_%C3%A0_jour)

## Synchronisation WPshop & Dolibarr

Pour pouvoir associer les deux, nous allons devoir installer et configurer un module qui va servir de passerelle.

### Génération de la clé secrète WordPress

* Rendez-vous sur votre profil utilisateur dans l'administration de votre WordPress (https://<votrewordpress.ext/profile.php)
* Dans la section WPshopAPI, nous retrouvons le champ API Key. Cliquer sur l'icone: ![](https://github.com/Eoxia/wpshop-docs/blob/master/images/generate-api-key.PNG)
* Sauvegardez la clé apparaissant dans le champs

### Génération de la clé secrète Dolibarr

* Rendez vous dans l'administration de Dolibarr
* Cliquez sur le bouton "Super Admin" en haut à droite de l'application, puis sur "modifier".
* Cherchez le champ "Clé pour l'API" puis cliquer sur l'icone: ![](https://github.com/Eoxia/wpshop-docs/blob/master/images/generate-api-key-doli.PNG)
* Sauvegardez la clé apparaissant dans le champs

### Installation du module

* Télécharger le ZIP en cliquant [ici](https://github.com/Eoxia/doli-wpshop/archive/master.zip).
* Dézipper et envoyer le dossier wpshop dans le répertoire /custom/ de votre dossier Dolibarr.
* Activer le module dans le menu Modules/Applications en pied de page sur votre Dolibarr.

### Configuration du module

Toujours sur Dolibarr, cliquez sur "Modifier" sur la page de configuration du module :

* WordPress URL: <https://<votrewordpress.ext>
* WordPress sercret: La clé récupéré depuis **WordPress**

Du coté de WordPress, rendez-vous dans "WPshop -> Réglages" :

* Dolibarr URL: https://<votrewordpress.ext>
* Dolibarr sercret: La clé récupérée depuis **Dolibarr**

### Problèmes connues

#### Connexion WPshop vers Dolibarr ne fonctionne pas

Le problème vient généralement des serveurs NGINX.
Si vous vous connectez sur la rest API de dolibarr (a finir)

#### Connexion Dolibarr vers WPshop ne fonctionne pas

!Ce fonctionnement vas être changé très bientot!

Si vous rencontrez ce message, c'est que la connexion vers WPshop ne fonctionne pas.
![Connexion dolibarr échouée](https://github.com/Eoxia/wpshop-docs/blob/master/images/dolibarrconnexionfailed.png?raw=true)

Vous devez autoriser l'adresse IP de dolibarr depuis notre framework.

Connecter vous en FTP sur le serveur du WordPress contenant le WPshop puis aller dans wpshop/core/external/eo-framework/modules/wpeo-model/wpeo_model.config.json.

Dans l'entrée allowed_ip_for_unauthentified_access_rest ajouter l'adresse IP du serveur contenant le dolibarr.

```
"allowed_ip_for_unauthentified_access_rest": [
		"127.0.0.1",
		"::1",
    "ADDRESS_IP_DOLIBARR"
	]
```
  
  La connexion doit être effectif maintenant, si celà ne marche toujours pas, veuillez ouvrir une issue https://github.com/Eoxia/wpshop-docs/issues

