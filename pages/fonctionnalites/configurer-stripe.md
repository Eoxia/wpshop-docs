# Configurer Stripe

Configuration de Stripe pour redirigé vos clients vers le site sécurisé Stripe pour payer sa commande.

## Prérequis

* Un compte Stripe activé
* Clé publique
* Clé secrète

## Comment récupérer la clé publique et secrète ?

Rendez vous sur https://dashboard.stripe.com/login, connectez vous à votre dashboard.
Dans le menu de gauche > Développeur > Clés API
Cocher "Environnement de test" si vous voulez faire des essaies de paiement, sinon décocher.

Dans le tableau "Clé standard" vous retrouver vos deux clés à utiliser pour la configuration au chapitre suivant.

![](https://github.com/Eoxia/wpshop-docs/blob/master/images/stripe-test-key.PNG)

## Configuration de Stripe

1. Aller dans: WPshop > Réglages > Moyen de paiement > Stripe > Configurer
2. Activer le paiement
3. Remplir le champ "Clé publique" avec la clé publique récupérée sur le dashboard de Stripe.
4. Remplir le champ "Clé secrète" avec la clé secrète récupérée sur le dashboard de Stripe.
5. Cocher la cache "Stripe Sandbox" si vous configurer un environnement de test.
6. Enregister vos modifications en cliquant sur "Save Changes"

![](https://github.com/Eoxia/wpshop-docs/blob/master/images/stripe.PNG)

## Ajout d'un crochet web

Pour avoir des informations sur la commande, comme le status si celle si 'est bien payé, il faut ajouter un crochet web sur votre compte Sripte qui vas permettre de communiquer à WPShop le status de la commande.

Dans stripe, cliquez sur "Developpeurs" dans le menu de gauche puis "Webhooks".

Enfin dans la section "Endpoints recevant les évènements de votre compte" cliquez sur "Ajouter un endpoint".

URL d'endpoint: <votre-wpshop.com/wp-json/wpshop/v2/wps_gateway_stripe/>
Description: Ce que vous voulez
Version: Votre version actuelle
Événements à envoyer: Cliquer sur "recevez tous les événements"

Puis "Ajouter un endpoint".

### Environnement de test

Pour mêttre en place un environnement de test, la procédure est similaire, mais selon se passe dans le menu "Environnement de test"
