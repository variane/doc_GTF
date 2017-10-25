# Installation des composants pré-requis et de GTF


## Installation des Pré-requis 
 
 ### Installation de FME 

Dans GTF, FME est en charge de l’exécution des projets.
Procéder en premier lieu à l'installation de FME pour que GTF puisse fonctionner et exécuter des traitements.
 

[Procédure d'installation de FME](http://documentation.veremes.net/public/fme/fme_guide_installation.pdf) 


 ### Installation du serveur https Apache 2.4 
 
GTF utilise le protocole sécurisé https qui assure le cryptage des échanges entre le Serveur d’Application Vitis et le poste client. Il est donc nécessaire d’installer une version spécifique du serveur http Apache compilé avec le module SSL.
 
[Procédure d’installation Apache 2.4 pour Windows](http://www.veremes.com/installation-apache-2-4-mod_ssl-windows)
 
### Installation de Postgresql

GTF utilise une base Postgresql pour stocker les informations sur les projets FME et les demandes de traitement ainsi que sur les utilisateurs et leurs droits. Si Postgresql est déjà installé sur votre poste, cette étape est facultative.
 
[Procédure d’installation Postgresql pour Windows](http://www.veremes.com/installation-postgresql-windows)
 
## Installation de GTF 

Editer le setup install.cmd (Windows) du répertoire 'installateur_gtf_application_web' contenu dans le répertoire de téléchargement des ressources, afin de définir les paramètres de votre installation.
Les variables à modifier pour l’installation sont :
 
| Variable |	Description |
|:-------|:-----------|
| dir | Répertoire d'installation (si le répertoire n'existe pas, il sera créé) |
| serveur	|Serveur de la base de données |
|port	|Port d'accès à la base de données|
|bdd	|Nom de la base de données (La base de données peut être existante)|
|dblogin	|Compte d'un super utilisateur de la base|
|dbpswd	|Mot de passe du compte super utilisateur|
|apacheService	|Nom du service Apache exploité par l'application|
|apachePort	|Port du service https du serveur Apache|
|appAdmin	|Compte PostgreSql de l'administrateur GTF. Ce compte sera créé s'il n'existe pas.|
|appPswd 	|Mot de passe du compte précédent s'il doit être créé. Si le compte existe déjà, cette valeur n'est pas exploitée mais la présence d'une valeur est obligatoire.| 




 
L’installateur assure les opérations suivantes :

- Copie du code du Serveur d’Application Vitis
- Installation du PHP
- Configuration du serveur HTTPS Apache
- Création de la base de données dans PostgreSql
- Création d’un compte administrateur dans PostgreSql
 
Exécuter le script install.cmd pour lancer l’installation.
 
 ![](../images/attention.png) Attendre une minute environ pour obtenir un retour console.
 
Un rapport d’installation install_report_dd-mm-yyyy.txt est généré dans le répertoire de téléchargement des ressources, il permet de savoir si l’installation s’est déroulée correctement.
 
 
 ## Test de l'installation de GTF 
 
L' instance de GTF doit désormais être disponible à l’adresse : https://<serveur>/gtf
Où <serveur> est l’adresse de la machine où l’application est installée. 
 
  ![](../images/attention.png)Attention ! La connexion à GTF par l’adresse localhost est impossible.
 
  ![](../images/attention.png)Si l'on se connecte avec le protocole http, la connexion est automatiquement redirigée vers https.
 
  ![](../images/attention.png)Si vous avez généré un certificat de type "self signer", le serveur n’est pas sécurisé et le navigateur va afficher un message d’alerte. Créer alors une exception de sécurité afin de pouvoir accéder et se connecter à GTF. 
 
 
Après exécution de l’installateur, il faut procéder à l’initialisation de l’application, c’est-à- dire à : 

-	l'initialisation du compte administrateur de GTF
-	l’installation du moteur GTF
 


