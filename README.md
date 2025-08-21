## Prérequis

- Accès FTP au serveur (FileZilla)
- Accès à la base de données MySQL
- Archive WordPress (.zip) à télécharger depuis [wordpress.org](https://fr.wordpress.org/download/)
- Informations de connexion fournies ci-dessous

## Informations de connexion

### FTP (FileZilla)

- **Hôte** : simplon-03.digisup.vm-plesk-01.drosalys.net
- **Utilisateur FTP** : simplon-03

### 1. Télécharger WordPress

- Rendez-vous sur [https://fr.wordpress.org/download/](https://fr.wordpress.org/download/)
- Téléchargez l'archive `.zip` de WordPress sur votre ordinateur.
- **Nom de la base** : admin_simplon-03
- **Utilisateur** : simplon-03

### 2. Se connecter au serveur avec FileZilla

- Ouvrez FileZilla.
- Saisissez les informations FTP :
  - **Hôte** : simplon-03.digisup.vm-plesk-01.drosalys.net
  - **Identifiant** : simplon-03
  - **Mot de passe** :
  <!-- x1a?odc6mdWbyD14R -->
  - **Port** : 21 (par défaut FTP)
- Cliquez sur "Connexion rapide".

![Connexion FileZilla](./Wordpress/procédure/image1.png)

---

### 3. Envoyer les fichiers WordPress sur le serveur

- Décompressez l'archive WordPress téléchargée.
- Dans FileZilla, naviguez dans la partie droite (serveur) jusqu'au dossier racine du sous-domaine `simplon-03.digisup.vm-plesk-01.drosalys.net` (souvent `httpdocs` ou `www`).
- Glissez-déposez tous les fichiers et dossiers de WordPress (contenu du dossier `wordpress`) dans ce dossier racine sur le serveur.
- Attendez la fin du transfert de tous les fichiers.

![Transfert fichiers WordPress](./Wordpress/procédure/image2.png)

- Téléchargez l'archive `.zip` de WordPress sur votre ordinateur.

### 4. Créer le fichier de configuration `wp-config.php`

- Sur le serveur, copiez le fichier `wp-config-sample.php` et renommez-le en `wp-config.php`.
- Éditez `wp-config.php` et renseignez les informations de la base de données :

```php
// ...
define( 'DB_NAME', 'admin_simplon-03' );
define( 'DB_USER', 'simplon-03' );

define( 'DB_HOST', 'localhost' );
// ...
```

- Enregistrez et uploadez le fichier modifié sur le serveur si besoin.
- Attendez la fin du transfert de tous les fichiers.

### 5. Lancer l'installation de WordPress

- Ouvrez votre navigateur et allez sur :
  [https://simplon-03.digisup.vm-plesk-01.drosalys.net/wp-admin/install.php?language=fr_FR](https://simplon-03.digisup.vm-plesk-01.drosalys.net/wp-admin/install.php?language=fr_FR)
- Suivez les instructions à l'écran :

![Écran de démarrage installation WordPress](./Wordpress/procédure/image3.png)

- Remplissez les informations de la base de données :

![Saisie infos base de données](./Wordpress/procédure/image4.png)

- Cliquez sur "Envoyer" puis suivez les instructions pour terminer l'installation.

![Succès installation WordPress](./Wordpress/procédure/image5.png)

---

# Procédure d'installation de WordPress sur le serveur via FileZilla


# Procédure de déploiement d'un projet Symfony sur le serveur via FileZilla

## Prérequis

- Accès FTP au serveur (FileZilla)
- Accès SSH si besoin (optionnel pour certaines commandes)
- Accès à la base de données MySQL
- Projet Symfony prêt à être déployé (dossier du projet sur votre ordinateur)
- Informations de connexion FTP (voir plus haut)

## Étapes détaillées

### 1. Préparer le projet Symfony en local

- Vérifiez que votre projet fonctionne en local.
- Supprimez les fichiers inutiles (node_modules, vendor, cache, etc. si vous souhaitez les réinstaller sur le serveur).
- Générez les assets si besoin (par exemple : `npm run build` ou `yarn build`).

### 2. Se connecter au serveur avec FileZilla

- Ouvrez FileZilla.
- Saisissez les informations FTP (voir section précédente).
- Naviguez dans la partie droite (serveur) jusqu'au dossier racine du sous-domaine ou du site (souvent `httpdocs` ou `www`).

![Connexion FileZilla](./Symfony/procedure/image7.png)

### 3. Envoyer les fichiers Symfony sur le serveur

- Glissez-déposez tous les fichiers et dossiers de votre projet Symfony (sauf les fichiers sensibles ou inutiles) dans le dossier racine du serveur.
- Attendez la fin du transfert de tous les fichiers.

![Transfert fichiers Symfony](./Symfony/procedure/image8.png)

### 4. Installer les dépendances sur le serveur

- Si vous avez accès SSH, connectez-vous au serveur.
- Placez-vous dans le dossier du projet Symfony.
- Exécutez la commande suivante pour installer les dépendances PHP :

```bash
composer install --no-dev --optimize-autoloader
```

![Installation des dépendances](./Symfony/procedure/image10.png)

### 5. Configurer les variables d'environnement

- Renommez le fichier `.env` en `.env.local` (ou créez-le).
- Renseignez les variables d'environnement nécessaires (base de données, mailer, etc.).

```env
APP_ENV=prod
APP_SECRET=VotreCléSecrète
DATABASE_URL="mysql://utilisateur:motdepasse@localhost:3306/nom_base"
```

### 6. Configurer les droits sur les dossiers

- Assurez-vous que les dossiers `var` et `public` (et leur contenu) sont accessibles en écriture par le serveur web.
- Exemple de commande SSH :

```bash
chmod -R 775 var public
```

### 7. Effectuer les migrations de la base de données

- Si votre projet utilise Doctrine, lancez les migrations :

```bash
php bin/console doctrine:migrations:migrate --no-interaction
```

### 8. Vérifier le bon fonctionnement du site

- Rendez-vous sur l'URL de votre site pour vérifier que tout fonctionne.

![Site Symfony en ligne](./Symfony/procedure/image11.png)

---

