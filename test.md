


Bienvenue dans GTF

GTF (Gestionnaire de Tâches pour FME) est une application 100% web qui permet de publier sur internet des traitements conçus avec FME et de les mettre à disposition d&#39;un grand nombre d&#39;utilisateurs. C&#39;est un outil de partage, de planification et de supervision de traitements FME.

GTF offre des fonctions d&#39;administration pour la création et la gestion des utilisateurs et l&#39;attribution des droits sur les traitements.

GTF est particulièrement bien adapté pour répondre à des besoins de :

- . conversion de fichiers
- .extraction de données
- .contrôle qualité
- .génération de rapport
- .gestion d&#39;alertes

GTF se compose d&#39;une application cliente, d&#39;une API REST qui permet d&#39;exploiter GTF sous forme de service web et d&#39;une API Formulaire :

- .GTF Client permet à l&#39;administrateur de publier des traitements préalablement conçus avec FME Workbench. Par cette interface, l&#39;administrateur gère les utilisateurs en leur attribuant des droits sur les traitements publiés, et peut également  s&#39;appuyer sur un annuaire MS-Active Directory pour assurer l&#39;authentification et la gestion des droits. Il dispose par ailleurs de fonctions de supervision et de consultation de statistiques. Les utilisateurs soumettent des demandes de traitements, chargent leurs propres données et téléchargent les résultats. Les traitements sont exécutés en mode asynchrone ce qui permet aux utilisateurs de continuer à travailler sans attendre la fin du traitement. Un e-mail avertit l&#39;utilisateur de la disponibilité du résultat. GTF Client permet également  de s&#39;abonner à un traitement à la fréquence souhaitée pour automatiser la production d&#39;un traitement.

- .L&#39;API REST de GTF permet à n&#39;importe quelle application de faire appel aux services de GTF de manière transparente pour les utilisateurs. C&#39;est la solution idéale pour les développeurs souhaitant offrir leur propre interface graphique.

- .L&#39;API Formulaire permet de mettre en forme le formulaire de saisie des paramètres en intégrant des composants (cartes open layer, arborescences de fichiers…)

  Les composants logiciels de GTF

L&#39;architecture de GTF est constituée de plusieurs composants logiciels.

| Composants | Description |
| --- | --- |
| GTF Client | Applications web  permettant aux utilisateurs l&#39;accès aux services GTF |
| Apache HTTPD | Logiciel serveur HTTP. |
| PHP | Langage de programmation |
| PostgreSQL | Système de gestion de base de données relationnelle utilisé pour le stockage des informations : demandes de traitements, traitements publiés, droits des utilisateurs...   |
| PYCRON | Service Windows assurant l&#39;exécution de tâches planifiées. |
| GTF Engine | GTF Engine désigne le moteur de GTF, la partie logicielle capable d&#39;exécuter les traitements FME. GTF exploite au minimum un moteur GTF. Les moteurs supplémentaires permettent de répartir la charge sur plusieurs process ou machines. L&#39;ajout de moteurs supplémentaires et soumis à l&#39;acquisition des licences correspondantes.  |
| FME | Logiciel FME Professional Edition ou supérieure en licence fixe ou flottante. FME ne fait pas partie du logiciel GTF, mais il est indispensable à son fonctionnement. |

 ![](./)

 Installation de GTF

Pour installer GTF, il faut télécharger l&#39;installateur sur le site [http://download.veremes.com](http://download.veremes.com/), dans le répertoire gtf/gtf2016.

Les codes d&#39;accès (login et password) sont fournis par e-mail à la suite d&#39;une commande ou demande d&#39;évaluation. Ces informations peuvent être renvoyées sur simple demande à codes@veremes.com.

L&#39;installateur comporte :

• Installateur \_gtf\_application\_web, exécutable et scripts d&#39;installation, de mise à jour et de suppression de GTF.

• Moteur\_gf.zip, archive d&#39;installation du module GTF

• Pycron-0.5.9.0.exe, installateur de Pycron

• Procedure\_installation\_gtf\_windows.pdf, la présente documentation.

Après téléchargement de l&#39;installateur, décompresser l&#39;intégralité de ces ressources dans un répertoire spécifique. Nous préconisons de nommer ce répertoire &#39;gtf\_telechargement&#39;.

Le processus d&#39;installation de GTF se déroule en 3 étapes :

- .Installation des composants pré requis et de GTF
- .Initialisation du compte administrateur de GTF
- .Installation du Moteur GTF

 Installation des composants pré-requis et de GTF

 Installation des Pré-requis

 Installation de FME

Dans GTF, FME est en charge de l&#39;exécution des projets.

Procéder en premier lieu à l&#39;installation de FME pour que GTF puisse fonctionner et exécuter des traitements.

[Procédure d&#39;installation de FME.](http://documentation.veremes.net/public/fme/fme_guide_installation.pdf)

 Installation du serveur https Apache 2.4

GTF utilise le protocole sécurisé https qui assure le cryptage des échanges entre le Serveur d&#39;Application Vitis et le poste client. Il est donc nécessaire d&#39;installer une version spécifique du serveur http Apache compilé avec le module SSL.

[Procédure d&#39;installation Apache 2.4 pour Windows](http://www.veremes.com/installation-apache-2-4-mod_ssl-windows)

 Installation de Postgresql

GTF utilise une base Postgresql pour stocker les informations sur les projets FME et les demandes de traitement ainsi que sur les utilisateurs et leurs droits. Si Postgresql est déjà installé sur votre poste, cette étape est facultative.

[Procédure d&#39;installation Postgresql pour Windows](http://www.veremes.com/installation-postgresql-windows)

Installation de GTF

Editer le setup install.cmd (Windows) du répertoire &#39;installateur\_gtf\_application\_web&#39; contenu dans le répertoire de téléchargement des ressources, afin de définir les paramètres de votre installation.

Les variables à modifier pour l&#39;installation sont :

| Variable | Description |
| --- | --- |
| dir | Répertoire d&#39;installation (si le répertoire n&#39;existe pas, il sera créé) |
| serveur | Serveur de la base de données |
| port | Port d&#39;accès à la base de données |
| bdd | Nom de la base de données (La base de données peut être existante) |
| dblogin | Compte d&#39;un super utilisateur de la base |
| dbpswd | Mot de passe du compte super utilisateur |
| apacheService | Nom du service Apache exploité par l&#39;application |
| apachePort | Port du service https du serveur Apache |
| appAdmin | Compte PostgreSql de l&#39;administrateur GTF. Ce compte sera créé s&#39;il n&#39;existe pas. |
| appPswd | Mot de passe du compte précédent s&#39;il doit être créé. Si le compte existe déjà, cette valeur n&#39;est pas exploitée mais la présence d&#39;une valeur est obligatoire. |

L&#39;installateur assure les opérations suivantes :

- .Copie du code du Serveur d&#39;Application Vitis
- .Installation du PHP
- .Configuration du serveur HTTPS Apache
- .Création de la base de données dans PostgreSql
- .Création d&#39;un compte administrateur dans PostgreSql

Exécuter le script install.cmd pour lancer l&#39;installation.

 ![](./)
_Attendre une minute environ pour obtenir un retour console._



Un rapport d&#39;installation install\_report\_dd-mm-yyyy.txt est généré dans le répertoire de téléchargement des ressources, il permet de savoir si l&#39;installation s&#39;est déroulée correctement.



 Test de l&#39;installation de GTF

L&#39; instance de GTF doit désormais être disponible à l&#39;adresse : https://&lt;serveur&gt;/gtf

Où &lt;serveur&gt; est l&#39;adresse de la machine où l&#39;application est installée.

 ![](./)
Attention ! La connexion à GTF par l&#39;adresse localhost est impossible.



 ![](./)



 ![](./)
Si vous avez généré un certificat de type &quot;self signer&quot;, le serveur n&#39;est pas sécurisé et le navigateur va afficher un message d&#39;alerte. Créer alors une exception de sécurité afin de pouvoir accéder et se connecter à GTF.



Après exécution de l&#39;installateur, il faut procéder à l&#39;initialisation de l&#39;application, c&#39;est-à- dire à :

- . [l&#39;initialisation du compte administrateur de GTF](../../C:/margot2/svn/produit/gtf/doc/gtf_manuel_utilisateur/Content/gtf_manuel_utilisateur/3.2%20Initialisation%20du%20compte%20Administrateur.htm#4)
- .l&#39;installation du moteur GTF

Initialisation du compte Administrateur

Configuration du compte administrateur

Le compte administrateur, défini en phase d&#39;installation par la variable &#39;appAdmin&#39;, dispose initialement des privilèges vitis\_user et vitis \_admin.

La configuration du compte administrateur permet l&#39;attribution des privilèges d&#39;administration spécifiques à GTF, c&#39;est à dire gtf\_admin :

• Se connecter à GTF avec le compte administrateur

• Mode Utilisateurs &gt; onglet Utilisateur, éditer le compte administrateur et lui attribuer les privilèges gtf\_admin. Attribuer à l&#39;administrateur les autres privileges gtf\_author et gtf\_user.

• Associer le compte courant au groupe Administration

• Mettre à jour

• Se déconnecter

 ![](./)

Attribution de privilèges gtf\_admin

En savoir plus sur les privilèges

 Test de Connexion du compte administrateur

A ce stade de l&#39;initialisation, le compte administrateur peut se connecter à GTF ( https://&lt;serveur&gt;/gtf) et accéder à l&#39;intégralité des 10 modes de l&#39;application.

Les 10 modes sont correctement affichés dans la barre de gauche :

 ![](./)

Interface Administrateur de GTF



Le compte administrateur peut procéder à une demande de traitement. Cette dernière restera en attente et ne sera pas exécutée.

 ![](./)
3 traitements sont intégrés dans GTF : Admin-Import, Admin-export et Vérification des formulaires.



Après avoir configuré le compte administrateur, procéder à l&#39;installation du moteur GTF.



Installation du moteur GTF

L&#39;installation du moteur GTF se décline en 5 étapes :

- .Installation de Pycron
- .Installation du moteur GTF
- .Configuration du moteur GTF
- .Configuration du serveur SMTP
- .Activation de la licence

 Installation de Pycron

Pycron est le programme qui permet aux utilisateurs de systèmes Windows d&#39;exécuter automatiquement des scripts, des commandes ou des logiciels à une date et une heure spécifiées à l&#39;avance. Dans GTF, il permet l&#39;exécution des demandes GTF aux dates et heures spécifiées.

[Procédure d&#39;installation de Pycron.](http://documentation.veremes.net/public/ressource/pycron_guide_installation.pdf#http://documentation.veremes.net/public/ressource/pycron_guide_installation.pdf)

Configuration de Pycron

• Démarrer le service de Pyrcon

Démarrer le service de pycron en ligne de commande :

sc start PyCron

 Test de l&#39;installation de Pycron

Exécuter la commande suivante pour accéder à la liste des services de Windows : services.msc

Rechercher dans la liste des services disponibles, le service Pycron (Python Cron Service).

Vérifier que le service soit démarré et que le type de démarrage soit en mode Automatique.

 Déclaration du serveur Pyrcon dans GTF

Dans GTF, indiquer le répertoire d&#39;installation du Pycron dans le Mode Configuration&gt; Configuration GTF&gt; Répertoire de pycron.

 ![](./)
**Test** : Cette opération rajoute un répertoire &#39;Log&#39; dans la fenêtre d&#39;affichage des journaux du Mode Log.

 Installation du Moteur

Décompresser l&#39;archive moteur\_gtf.zip, dans le répertoire d&#39;installation au même niveau que les répertoires client et vas.

 ![](./)
_Lors de la décompression de l&#39;archive gtf.engines, l&#39;administrateur doit penser à modifier manuellement le fichier de configuration de la base de données PostgreSQL pour autoriser la connexion de l&#39;utilisateur scheduler à la base de données créée lors de l&#39;installation de GTF. Dans le répertoire d&#39;installation de PostgreSQL (répertoire data),  modifier à l&#39;aide d&#39;un éditeur de texte le fichier pg\_hba.conf en y insérant les lignes suivantes pour les deux connexions IPv4 et IPv6._



Immédiatement après « # IPv4 local connections » insérer la ligne :

host &lt;base de donnnées&gt; u\_scheduler 127.0.0.1/32 trust

Immédiatement après « # IPv6 local connections » insérer la ligne :

host&lt;base de donnnées&gt; u\_scheduler ::1/128 trust

où&lt;base de donnnées&gt; est le nom de la base de données créée en phase d&#39;installation. (vitis par défaut)

Redémarrer le service PostgreSQL.

Configuration du moteur GTF

Déclaration du serveur

La déclaration du serveur permet de définir les répertoires contenant l&#39;ordonnanceur Pycron et le moteur GTF.

• Mode Moteur &gt; Onglet Serveur : Ajouter un serveur

• Nommer le serveur

• Définir le répertoire d&#39;installation de Pycron.

• Définir le répertoire contenant le moteur GTF gtf.engines

• Cliquer sur Créer

 ![](./)

Déclaration de serveur.

Déclaration d&#39;un moteur FME

Un moteur FME est l&#39;instance de FME en charge de l&#39;exécution des projets. GTF permet d&#39;exploiter différents moteurs hétérogènes. On peut ainsi exploiter un moteur FME 2015 en 32 bits et une instance de FME 2016 en 64 bits.

La première étape consiste à déclarer un moteur FME exploitable par GTF.

• Mode Moteurs &gt; Onglet Moteur FME : Ajouter un moteur FME

• Nommer le moteur et indiquer le chemin du moteur fme.exe.

• Associer le serveur désiré

• Cliquer sur Créer

 ![](./)

Déclaration de moteur FME.

 ![](./)
Il est conseillé de nommer le moteur FME en indiquant le numéro de version, le numéro de build et le nombre de bits. Par exemple : « FME2016 b16494-32b ».

  ![](./)
Le bouton &#39;Test&#39; permet de vérifier la validité de la licence FME. Avec FME 2016, pour que la licence soit valide, copier le fichier de licence présent dans le répertoire C:\ProgramData\SafeSoftware\FME\Licenses) dans le répertoire \licenses du répertoire d&#39;installation de FME2016.



Déclaration de moteur GTF

On entend par Moteur GTF la capacité d&#39;exploiter un moteur FME dans GTF. La création d&#39;un moteur GTF permet d&#39;associer à un serveur un moteur et de définir une période de déclenchement de l&#39;activité spécifique. Un moteur GTF est associé à un seul moteur FME mais plusieurs moteurs GTF peuvent exploiter le même moteur FME.

L&#39;ajout de moteurs GTF supplémentaires permet à l&#39;administrateur d&#39;appliquer une stratégie de traitement de projets en spécialisant par exemple certains moteurs et en permettant la parallélisation des traitements.

Dans le mode Moteurs &gt; Onglet Moteur GTF, le bouton « Ajouter un moteur GTF » ouvre le formulaire de création  de moteur GTF.

Attribuer un nom au moteur GTF et définir la période d&#39;activité en minutes de ce dernier (période de déclenchement du moteur). On peut choisir de rendre inactif ce moteur, puis on sélectionne le serveur et le moteur FME à associer. Associer ensuite un ou plusieurs mots clés au moteur.

 ![](./)

L&#39;administrateur peut choisir des mots clés existants et déjà affiliés à d&#39;autres moteurs dans la partie de gauche &#39;Mots clés disponibles&#39;, ou saisir directement le nom d&#39;un nouveau mot clé dans le bloc de droite &#39;Mot clé lié au moteur&#39;. Un simple clic sur un mot clé disponible permet de le lier au moteur GTF.

 ![](./)
Il est recommandé de nommer le moteur GTF selon cette règle : ID (auto)\_ FME Version Service Pack. Par exemple : «  #3 FME 2013 SP 3 ».



 ![](./)

Déclaration de moteur GTF.

Cliquer ensuite sur le bouton &#39;Créer&#39; pour finaliser la création du moteur GTF

Configuration du serveur SMTP

La phase de configuration du serveur SMTP est nécessaire à ce stade de l&#39;initialisation, pour que l&#39;administrateur puisse demander le fichier de licence GTF en envoyant un mail au service administratif de Veremes.

Dans le mode Configuration,configuration GTF, la section serveur SMTP permet de procéder à la déclaration du serveur SMTP.

Activation du fichier de licence GTF

L&#39;installation du fichier de licence GTF est la dernière étape du processus d&#39;initialisation de GTF.

Dans le mode Configuration, la section Licence permet de demander un fichier de licence nécessaire pour activer les licences permanentes.

Le bouton « Demande de fichier de licence » permet d&#39;envoyer au service administratif de Veremes une demande de génération de fichier de licence. Indiquer le numéro de licence fourni dans l&#39;accusé de réception de votre commande, ainsi que l&#39;adresse mail à laquelle le fichier doit être envoyé.

Une fois obtenu,  indiquer l&#39;emplacement du fichier de licence délivré par Veremes dans le champ &#39;Fichier .txt&#39;, puis cliquer sur « Activer ».

Tests : Import de nouveaux traitements

A ce stade, pour s&#39;assurer du bon fonctionnement de GTF, il est recommandé de procéder à l&#39;import de nouveaux traitements. Pour cela, Veremes met à disposition sur son site de téléchargement des projets exemples au format .gex.

Le projet &#39;Admin\_Import&#39; (associé au groupe Administration et installé automatiquement lors de l&#39;installation de GTF) permet l&#39;import de nouveaux traitements stockés dans un fichier .gex. Au préalable, l&#39;administrateur doit être associé au groupe Administration pour pouvoir exploiter ces deux projets.

Télécharger le fichier «exemples.gex»  sur notre site de téléchargement. [http://download.veremes.com](http://download.veremes.com/) (répertoire gtf/gex)

Se connecter à GTF (compte administrateur) puis ajouter une demande.

 ![](./)

Import du fichier d&#39;exemples.

Choisir le traitement &quot;Admin-Import&quot; puis dans « Fichier d&#39;export GTF à importer (.gex) : », cliquer sur « Parcourir » et sélectionner le fichier exemples.gex préalablement téléchargé. Définir ensuite le nom du rapport html à générer. Il indique la liste des projets importés, leurs clé et ID ainsi que le statut de l&#39;importation : Inséré dans GTF, Mis à jour dans GTF ou Non mis à jour dans GTF.

 ![](./)
_Il est obligatoire d&#39;insérer l&#39;extension .html dans le champs Nom du rapport à générer._

 ![](./)
_Le paramètre &quot;Que faire des projets existants déjà dans la base GTF (même Clé)&quot; indique à GTF s&#39;il doit charger ou pas les projets déjà existants dans la base GTF et identifiés de façon unique  par l&#39;attribut Clé (cet attribut est généré automatiquement et est associé de façon unique à chaque projet)._

- _._Si ce paramètre vaut &#39;Ne pas importer&#39; et que le fichier .gex contient un projet FME avec une clé déjà existante dans la base GTF, alors le fichier n&#39;est pas chargé.
- _._Inversement, si ce paramètre vaut &#39;Remplacer les projets existants&#39;, alors les projets dont la clé existe déjà dans la base de données GTF seront écrasés.
- _._Choisir &#39;Importer le projet avec un nouvel identifiant et un nouveau nom&#39;, si le projet FME avec la même clé existe déjà en base et que vous souhaitez importer le même projet mais avec un nouveau nom. Le projet est renommé en étant suffixé par la chaîne &quot;(import date de l&#39;import)&quot;.



Cliquer  sur « Créer la demande ». La demande est prise en compte et se retrouve dans la file d&#39;attente du moteur GTF.

S&#39;assurer que la Demande ait bien été traitée en consultant le mode Supervision, puis retourner dans le mode Publication pour consulter la liste des traitements nouvellement importés.

 ![](./)

3 nouveaux traitements sont désormais disponibles dans GTF.



Import des traitements d&#39;administration

Le projet &#39;Nettoyage des fichiers temporaires&#39; est disponible sur notre site de téléchargement, via le projet admin.gex. Il permet les fonctions d&#39;administration suivantes :

- .le nettoyage des fichiers temporaires stockés dans les répertoires temporaires de GTF et FME.

Pour importer ce fichier, procéder de la même manière que précédemment en téléchargeant sur le site [http://download.veremes.com](http://download.veremes.com/) (répertoire gtf/gex) le fichier admin.gex.

Se connecter ensuite à GTF et faire une demande du Traitement Admin-Import. Choisir le fichier admin.gex précédemment téléchargé.

Assurez-vous que dans le mode Publication,  ce nouveau traitement ait bien été importé :









Une fois le module GTF installé, l&#39;administrateur peut procéder à la configuration spécifique de GTF en en définissant le compte public, et mettant en place une stratégie de sécurité utilisateur.

Il créé ensuite les utilisateurs et/ou les importe depuis un annuaire Active Directory.



 Gestion des utilisateurs

Un utilisateur GTF est un compte connu par l&#39;application GTF qui peut se connecter à GTF et utiliser ses services.

Deux profils d&#39;utilisateurs GTF sont à distinguer :

- .« Utilisateurs PostgreSQL » : utilisateurs authentifiés par la base de données interne à GTF, PostgreSQL, créés directement dans GTF.
- .« Utilisateurs Active Directory (AD) » : utilisateurs d&#39;un domaine et authentifiés par un annuaire Active Directory, importés dans GTF.

La procédure de création des utilisateurs GTF diffère selon le profil :

 Création d&#39;utilisateurs et des groupes PostgreSQL

Le mode &#39;Utilisateurs &gt; Onglet Utilisateurs&#39; liste l&#39;ensemble des utilisateurs. Il permet l&#39;ajout de nouveaux utilisateurs, leur édition et suppression. Après avoir cliqué sur &#39;Ajouter un utilisateur&#39;, le formulaire suivant s&#39;affiche :

 ![](./)

Formulaire d&#39;ajout d&#39;utilisateur.

Attribuer un compte de connexion, un nom, un e-mail, un organisme et un service à l&#39;utilisateur en cours de création et lui associer son ou ses groupes d&#39;appartenance.

 ![](./)
Adresse IP du poste

Une expression régulière permet de définir la ou les adresses IP à partir desquelles l&#39;utilisateur peut se connecter. Si ce champ est laissé vide, alors toutes les adresses IP seront acceptées.

 ![](./)

De la même façon, et dans le cadre de modules spécifiques , un administrateur peut restreindre l&#39;accès à des données à un utilisateur en insérant une restriction sur une table. Le mécanisme de filtre doit être implémenté au préalable via un traitement GTF ou dans un module vMap tel que le module Cadastre. Par exemple, dans le cadre du module cadastre, l&#39;administrateur peut restreindre l&#39;accès aux données, à un utilisateur spécifique, via une expression régulière : il peut par exemple, limiter l&#39;accès à deux communes en saisissant l&#39;expression régulière :&#39; 75001|75002&#39;



Valider la création du compte en cliquant sur &#39;Créer&#39;. Saisir ensuite le mot de passe propre à l&#39;utilisateur. En cliquant sur &#39;Mettre à jour&#39;, le processus de création d&#39;un utilisateur est terminé.

 Création de groupes d&#39;utilisateurs PostgreSQL

Chaque utilisateur doit être associé à un ou plusieurs groupes. Chaque groupe correspond à un profil d&#39;utilisateurs ayant accès à des traitements qui leurs sont spécifiquement dédiés. Chaque groupe doit comporter au moins un traitement.

Le mode &#39;Utilisateurs &gt; Onglet Groupes&#39; liste les groupes d&#39;utilisateurs. Il permet d&#39;en ajouter ou d&#39;en supprimer et de leur associer un ou plusieurs traitements, un ou plusieurs utilisateurs ainsi que un ou plusieurs Dépôts (Répertoires de surveillance).

Après avoir cliqué sur &quot;Ajouter groupe&quot;, le formulaire suivant s&#39;affiche :

 ![](./)

Formulaire de création de groupe.

Attribuer un nom au nouveau groupe et lui associer un ou plusieurs utilisateurs. La section GTF permet ensuite d&#39;associer un ou plusieurs traitements et/ou dépôts au groupe. Cliquer ensuite sur « Mettre à jour». Le nom du groupe nouvellement créé apparaît désormais dans la liste des groupes.

 Utilisateurs et groupes d&#39;un annuaire Active Directory

Il est possible de gérer plusieurs domaines et d&#39;exploiter des groupes de sécurité définis directement dans un annuaire Active Directory.

L&#39;administrateur a la possibilité d&#39;importer des utilisateurs et des groupes depuis Active Directory. Cette méthode permet d&#39;hériter des droits issus de la gestion centralisée AD des utilisateurs au sein d&#39;un organisme.

L&#39;administrateur crée dans GTF le nouveau domaine, puis importe les utilisateurs et les groupes. L&#39;attribution des groupes ainsi que les mots de passe des utilisateurs ne pourront pas être changés.

 Ajout de domaines Active Directory

Le mode &#39;Utilisateurs &gt; Onglet Domaines&#39; liste les domaines Active Directory. Il permet de créer, modifier et supprimer des domaines. Le bouton &#39;Ajouter un Domaine&#39; affiche le formulaire suivant :

 ![](./)

Ajout de domaine AD.

L&#39;administrateur saisit les informations suivantes :

- .Type, Nom et Alias du domaine : le nom de domaine utilisé pour la connexion. Par exemple,  &#39;siege.entreprise.com&#39;.
- .IP ou nom de serveur : adresse IP ou nom du serveur assurant le rôle de serveur Active Directory.
- .Dn de base de recherche (utilisateur) : point d&#39;entrée pour la recherche des utilisateurs.
- .Dn de base de recherche (groupe) : point d&#39;entrée pour la recherche des groupes.
- .Filtre (utilisateur) : permet de définir des filtres pour la recherche des utilisateurs.
- .Filtre (groupe) : permet de définir des filtres pour la recherche des groupes.
- .Vérifier les droits lors du lancement du robot : permet au robot de vérifier si un utilisateur du domaine possède toujours les droits lors de l&#39;exécution du traitement. Pour cela le robot a besoin de connaître le login et le mot de passe d&#39;un utilisateur du domaine.
- .Login : login d&#39;un utilisateur du domaine.
- .Mot de passe : mot de passe de l&#39;utilisateur du domaine.

Le login et le mot de passe saisis ici permettent de vérifier les droits de l&#39;utilisateur Active Directory lors de l&#39;exécution du robot.

En cliquant sur « Créer » la procédure de création de domaine Active Directory dans GTF est finalisée.

 ![](./)
_L&#39;administrateur doit ensuite  modifier manuellement le fichier de configuration de la base de données PostgreSQL pour autoriser la connexion des utilisateurs du domaine. Dans le répertoire d&#39;installation de PostgreSQL,  modifier à l&#39;aide d&#39;un éditeur de texte le fichier pg\_hba.conf situé dans le dossier data:_



Avant modification vous devriez avoir la configuration suivante :

host    all         u\_scheduler  127.0.0.1/32         trust

host    all             +superusers             127.0.0.1/32            md5

host    all             all             127.0.0.1/32            md5

# IPv6 local connections:

host    all         u\_scheduler  ::1/128          trust

host    all             +superusers             ::1/128            md5

host    all             all             ::1/128                 md5

_Vous_ devez rajouter les deux lignes suivantes :

host    all         +gtf\_nomdomaine  127.0.0.1/32      ldap ldapserver=nomduserveur ldapprefix=&quot;&quot;

host    all         +gtf\_nomdomaine  ::1/128      ldap ldapserver=nomduserveur ldapprefix=&quot;&quot;

Pour obtenir la configuration suivante :

host    all         u\_scheduler  127.0.0.1/32         trust

host    all             +superusers             127.0.0.1/32            md5

_host    all         +gtf\ ___nomdomaine__   127.0.0.1/32      ldap ldapserver=__nomduserveur_ _ldapprefix=&quot;&quot;_

host    all             all             127.0.0.1/32            md5

# IPv6 local connections:

host    all         u\_scheduler  ::1/128          trust

host    all             +superusers             ::1/128            md5

_host    all         +gtf\ ___nomdomaine__   ::1/128      ldap ldapserver=__nomduserveur_ _ldapprefix=&quot;&quot;_

host    all             all             ::1/128                 md5

 ![](./)
**Attention !  L&#39;ordre des lignes doit impérativement être respecté.**

  Import d&#39;utilisateurs d&#39;Active Directory

Dans l&#39;onglet Utilisateurs, le bouton « Importer de l&#39;AD » permet d&#39;importer des utilisateurs à partir d&#39;un serveur Active Directory.

Une interface de connexion apparaît à l&#39;écran. L&#39;administrateur saisit son login et mot de passe Active Directory afin de se connecter au domaine précédemment créé.

Une fois la connexion effectuée, l&#39;administrateur GTF peut soit naviguer dans l&#39;arborescence de l&#39;annuaire du domaine, soit effectuer une recherche à partir de critères.

 ![](./)

Navigation dans l&#39;arbre

L&#39;arborescence du serveur Active Directory s&#39;affiche dans la fenetre de gauche de l&#39;écran. Lorsque l&#39;administrateur sélectionne un nœud, la liste des utilisateurs apparaît dans la fenetre de droite.

 ![](./)

Connexion à un serveur AD

Sélectionner ensuite les utilisateurs désirés puis cliquer sur le bouton « Importer ». Le processus d&#39;import est terminé.

Pour se connecter, les utilisateurs devront utiliser un login de type **login@nomdomaine**

Recherche d&#39;utilisateur AD

Le formulaire de recherche de l&#39;Active Directory s&#39;affiche dans la partie gauche de l&#39;écran, dans l&#39;onglet Recherche.

 ![](./)

La recherche d&#39;utilisateurs peut se faire selon 3 critères :

- .Le compte utilisateur
- .Le ou les groupes AD
- .Le service

Une fois l&#39;utilisateur désiré trouvé, il suffit de le cocher puis de cliquer sur le bouton Importer.

L&#39;interface de connexion d&#39;un utilisateur importé de la sorte, comporte désormais un champ Domaine, permettant la sélection du domaine AD d&#39;appartenance. L&#39;utilisateur s&#39;authentifie avec son  login et mot de passe de l&#39;annuaire AD.

 ![](./)

Import de groupes Active Directory

Le bouton « Importer de l&#39;AD » permet d&#39;importer des groupes à partir d&#39;un serveur Active Directory.

L&#39;association des utilisateurs et des groupes Active Directory s&#39;effectue directement dans l&#39;Active Directory. L&#39;application récupère les groupes d&#39;un utilisateur Active Directory au moment de la connexion.

Une interface de connexion apparaît à l&#39;écran. Saisir le login et mot de passe afin de se connecter au domaine.

Une fois la connexion effectuée, l&#39;administrateur GTF peut soit naviguer dans l&#39;arborescence de l&#39;annuaire du domaine, soit effectuer une recherche à partir  du nom du groupe.

Navigation dans l&#39;arbre

 Lorsque l&#39;administrateur sélectionne un nœud, la liste des groupes apparaît dans la partie droite de l&#39;écran.

Il suffit alors de sélectionner le ou les groupes désirés puis de cliquer sur le bouton « Importer ». Les groupes sont importés. Le groupe nouvellement créé apparaît dans la liste des groupes.

Recherche de groupe AD

La recherche d&#39;un groupe AD peut se faire à partir du nom de groupe recherché.

Gestion mixte des utilisateurs de domaines

GTF permet d&#39;attribuer aux utilisateurs d&#39;un domaine Active Directory, un groupe local défini dans la base interne PostgreSQL. De la sorte, un administrateur GTF ne disposant pas de droits d&#39;administration d&#39;un annuaire Active Directory, peut tout de même créer ses propres groupes d&#39;utilisateurs de GTF issus d&#39;un annuaire.

La sous-section « Sécurité » du mode Configuration permet d&#39;activer la gestion mixte des utilisateurs en autorisant des utilisateurs du domaine à appartenir à des groupes locaux.

 ![](./)

Gestion des privilèges utilisateurs

Les privilèges préfixés par &quot;vitis\_&quot; correspondent aux droits propres au socle de développement Vitis :

- .Le privilège vitis\_user permet l&#39;accès au mode Utilisateur, offrant la possibilité d&#39;éditer le compte et le mot de passe de l&#39;utilisateur courant.
- .Le privilège vitis\_admin permet l&#39;accès aux modes Utilisateurs, Configuration, Logs. Il a en charge la gestion des paramètres système et de la configuration de GTF. Il accède également dans le mode Aide à la documentation relative à l&#39;API Vitis.

3 profils d&#39;utilisateurs propres à GTF sont disponibles, chacun ayant des privilèges spécifiques. L&#39;accès aux modes dépend des privilèges attribués à l&#39;utilisateur.

- .gtf\_user = utilisateur de GTF ayant accès aux modes Mon travail, Utilisateurs et Aide. Un utilisateur ayant ce privilège exécute un projet FME mais n&#39;en publie pas.
- .gtf\_author = un utilisateur avec ce privilège est responsable de la publication de projets FME et à ce titre a accès aux modes Publication, Statistiques et Supervision. Il supervise l&#39;intégralité des projets (ceux qu&#39;il a publiés mais également les autres).
- .gtf\_admin = l&#39;administrateur de l&#39;application a tous les droits. En plus des privilèges vitis\_admin, il accède au mode Moteurs dans lequel il configure les moteurs FME et GTF. Il a en charge la gestion des utilisateurs de GTF  et de la base de données.



Dans le mode Utilisateurs, l&#39;administrateur associe à l&#39;utilisateur en cours de création le ou les privilèges désirés :

 ![](./)

Publication de traitements

Un utilisateur avec des droits d&#39;auteur peut publier un traitement. Après avoir généré un projet dans FME, il crée un traitement dans GTF puis l&#39;associe au projet.

Le mode Publication comporte l&#39;ensemble des formulaires permettant la création et le paramétrage des traitements GTF.

Ajout de projet FME

Il existe deux façons dans GTF de créer des Projets FME : l&#39;ajout de projet et l&#39;Import de projets par lot.

Ajout de projet FME

Le bouton &#39;Ajouter un Projet FME&#39; de l&#39;onglet Projets FME permet d&#39;accéder au formulaire de création de projet.

 ![](./)

_Formulaire de création de projet_

La première étape consiste à Attribuer un nom au traitement.

 INCLUDEPICTURE &quot;Resources/Images/attention.png&quot; \\* MERGEFORMAT \d ![](./)
Règles de nommage des projets



Plusieurs options sont possibles :

- .L&#39;auteur nomme le projet directement dans GTF. Dans l&#39;exemple, ci-dessus, le projet se nomme &quot;Zone\_inondable&quot;.
- .L&#39;auteur choisit d&#39;utiliser le nom du script FME et laisse dans GTF le champ &#39;Nom du traitement&#39; vide. Le nom du traitement est le nom du script FME sans son extension. Dans l&#39;exemple ci-dessus, le projet se nommerait &quot;zone\_inondableswfs2kml&quot;.
- . Si le nom du traitement existe déjà, alors le nom du nouveau projet est suffixé par la date du jour. Dans l&#39;exemple ci-dessus, le nouveau projet serait nommé &#39;Zone\_inondable\_jjmm.aaaa&#39;.

L&#39;auteur charge ensuite le projet FME dans lequel il aura pris soin de publier certains paramètres comme par exemple le répertoire destination. Le paramètre &quot;Ressources complémentaires&quot; permet d&#39;associer les ressources nécessaires pour l&#39;exécution du projet FME, comme par exemple des données sources.

 ![](./)
GTF détecte les formats de types multifichiers (Shape File, EDIGEO…) contenus dans un fichier compressé ZIP que l&#39;utilisateur uploade sur le serveur. Les fichiers sont automatiquement décompressés dans le répertoire projet.



Il définit ensuite la disponibilité du traitement sur abonnement et pour Surveillance .

Le modèle d&#39;email à associer au traitement doit ensuite être défini, ainsi que le moteur GTF auquel rattacher le traitement. La stratégie d&#39;affiliation se fait à partir de la liste des [mots clés/moteurs](../../C:/margot2/svn/produit/gtf/doc/gtf_manuel_utilisateur/Content/gtf_manuel_utilisateur/3.2%20Initialisation%20du%20compte%20Administrateur.htm#4.2), définis au préalable par l&#39;administrateur de l&#39;application.

 Le bouton &#39;Créer&#39; permet ensuite de finaliser la première étape du processus de création de traitement en générant le formulaire correspondant.

 INCLUDEPICTURE &quot;Resources/Images/attention.png&quot; \\* MERGEFORMAT \d ![](./)
La création d&#39;un projet génère ensuite un attribut &quot;Clé&quot; qui correspond à un identifiant unique universel du projet. Il s&#39;agit d&#39;une clé unique qui permet par exemple en cas de réinstallation de GTF, d&#39;assurer l&#39;unicité et le référencement du projet. Sa valeur est conservée en cas d&#39;installation du projet sur un nouveau serveur contrairement à l&#39;identifiant système ID.



 ![](./)
Tous les visualiseurs contenus dans un projet FME sont désactivés lors du processus d&#39;import ou d&#39;ajout  de projets dans GTF.



Import de projets FME par lot

GTF offre des fonctionnalités de catalogage et de gestion du patrimoine de projets FME disponibles dans un organisme. A cette fin et pour faciliter la création de plusieurs projets en même temps,  la fonction d&#39;ajout par lot a été créée permettant le chargement de plusieurs projets FME en une seule fois.

Après avoir cliqué sur le bouton &#39;Ajout par lot&#39;, l&#39;auteur clique sur le bouton Parcourir, et sélectionne les projets FME qu&#39;il souhaite intégrer à GTF. Il clique ensuite sur le bouton &#39;Transférer&#39;.

 ![](./)

Import de projets par lot

Une fois chargés, les projets FME apparaissent dans la liste des projets FME du mode Publication. L&#39;auteur est ensuite en charge de nommer ou renommer les fichiers, de gérer leur métadonnées et de leur associer les groupes et droits  désirés.

 ![](./)
Tous les visualiseurs contenus dans un projet FME sont désactivés lors du processus d&#39;import ou d&#39;ajout  de projets dans GTF.



Attribution de droits au traitement

Pour pouvoir être exploité, un traitement doit être associé à un groupe. Dans la section &#39;Droits&#39;, l&#39;auteur associe un groupe au projet nouvellement créé en faisant glisser le groupe choisi dans la partie de Groupes associés au traitement. Il clique ensuite sur le bouton « Mettre à jour ».

 ![](./)

Attribution de droits à un traitement

Gestion des métadonnées

 GTF permet la gestion des métadonnées d&#39;un projet et l&#39;exploitation des métadonnées natives issues des projets FME.

Les métadonnées d&#39;un projet, définies dans FME via le Navigateur, sont chargées dans GTF.

- . Les sections Description, Catégorie, Conditions d&#39;utilisation, Utilisation, Pré requis et Historique sont directement issues du projet FME et peuvent être modifiées .
- . La date de dernière sauvegarde, l&#39;encodage et la version FME sont propres au projet FME source et sont modifiés automatiquement dans GTF en cas de rechargement du projet FME.

 ![](./)
_Une catégorie définie dans un projet FME, est importée dans GTF et créée dans le menu Catégories, si elle n&#39;existe pas._



 ![](./)

Métadonnées d&#39;un projet

La section Métadonnées du mode Publication permet à l&#39;auteur, de modifier ces dernières et de les réécrire dans le projet FME.

- .Le bouton &#39;Mettre à jour&#39; permet d&#39;enregistrer les modifications des métadonnées dans GTF.
- .Le bouton &#39;Relire le projet&#39; permet de recharger les métadonnées du projet FME initial. Les champs Description, Utilisation, Pré requis et Conditions d&#39;utilisation saisies dans GTF sont remplacés par les valeurs issues du projet FME source.
- .Le bouton &#39;Ecrire le projet&#39; permet de modifier les métadonnées du projet FME source. Les valeurs des champs Description, Utilisation, Pré requis et Conditions d&#39;utilisation initiales sont remplacées par les valeurs saisies dans GTF. Le projet .fmw modifié est disponible dans la section Répertoire Projet.

 ![](./)
Les métadonnées d&#39;un projet sont chargées lors du premier chargement d&#39;un projet FME. Si les métadonnées sont ajoutées et/ou modifiées dans GTF et que l&#39;on procède à un nouveau chargement du projet FME, alors les métadonnées du projet FME, n&#39;écrasent pas celles éditées dans GTF. Les métadonnées sont ainsi chargées que lors du premier chargement d&#39;un projet FME. Le bouton &#39;Relire le projet&#39; permet de contourner ce fonctionnement pour permettre le rechargement des du projet FME source initialement chargé.



Gestion et personnalisation des paramètres publiés : Travailler dans le studio

La section Formulaire du mode Publication permet de gérer l&#39;affichage du formulaire de demande de traitement tel qu&#39;il sera affiché lors d&#39;une demande émise par  un utilisateur.

 Le studio permet de personnaliser graphiquement chaque paramètre publié importé depuis FME, et permet la mise en page générale du formulaire de demande.

 ![](./)

Studio de personnalisation de formulaire.

Le studio de personnalisation des formulaires est composé de 4 fenêtres :

-
.Une fenêtre centrale de prévisualisation du formulaire. Elle permet de prévisualiser le formulaire tel qu&#39;il sera affiché lors d&#39;une demande de traitement, mais il est possible d&#39;afficher le formulaire JSON ou Javascript en sélectionnant le type d&#39;affichage désiré en haut de la fenêtre. ![](./)
-
.Une fenêtre des paramètres publiés, à droite de l&#39;écran : elle liste l&#39;ensemble des paramètres publiés du projet et leur ordre d&#39;affichage. Il est possible de modifier l&#39;ordre d&#39;affichage des paramètres ![](./)
, de les supprimer
 ![](./)
 et en d&#39;en créer de nouveaux
 ![](./)
.
, de les supprimer ![](./)
 et en d&#39;en créer de nouveaux
 ![](./)
.
 et en d&#39;en créer de nouveaux ![](./)
.
.
- .Une fenêtre de définition des paramètres, à gauche en bas de l&#39;écran, qui permet leur édition et configuration.
- .Une fenêtre formulaire, en haut à gauche de l&#39;écran, qui permet l&#39;enregistrement, la publication et le nommage de chaque formulaire. Il permet d&#39;afficher le formulaire par défaut, le formulaire publié et le formulaire personnalisé.

Formulaire par défaut, Formulaire personnalisé, Formulaire publié

Le formulaire par défaut comporte les paramètres publiés du projet FME. Après visualisation, l&#39;auteur peut choisir de conserver en l&#39;état ce formulaire ou de le personnaliser.

Chaque projet FME chargé dans GTF est stocké dans le répertoire \workspace du répertoire d&#39;installation de GTF. Le  sous-répertoire workspace\fme stocke le projet .fmw et les ressources du projet, et le répertoire workspace\form stocke les fichiers de gestion et de personnalisation des formulaires du traitement.

Une fois un projet créé, GTF créé 3 fichiers identiques :

-
.DsubForm.json : formulaire par défaut du traitement, affiché dans le studio lorsque l&#39;on sélectionne le bouton ![](./)
-
.SubForm.json : formulaire publié par GTF, affiché dans le studio lorsque l&#39;on sélectionne le bouton ![](./)
-
.WsubForm.json : formulaire destiné à être personnalisé, affiché dans le studio lorsque l&#39;on sélectionne le bouton de personnalisation ![](./)

Lors de la publication d&#39;un formulaire personnalisé, le fichier WsubForm est modifié puis écrase le fichier SubForm.

Lors de la création d&#39;un projet, les 3 formulaires par défaut, personnalisé et publié sont identiques. L&#39;auteur d&#39;un projet peut ensuite personnaliser le formulaire par défaut. Il choisit de publier ou pas le formulaire personnalisé.

A tout moment il peut revenir au formulaire par défaut et le publier à nouveau.

 ![](./)
En cas de re chargement d&#39;un projet FME, si le formulaire publié est identique au formulaire par défaut alors les 3 formulaires sont écrasés. En revanche, lorsque le formulaire publié est identique au formulaire personnalisé, alors seul le formulaire par défaut est écrasé. Dans ce cas de figure, les formulaires personnalisés et publiés sont donc conservés.



 ![](./)
Dans la liste des projets, on peut distinguer les projets publiés exploitant un formulaire par défaut, des projets exploitant un formulaire personnalisé par la couleur du pictogramme du champ Formulaire : un pictogramme vert signifie que le formulaire par défaut est publié. Un pictogramme bleu indique que le formulaire publié est un formulaire personnalisé.

 ![](./)

Liste des projets et formulaires exploités

Création d&#39;onglets dans un formulaire

L&#39;auteur d&#39;un projet peut choisir d&#39;agencer le formulaire de demande de traitement sous forme d&#39;onglets. Il peut ainsi répartir les paramètres sur plusieurs onglets.

Le bouton &#39;Edition &gt; Gestion des onglets&#39; ![](./)
 de la fenêtre des formulaires personnalisés permet d&#39;accéder à la fenêtre de gestion de ces derniers.



 ![](./)

Studio - Fenêtre de gestion des onglets d&#39;un formulaire.

Après avoir édité et nommé un onglet ![](./)
, cocher les paramètres devant le composer. Le bouton &#39;Ajouter un onglet&#39; en bas de la fenêtre permet la création d&#39;un nouvel onglet.

Un aperçu des onglets nouvellement créés s&#39;affiche dans la partie de droite de la fenêtre.

Cliquer sur Valider pour revenir au studio.

 ![](./)



 ![](./)
Un paramètre peut apparaître sur deux onglets différents. Lors de la demande d&#39;un tel projet, l&#39;édition d&#39;un paramètre dans un onglet est automatiquement reportée dans le deuxième onglet.





**Paramètres publiés FME et contrôles**  **GTF **

Les paramètres publiés de FME sont importés dans GTF et peuvent être modifiés dans le studio via des contrôles GTF. Un contrôle GTF est converti en paramètre publié FME lors du traitement du projet.

Certains contrôles GTF ne sont pas issus de paramètres publiés de FME et correspondent à des composants de mise en page (interface) destinés à personnaliser l&#39;interface du formulaire de demande de projet.

Il existe 20 types de contrôles GTF paramétrables dans la fenêtre de Définition des Paramètres :



| Nom du contrôle GTF |
| --- |
| Bouton radio |
| Carte Bing |
| Carte OSM |
| Carte vMap |
| Champ caché |
| Couleur |
| Curseur |
| Date et Heure |
| Décimal |
| Entier |
| Fichier local |
| Interface - Ligne de séparation |
| Label |
| Label Titre |
| Liste |
| Liste déroulante |
| Texte en édition 1 ligne |
| Texte en édition Mot de passe |
| Texte en édition Multiligne |
| Texte en édition URL |

 ![](./)

 ![](./)

Paramètre publié de type Choix - Contrôle de type Liste déroulante

 Un paramètre publié FME de type Choix est importé dans un GTF en contrôle de type Liste déroulante.

La configuration de la liste se fait via le Gestionnaire de source de données.

L&#39;auteur du projet nomme le paramètre et son libellé tel qu&#39;il sera affiché dans le formulaire de demande et définit le nombre de lignes. Il indique si le paramètre est obligatoire en cochant ou pas la case Requis.

Il est possible de faire de cette liste une liste en cascade, en définissant la liste parent et les attributs sur lesquels doit reposer l&#39;ascendance.

 ![](./)

Paramètre publié de type Choix et Contrôle GTF de type Liste déroulante

 Paramètre publié de type Choix multiple - Contrôle de type Liste

Un paramètre publié FME de type Choix multiple est importé dans GTF en contrôle de type Liste. Le Gestionnaire de source de données permet de configurer la liste importée.

L&#39;auteur du projet nomme le paramètre et le libellé tel qu&#39;il sera affiché dans le formulaire de demande et définit la valeur par défaut. Il paramètre le nombre de lignes à afficher. Il définit si le paramètre est obligatoire en cochant ou pas la case Requis.

 ![](./)

Paramètre publié de type Choix multiple et contrôle GTF de Type Liste

Il est possible de faire de cette liste une liste en cascade, en définissant la liste parent et les attributs sur lesquels doit reposer l&#39;ascendance.

Paramètre publié de type Choix avec alias - Contrôle de type Liste déroulante

Un paramètre publié de type choix avec alias est importé dans GTF en contrôle de type Liste déroulante.

La configuration de la liste se fait dans le Gestionnaire de source de données.

L&#39;auteur du projet nomme le paramètre et son libellé tel qu&#39;il sera affiché dans le formulaire de demande et définit sa valeur par défaut. Il paramètre le nombre de lignes à afficher. Il définit si le paramètre est obligatoire en cochant ou pas la case Requis.

 ![](./)

Paramètre publié de type Choix avec alias et Contrôle GTF de type Liste déroulante.

Il est possible de faire de cette liste une liste en cascade, en définissant la liste parent et les attributs sur lesquels doit reposer l&#39;ascendance.

 Paramètre publié de type Choix avec Alias Multiple - Contrôle de type Liste

Un paramètre pubié de type choix avec alias multiple est importé dans GTF en contrôle de type Liste.

La configuration de la liste se fait dans le Gestionnaire de source de données.

L&#39;auteur du projet nomme le paramètre et le libellé qui sera affiché dans le formulaire de demande, définit le nombre de lignes à afficher. Il définit si le paramètre est obligatoire en cochant ou pas la case Requis.

 ![](./)

Paramètre publié de type Choix avec alias multiple et contrôle GTF de type Liste

Il est possible de faire de cette liste une liste en cascade, en définissant la liste parent et les attributs sur lesquels doit reposer l&#39;ascendance.

Paramètre publié de type choix de couleur - Contrôle de type Couleur

Un paramètre publié de tye Choix de la couleur est importé dans GTF en contrôle de type Couleur . L&#39;auteur nomme le paramètre et le libellé qui sera affiché dans le formulaire de demande, définit la couleur par défaut . Il peut choisir la largeur du contrôle et définir si ce paramètre est obligatoire ou pas.

 ![](./)

Paramètre publié de type Choix de la couleur et Contrôle GTF de type Couleur

 Paramètre publié de type Curseur - Contrôle de type Curseur

Un paramètre publié de type curseur est importé sous la forme de contrôle de type Curseur. L&#39;auteur du projet nomme le paramètre et le libellé tel qu&#39;il sera affiché dans le formulaire de demande et définit les valeurs minimales et maximales ainsi que la valeur par défaut du curseur.

 ![](./)

Paramètre publié et contrôle de type Curseur

 Paramètre publié de type Date/heure - Contrôle de type Date et Heure

Un paramètre publié de type Date/Heure est importé dans GTF sous la forme de contrôle Date et Heure.

L&#39;auteur nomme le paramètre et le libellé qui sera affiché dans le formulaire de demande. Il peut définir la date et heure affichées par défaut. Il définit si le paramètre est obligatoire en cochant ou pas la case Requis.

 ![](./)

Paramètre publié et contrôle de type Date/heure

Paramètre publié de type Entier - Contrôle de type Entier

Un paramètre publié de type Entier est importé dans GTF en contrôle de type Entier. L&#39;auteur nomme le paramètre et le libellé qui sera affiché dans le formulaire de demande et définit la valeur par défaut . Il peut définir si ce paramètre est obligatoire ou pas en cochant la case Requis.

 ![](./)

 ![](./) ![](./)

Paramètre publié et contrôle de type Entier

 Paramètre publié de type Flottant - Contrôle de type Décimal

Un paramètre publié de type Flottant est importé dans GTF en contrôle de type Décimal. L&#39;auteur nomme le paramètre et le libellé qui sera affiché dans le formulaire de demande et définit la valeur par défaut. Il peut définir si ce paramètre est obligatoire ou pas en cochant la case Requis.

 ![](./)

Paramètre publié de type Flottant et contrôle de type Décimal

Paramètre publié de type Mot de passe - Contrôle de type Texte en édition mot de passe

Un paramètre publié FME de type Mot de passe est importé dans GTF sous la forme de contrôle de type Texte en édition - mot de passe.

 L&#39;auteur nomme le paramètre et le libellé qui sera affiché dans le formulaire de demande.

Il peut définir un motif sous la forme d&#39;expression régulière, pour contrôler l&#39;affichage du mot de passe et s&#39;assurer que la valeur respecte bien un modèle.

 Il peut définir si ce paramètre est obligatoire ou pas en cochant la case Requis, et choisit la largeur du contrôle.

 ![](./)

Paramètre publié de type mot de passe et Contrôle de type Texte en édition - mot de passe

Paramètre publié de type Nom de fichier multiple - Contrôle de type Fichier Local

Un paramètre publié FME de type Nom de fichier (Multiple) est importé dans GTF sous la forme de contrôle de type Fichier Local.

L&#39;auteur du projet nomme le paramètre et le libellé qui sera affiché dans le formulaire de demande, définit la largeur du contrôle et indique si le paramètre est obligatoire ou pas.

 ![](./)

Paramètre publié de type Nom de fichier Multiple et Contrôle de type Fichier local



Options avancées

Les options avancées permettent d&#39;affiner l&#39;affichage du formulaire lors du chargement de fichiers en faisant apparaître ou pas la prévisualisation des fichiers, ainsi que les boutons de chargement et de suppression des fichiers.

 ![](./)

Contrôle GTF de Type Fichiers Multiples. Options avancées.

Paramètre publié de type Nom de fichier existant - Contrôle de type Fichier local

Un paramètre publié FME de type Nom de fichier (Existant) est importé dans GTF sous la forme de contrôle de type Fichier Local.

L&#39;auteur du projet nomme le paramètre et le libellé qui sera affiché dans le formulaire de demande, définit la largeur du contrôle et indique si le paramètre est obligatoire ou pas.

 ![](./)

Paramètre publié de type Nom de fichier existant et contrôle GTF de type Fichier Local

Options avancées

Les options avancées permettent d&#39;affiner l&#39;affichage du formulaire lors du chargement de fichiers en faisant apparaître ou pas la prévisualisation des fichiers, ainsi que les boutons de chargement et de suppression des fichiers.

Paramètre de type Nom de fichier en sortie - Contrôle de type Fichier Local

Le paramètre publié de type Fichier en sortie est importé sous la forme de contrôle de type Texte en édition - 1 ligne. L&#39;auteur du projet nomme le paramètre et définit le libellé tel qu&#39;il sera affiché dans le formulaire de demande. Il peut insérer une expression régulière dans le champ Motif pour assurer un contrôle de la valeur saisie. Il peut définir une valeur par défaut, la largeur du contrôle à afficher et indique si le paramètre est obligatoire ou pas.

 ![](./)

Paramètre publié de type Nom de fichier en sortie et contrôle GTF de type Texte en édition - 1 ligne

Paramètre publié de type Nom de système de coordonnées - Contrôle de type Liste déroulante

Un paramètre publié de type Nom de Système de coordonnées est importé dans GTF sous la forme d&#39;une Liste déroulante. Les valeurs de la liste sont automatiquement importées et visibles dans le gestionnaires de source de données.

 ![](./)

Paramètre publié de type Nom de système de coordonnées et Contrôle de type Liste déroulante.

La configuration de la liste se fait via le Gestionnaire de source de données.

L&#39;auteur du projet nomme le paramètre et le libellé qui sera affiché dans le formulaire de demande et définit le nombre de lignes à afficher ainsi que la largeur du contrôle. Il indique si le paramètre est obligatoire en cochant ou pas la case Requis.

Paramètre publié de type Répertoire existant - Contrôle de type Fichier local

Un paramètre publié de type Répertoire existant est importé sous la forme d&#39;un contrôle de type Fichier local. L&#39;auteur du projet nomme le paramètre et le libellé tel qu&#39;il sera affiché dans le formulaire de demande, il définit la largeur du contrôle et indique si ce paramètre est obligatoire ou pas.

Les options avancées permettent d&#39;affiner les paramètres d&#39;affichage lors du téléchargement du fichier.

 ![](./)

Paramètre publié de type Répertoire (Existant) et contrôle de type Fichier Local

 Paramètre publié de type Répertoire en sortie - Contrôle de type Texte en édition 1 ligne

Un paramètre publié de type Répertoire en sortie est importé sous la forme d&#39;un contrôle de type Texte en édition 1 ligne. L&#39;auteur du projet nomme le paramètre et le libellé tel qu&#39;il sera affiché dans le formulaire de demande. Il peut définir la valeur par défaut du nom de répertoire à créer, et il peut saisir une expression régulière dans le champ Motif pour assurer un contrôle du nom créé.

 Il peut définir la largeur du contrôle et indiquer si le paramètre est obligatoire en cochant ou pas la case Requis.

 ![](./)

 ![](./) ![](./)

Paramètre publié de type Répertoire en sortie et contrôle de type Texte en édition- 1 ligne

 Paramètre publié de type Texte -Contrôle de type Texte en édition 1 ligne

Un paramètre publié de type Texte est importé sous la forme d&#39;un contrôle de type Texte en édition- 1 ligne. L&#39;auteur du projet nomme le paramètre et le libellé tel qu&#39;il sera affiché dans le formulaire de demande. Il peut définir la valeur par défaut à créer, et peut saisir une expression régulière dans le champ Motif pour assurer un contrôle de la valeur saisie.

 Il peut définir la largeur du contrôle et indiquer si le paramètre est obligatoire en cochant ou pas la case Requis.

 ![](./)

Paramètre publié de type texte et contrôle GTF de type Texte en édition - 1 ligne

 Paramètre publié de type Texte multiligne - Contrôle de type Texte en édition - Multiligne

Un paramètre publié de type Texte multiligne est importé sous la forme d&#39;un contrôle de type Texte en édition-multiligne. L&#39;auteur du projet nomme le paramètre et le libellé tel qu&#39;il sera affiché dans le formulaire de demande. Il peut définir la valeur par défaut et la largeur du contrôle et indiquer si le paramètre est obligatoire en cochant ou pas la case Requis.

 ![](./) ![](./)

Paramètre publié de type Texte multiligne et contrôle de type Texte en édition - Multiligne

 Paramètre publié de type Texte Multiligne ou Nombre- Contrôle de type Texte en édition - Multiligne

Un paramètre publié de type Texte Multiligne ou Nombre est importé sous la forme d&#39;un contrôle de type Texte en édition-Multiligne. L&#39;auteur du projet nomme le paramètre et le libellé tel qu&#39;il sera affiché dans le formulaire de demande. Il peut définir la valeur par défaut et la largeur du contrôle et indiquer si le paramètre est obligatoire en cochant ou pas la case Requis.

 ![](./) ![](./)

 ![](./)

Paramètre publié de type Texte multiligne ou Nombre et contrôle de type Texte en édition - Multiligne

Paramètre publié de type URL - Contrôle de type Texte en édition URL

Un paramètre publié de type URL est importé sous la forme d&#39;un contrôle de type Texte en édition-URL. L&#39;auteur du projet nomme le paramètre et le libellé tel qu&#39;il sera affiché dans le formulaire de demande. Il peut insérer un motif via une expression régulière pour assurer un contrôle sur la valeur saisie (type de protocole spécifique) , définir la valeur par défaut et la largeur du contrôle et indiquer si le paramètre est obligatoire en cochant ou pas la case Requis

 ![](./)

 ![](./) ![](./)

Paramètre publié de type URL et contrôle de type Texte en édition - URL

Contrôle GTF de type Bouton radio- Contrôle de type Bouton Radio

Un paramètre publié FME de type Choix est importé dans GTF en tant que contrôle de type Liste Déroulante, mais il est possible de modifier ce dernier en exploitant un contrôle de Type Bouton radio.

L&#39;auteur du projet nomme le paramètre et son libellé tel qu&#39;il sera affiché dans le formulaire de demande.

 Il définit la valeur par défaut et détermine si les boutons radios seront désactivés ou pas. Il définit ensuite les options possibles en entrant le libellé du bouton et la valeur envoyée en base.

Le bouton ![](./)
 permet de rajouter des boutons au paramètre.



 ![](./)

Contrôle de type Bouton Radio

Contrôles GTF de type Carte OSM, carte Bing et carte vMap

GTFpermet d&#39;exploiter les services web OSM, Bing Maps ou Vitis vMap pour personnaliser un formulaire en exploitant leurs ressources cartographiques.

Par exemple, dans FME, on peut définir une géométrie dans un champ de type texte définie par une chaîne de caractère WKT.

 Dans GTF, Il est plus simple de personnaliser le formulaire de saisie  en exploitant une carte OSM comme support de saisie de la géométrie plutôt que de rentrer une chaîne WKT dans un contrôle de type Texte.

L&#39;auteur du projet qui insère un élément (ou qui modifie un paramètre existant) de type carte OSM, nomme le paramètre, et définit le libellé qui sera affiché dans le formulaire de demande. Il définit la hauteur et la largeur de la carte et indique si ce paramètre est obligatoire ou pas en cochant la case Requis.

 ![](./)

Il définit ensuite les options spécifiques aux éléments de type carte :

 INCLUDEPICTURE &quot;Resources/Images/carte\_outils.png&quot; \\* MERGEFORMAT \d ![](./)

- .La projection de la carte : WGS84 ou Lambert 93. En Lambert 93, l&#39;étendue par défaut correspond à l&#39;ensemble de la France métropolitaine.
- .Méthode de centrage de la carte : l&#39;auteur choisit si le centre de la carte est défini par un point défini via des coordonnées X/Y et une échelle d&#39;affichage, ou si le centre de la carte est paramétrée par son étendue définie par les coordonnées X et Y Min et Max.

L&#39;auteur choisit ensuite les éléments de dessin et de navigation qui seront affichés sur la carte du formulaire de demande :

- .Position de la souris : affichage dynamique des coordonnées de la souris selon la projection définie.
- .Boutons de zoom : affichage des boutons de navigation classique zoom avant, zoom arrière et retour à l&#39;étendue par défaut.
- .Echelle : affichage de l&#39;échelle.
- .Projection de la carte : affichage de la projection Lambert 93 ou WGS 84.
- .Multiples géométries : possibilité ou pas de saisir des géométries de type différent (point, ligne et polygone).
- .Plein écran : permet d&#39;afficher la carte en mode plein écran.
- .Suppression générale : Suppression de toutes les géométries saisies sur la carte.
- .Edition : modification de la géométrie sélectionnée.
- .Dessiner un point.
- .Dessiner une ligne.
- .Dessiner un polygone.

Le champ Valeur permet à l&#39;auteur de définir une géométrie qui sera affichée par défaut dans le formulaire de demande. Cette géométrie est décrite via une chaîne WKT.

 ![](./)

Contrôle Carte OSM. Exemple de valeur par défaut



 ![](./)

Formulaire de demande d&#39;un contrôle de type carte OSM- Géométrie saisie par défaut



Carte Bing

Tous les paramètres de personnalisation d&#39;une carte Bing Maps sont identiques à ceux des cartes OSM. Il faut fournir en plus, une clé d&#39;accès pour pouvoir exploiter ce service web cartographique.

Générer une clé Bing Maps sur le site [https://www.bingmapsportal.com/](https://www.bingmapsportal.com/)

Une fois obtenue, entrer la clé dans le champs Clé et sélectionner la carte à afficher dans le formulaire de demande :

- .Aerial
- .Aerial WithLabels
- .Road

 ![](./)

 ![](./)

Formulaire de demande de traitement avec contrôle de type carte Bing.

**Carte vMap**

Pour pouvoir exploiter une carte vMap dans GTF, Il faut au préalable, dans vMap, exporter la définition de la carte . L&#39;export d&#39;une carte vMap génère un fichier map.json que l&#39;auteur du formulaire doit télécharger (champ Fichier local) pour pouvoir l&#39;intégrer dans un formulaire. Il procède ensuite de la même façon qu&#39;avec les autres ressources de type carte, en nommant le paramètre et son libellé, puis en paramétrant l&#39;affichage des outils propres aux cartes.

 ![](./)



 ![](./)

Formulaire de demande de traitement avec contrôle de type carte vMap.

Contrôle GTF de type Interface - Ligne de séparation

Un contrôle de type Interface-Ligne de séparation permet d&#39;améliorer l&#39;affichage d&#39;un formulaire de demande d&#39;un traitement en y insérant des lignes et accroître de la sorte son organisation et sa lisibilité.

Contrôles GTF de type Label

Il existe 2 contrôles de type Label :

- .Label

Un contrôle GTF de type Label permet d&#39;insérer un champ et sa valeur dans un formulaire de demande de projet, sans qu&#39;il puisse être modifié. L&#39;auteur nomme le paramètre et son libellé tel qu&#39;il sera affiché dans le formulaire. Il définit ensuite la valeur à afficher, ainsi que la largeur du contrôle.

- .Label- Style Titre

Un contrôle Label Style Titre permet d&#39;insérer un titre dans le formulaire de demande. L&#39;auteur définit le nom du paramètre et son libellé, puis définit la classe html à associer au titre.



Contrôle GTF de type Champ caché

Un contrôle GTF de type Champ caché permet de masquer un paramètre publié. Le paramètre est exploité dans le traitement mais n&#39;est pas apparent.

L&#39;auteur nomme le paramètre et définit la valeur à exploiter.

 ![](./)
Un paramètre publié FME caché, c&#39;est-à-dire que son nom est par préfixé par H\_, est directement importé dans GTF en contrôle de type Champ caché.



 ![](./) ![](./) ![](./)

Contrôle de type champ caché.

 Gestionnaire de sources de données

Le gestionnaire de sources de données permet la création, l&#39;édition et la suppression des sources de données à associer aux contrôles GTF de type :

- .Liste
- .Liste déroulante

 Le Gestionnaire de sources de données permet d&#39;exploiter des données :

- .Texte : valeurs saisies directement dans le gestionnaire ou importées depuis un paramètre FME de type Choix.
- .Valeurs de table locale : valeurs issues d&#39;une table de base de données installée sur le même serveur que GTF.
- .Base de données externe : valeurs importées d&#39;une table de base de données externe à GTF.
- .Service web Vitis : permet d&#39;exploiter un service web pour en récupérer les ressources.

Le gestionnaire de source de données est accessible en cliquant sur le bouton ![](./)
 en bas à droite de la fenêtre des paramètres publiés.



 ![](./)

Fenêtre du Gestionnaire de source de données

On peut ajouter, éditer ou supprimer une source de données.

Le bouton &#39;Ajouter&#39; permet de créer une nouvelle source de données.

Le type de source détermine les paramètres de connexion devant être définis pour pouvoir importer les valeurs.

** **** Ajout de source de données de type texte**

Cette option permet de saisir directement des valeurs de type texte qui s&#39;afficheront dans le formulaire sous forme de liste déroulante.

Paramétrer la source de données

 ![](./)

_Gestionnaire de source de données. Source de données de type Texte._

Après avoir nommé la source de données, saisir les libellés et les clés (stockées en base) séparés par le caractère |.

Le bouton &#39;Aperçu&#39;, permet de visualiser la liste en cours de création.

Le bouton &#39;Valider&#39; permet de valider la création de la liste, de fermer la fenêtre en cours et de revenir à la liste des sources de données.

Cliquer à nouveau sur &#39;Valider&#39; pour fermer le gestionnaire de source de données et revenir au studio.

**Lier la source de données au paramètre publié**

Pour associer la source de données créée à un paramètre de type liste , sélectionner le paramètre dans la fenêtre Paramètres publiés, puis l&#39;éditer dans la fenêtre de Définition.

 ![](./)

_Sélection du paramètre publié dans le studio._

Sélectionner ensuite la source de données nouvellement créée dans le champs Source de données :

 ![](./)

_Sélection de la source de données._

Cliquer ensuite sur le bouton &#39;Recharger les sources de données&#39; ![](./)
 en haut à droite de la fenêtre de prévisualisation, pour pouvoir visualiser la liste.



Vous pouvez paramétrer le nombre de lignes à afficher dans la liste, sa largeur et définir si ce paramètre est obligatoire ou pas, en cochant le paramètre &#39;Requis&#39;.

Ajout d&#39;une source de données de type Valeurs d&#39;une table locale

Le Gestionnaire de source de données permet d&#39;importer les valeurs d&#39;une table de base de données installée sur le même serveur que GTF.

Paramétrer la source de données

 ![](./)

_Gestionnaire de source de données. Source de données de type Valeurs de table locale._

Saisir le nom à attribuer à la source de données à créer, puis la base de données (facultatif). Appuyer sur le bouton Schémas pour obtenir la liste des schémas de la base, puis sur le bouton Tables pour sélectionner celles contenant les valeurs à utiliser. Le bouton &#39; Test&#39; permet de tester la connexion en affichant la table dans la fenêtre Aperçu.

Il est possible de filtrer les données à importer via une clause de type Where, définie dans le champs &#39;Filtre&#39;. Dans l&#39;exemple ci-dessus, on peut choisir de n&#39;afficher que les bâtiments d&#39;une commune et saisir dans le champs filtre la clause : id\_com=&#39;340003&#39;.

Le bouton &#39;Valider&#39; permet de fermer la fenêtre en cours et de revenir à liste des sources de données.

Cliquer à nouveau sur Valider pour fermer le gestionnaire de source de données et revenir au studio.

**Lier la source de données au paramètre publié**

Pour lier cette liste à un paramètre publié, sélectionner le paramètre désiré dans la fenêtre des Paramètres publiés à droite de l&#39;écran, pour pouvoir ensuite l&#39;éditer dans la fenêtre de Définition :

 ![](./)

_Sélection de la source de données._

Nommer le paramètre, éditer son libellé puis sélectionner dans la liste déroulante la source de données nouvellement créée, dans l&#39;exemple ci-dessus : &#39;liste\_moteurs&quot;.

Définir ensuite la clé ainsi que le libellé qui sera affiché dans le formulaire : pour cela cliquer sur le bouton ![](./)
 pour charger les valeurs et sélectionner celles à définir comme clé puis comme libellé :

  ![](./)

_Définition de l&#39;attribut clé._

Dans la fenêtre de prévisualisation, cliquer ensuite sur le bouton &#39;Recharger les sources de données&#39; ![](./)
, pour pouvoir prévisualiser la liste, telle qu&#39;elle s&#39;affichera dans le formulaire de demande :

 ![](./)

_Prévisualisation du paramètre de type Liste._

Vous pouvez paramétrer le nombre de lignes à afficher dans la liste, sa largeur et définir si ce paramètre est obligatoire ou pas, en cochant le paramètre &#39;Requis&#39;.

Vous pouvez faire de cette liste une liste en cascade en cochant la case Cascade.

  ![](./)
.

Options avancées = affiner l&#39;affichage des listes

Il est possible d&#39;affiner l&#39;affichage des éléments de la liste via des commandes de tri (order\_by et sort\_order) sur les attributs dont on spécifie les noms dans le champs Attributs. Ils doivent êtres séparés par le caractère |. Pour distinguer les valeurs identiques, on peut définir une clause distinct.

On peut également filtrer les valeurs à afficher via une clause Where dont on spécifie les arguments dans le champ &#39; filter&#39;. Dans l&#39;exemple ci-dessous, on choisit de n&#39;afficher que le moteur n° 1 en insérant une clause Where sur l&#39;attribut gtf\_engine\_id :

 ![](./)

Ajout d&#39;une source de données de type Base de données externe

GTF permet d&#39;importer des valeurs d&#39;une table de base de données externe.

Paramétrer la source de données

 ![](./)

 _Gestionnaire de source de données. Source de données de type Base de données externe._

Après avoir saisi le nom de la nouvelle source de données, saisir les paramètres de connexion à la base de données (serveur, port, sgbd, login, mot de passe et tables). Le bouton ![](./)
 permet d&#39;afficher la liste des tables de la base et de la sorte de s&#39;assurer de la réussite de la connexion.

Il est également possible de filtrer les données à importer via une clause de type Where, saisie dans le champs Filtre.

Dans l&#39;exemple ci-dessus, seuls les ESI en instruction et inscrits seront listés dans le formulaire.

Le bouton &#39;Valider&#39; permet de fermer la fenêtre en cours et revenir à liste des sources de données.

Cliquer, à nouveau, sur Valider pour fermer le gestionnaire de source de données et revenir au studio.

Lier la source de données au paramètre publié

Pour lier cette liste à un paramètre publié, sélectionner le paramètre désiré dans la fenêtre des Paramètres publiés à droite de l&#39;écran, pour pouvoir ensuite l&#39;éditer dans la fenêtre de Définition :

 ![](./)

Nommer le paramètre, éditer son libellé puis sélectionner dans la liste déroulante la source de données nouvellement créée, dans l&#39;exemple ci-dessus : &#39;esi&#39;.

Définir ensuite la clé ainsi que le libellé : pour cela, cliquer sur le bouton ![](./)
 pour charger les valeurs et sélectionner celles à définir comme clé puis comme libellé :

 ![](./)

Cliquer ensuite sur le bouton &#39;Recharger les sources de données&#39; ![](./)
 dans la fenêtre de prévisualisation, pour pouvoir prévisualiser la liste, telle qu&#39;elle s&#39;affichera dans le formulaire de demande :

 ![](./)

Vous pouvez paramétrer le nombre de lignes à afficher dans la liste, sa largeur et définir si ce paramètre est obligatoire ou pas, en cochant le paramètre &#39;Requis&#39;.

Vous pouvez faire de cette liste une liste en cascade en cochant la case Cascade.

 ![](./)
.

Options avancées

 Ajout d&#39;une source de données de type Service web

Il est possible d&#39;exploiter les ressources des services web Vitis et Gtf pour configurer les paramètres de type liste.

 ![](./)

_Gestionnaire de source de données. Source de données de type Service Web._

Après avoir sélectionné le service à exploiter (Vitis ou Gtf), sélectionner la ressource dont vous voulez importer les données.

Dans l&#39;exemple ci-dessus, on exploite la ressource Groups du service Vitis. Les groupes d&#39;utilisateurs de Vitis seront importés dans le paramètre publié de type liste, en cours de création.

 ![](./)
_L&#39;accès aux services web diffère selon les privilèges liés à l&#39;utilisateur. Il faut donc s&#39;assurer que le compte connecté ait bien les droits requis pour accéder au service web de son choix._ _Consulter la liste des droits par service__._



Le bouton &#39;Valider&#39; permet de fermer la fenêtre en cours et revenir à liste des sources de données.

Cliquer à nouveau sur Valider pour fermer le gestionnaire de source de données et revenir au studio.

Lier la source de données au paramètre publié

Pour lier cette liste à un paramètre publié, sélectionner le paramètre désiré dans la fenêtre des Paramètres publiés à droite de l&#39;écran, pour pouvoir ensuite l&#39;éditer dans la fenêtre de Définition :

 ![](./)

Nommer le paramètre, éditer son libellé puis sélectionner dans la liste déroulante la source de données nouvellement créée, dans l&#39;exemple ci-dessus : &#39;groupes&#39;.

Définir ensuite la clé ainsi que le libellé. Pour cela cliquer sur le bouton ![](./)
 pour charger les valeurs et sélectionner celles à définir comme clé puis comme libellé :

 ![](./)

Cliquer ensuite sur le bouton &#39;Recharger les sources de données&#39; ![](./)
 dans la fenêtre de prévisualisation, pour pouvoir visualiser la liste, telle qu&#39;elle s&#39;affichera dans le formulaire de demande :

 ![](./)

Vous pouvez paramétrer le nombre de lignes à afficher dans la liste, sa largeur et définir si ce paramètre est obligatoire ou pas, en cochant le paramètre &#39;Requis&#39;.

Vous pouvez faire de cette liste une liste en cascade en cochant la case cascade.

Options avancées

 Créer des listes en cascade

On peut choisir d&#39;afficher une liste dont le contenu varie en fonction des valeurs sélectionnées dans une autre liste. L&#39;option Cascade permet le paramétrage de telles listes en spécifiant le paramètre publié parent et l&#39;attribut enfant sur lequel effectuer le filtre d&#39;affichage.

**Attributs de filtrage et**  **Signe de comparaison**

Après avoir défini quel est l&#39;élément parent, il faut définir le champ enfant sur lequel repose l&#39;ascendance ainsi que le signe de comparaison sur lequel doit reposer la comparaison entre les champs liant la table parent à la table enfant.

Les signes de comparaison sont :

- .= Egalité parfaite entre le champ parent et le champ enfant
- .&gt; Ne seront affichés dans la liste enfant que les enregistrements dont la valeur est supérieure à l&#39;attribut de filtre parent.
- .&lt; Ne seront affichés dans la liste enfant que les enregistrements dont la valeur est inférieure à l&#39;attribut de filtre parent.

**Attendre le parent**

Pour forcer l&#39;affichage de la liste des éléments enfants uniquement lorsqu&#39;un élément parent est sélectionné, il faut cocher la case &#39;Attendre le parent&#39;. Ainsi, si aucun élément parent n&#39;est sélectionné, aucun élément enfant n&#39;apparaîtra dans la liste.

Exemple

On veut faire apparaître les sections d&#39;une commune sélectionnée préalablement.

Un premier paramètre nommé &#39;commune&#39; est créé. Il exploite les valeurs d&#39;une table &#39;commune&#39; d&#39;une base de données. Un deuxième paramètre nommé &#39;section&#39; est créé. Il exploite les valeurs d&#39;une table &#39;section&#39; de la même base.

Dans la fenêtre de la définition du paramètre &#39;section&#39;, après avoir lié le paramètre à la source de données, sélectionner la boîte à cocher &#39;cascade&#39; puis sélectionner le paramètre parent &#39;commune&#39; :

 ![](./)

Seules les 2 sections de la commune sélectionnée d&#39;Abeilhan apparaissent désormais dans la liste Section :

 ![](./)

 Appel externe

La section Appel externe permet l&#39;intégration dans une page html d&#39;un formulaire GTF. C&#39;est un moyen de donner accès à un projet GTF depuis une quelconque page web, sans avoir GTF installé sur son poste. La section Appel Externe du mode Projet permet de définir la façon dont l&#39;utilisateur final aura accès au formulaire GTF puis génère le code à intégrer directement dans la page html désirée.

L&#39;administrateur définit le type d&#39;accès souhaité au formulaire GTF :

- . soit via un bouton intégré dans la page Internet,
- . soit via l&#39;insertion telle quelle du formulaire GTF dans la page web.

Il associe ensuite un Titre au formulaire et dans le cas d&#39;un bouton, il spécifie le texte associé au bouton d&#39;accès du formulaire dans le champ &#39;Texte du bouton&#39;. La hauteur et largeur du formulaire peuvent également être paramétrées.

 ![](./)

_Appel externe_

Jetons de connexion

Un jeton agit comme une clé permettant d&#39;accéder à un formulaire GTF. Un jeton ne peut être donné qu&#39;à un utilisateur authentifié.

L&#39;administrateur a la possibilité d&#39;associer à un traitement un jeton privé ou un jeton public permettant l&#39;accès et l&#39;utilisation du formulaire GTF :

- .Le jeton public est l&#39;identifiant de connexion du compte PUBLIC défini au préalable par l&#39;administrateur dans le mode [Configuration](../../C:/margot2/svn/produit/gtf/doc/gtf_manuel_utilisateur/Content/gtf_manuel_utilisateur/11%20Configuration%20et%20proc%C3%A9dures%20d&#39;exploitation.htm#11.1.2)-716311482
- .Fournir un jeton privé est un moyen de donner accès à un compte de connexion à un traitement GTF particulier. Pour générer une clé privée, l&#39;administrateur saisit le login et mot de passe de l&#39;utilisateur pour lequel il souhaite générer un jeton privé puis définit une date de fin de validité de cette dernière. Après avoir cliqué sur le bouton &#39;Clé privée&#39;, la clé est retournée et intégrée dans le code à utiliser.

 ![](./)

Utilisation de CAPTCHA

Il est possible d&#39;intégrer un CAPTCHA au formulaire pour s&#39;assurer que la demande de traitement est bien générée par un être humain et non par un ordinateur.

 ![](./)
L&#39;insertion d&#39;un Captcha, nécessite l&#39;obtention d&#39;une clé sur le service Web de Google à l&#39;adresse [https://www.google.com/recaptcha/admin](https://www.google.com/recaptcha/admin). Une fois la clé obtenue, l&#39;administrateur saisit la clé fournie dans le champ Clé Recaptcha.

 ![](./)
La clé est directement intégrée dans le code généré par GTF. Le motif CAPTCHA est généré automatiquement à chaque demande de traitement.

6.1.6.3 Insertion du code généré

Le bouton &#39;Générer le code&#39; retourne le code à copier dans la page Html permettant d&#39;accéder au formulaire GTF. Le code contient le jeton de connexion défini au préalable (public ou privé), ainsi que le cas échéant la clé Captcha.

Exemple de code:

 ![](./)

Jeton de connexion public / Clé Captcha

Ce code est à insérer directement dans la page html à l&#39;emplacement désiré.

L&#39;exemple ci-dessous illustre l&#39;insertion d&#39;une fenêtre de demande de création de gex (traitement administration &#39;admin\_export&#39;) dans un page html :

 ![](./)



 Répertoire Projet

La section Répertoire projet permet de visualiser le contenu du répertoire contenant le projet FME ainsi que les ressourceS associées à ce dernier. Ce répertoire contient les copies systématiques des projets FME (renommés en .bak) dont les visualiseurs ont été désactivés.

En cas de chargement de projets fmw de même nom, l&#39;ancien projet est renommé en .bak.

Les ressources sont écrasées en cas de chargement de ressources de même nom. La date de dernière modification des fichiers est indiquée et permet de contrôler la bonne mise à jour des fichiers écrasés.

 ![](./)

 ![](./)
GTF détecte les formats de types multifichiers (Shape File, EDIGEO…) contenus dans un fichier compressé ZIP que l&#39;utilisateur uploade sur le serveur. Les fichiers sont automatiquement décompressés dans le répertoire projet.



Gestion des Transformers et formats personnalisés

FME stocke les formats et Transformers personnalisés dans des répertoires propres à chaque utilisateur identifiés par la variable d&#39;environnement %userprofile%.

- .Les Transformers personnalisés sont stockés dans le répertoire %userprofile%\Mes documents\FME\Transformers.
- . Les formats personnalisés sont stockés dans le répertoire %userprofile%\Mes documents\FME\Formats

De la sorte, chaque utilisateur dispose de son propre environnement de travail.

Dans GTF, un traitement FME est exécuté par le compte qui exécute le service Pycron, en général &#39;système local&#39;. Ce dernier ne dispose pas de répertoire utilisateur %userprofile% . FME ne peut donc pas localiser les fichiers des Transformers et des formats personnalisés. Le traitement ressortira en erreur.

Pour pouvoir être exploités, les formats et Transformers personnalisés doivent donc être installés manuellement (copiés) sur le serveur GTF dans les répertoires suivants :

- .Formats personnalisés ==&gt; $FME\_HOME\datasources
- .Transformers personnalisés ==&gt; $FME\_HOME\transformers

Gestion des connexions nommées

Les connexions nommées stockent les informations de connexions aux bases de données et services web. De la même manière que les formats et Transformers personnalisés, les connexions nommées sont stockées dans des répertoires propres à chaque utilisateur.

Elles sont ainsi stockées dans un fichier crypté &#39;namedConnections.data&#39; situé dans le répertoire %userprofile%\AppData\Roaming\Safe Software\FME\

Ce fichier doit pouvoir être accessible par un utilisateur réel via FME Workbench pour créer et gérer les connexions, mais il doit également pouvoir être utilisé par le compte système local, compte qui, dans GTF, exécute le service Pycron pour lancer un traitement FME.

Or, contrairement aux utilisateurs classiques, le compte système local ne dispose pas de répertoire personnel %userprofile%. Il ne peut donc pas exploiter les connexions nommées d&#39;un projet FME publié sur un serveur GTF.

Pour pouvoir exploiter les connexions nommées dans GTF, le fichier crypté des connexions nommées doit donc être localisé, puis une clé de registre doit ensuite être créée : elle indiquera l&#39;emplacement du fichier crypté, de sorte à en assurer son utilisation par tout compte ne disposant pas de répertoire personnel tel que le compte Système local.

- .Rendre publiques les connexions nommées désirées
- .Exporter les connexions nommées désirées dans un répertoire spécifique
- .Créer une clé de registre contenant le chemin du répertoire par défaut, stockant le fichier des connexions nommées
- .Tester

Rendre publiques les connexions nommées

Dans un premier temps, pour pouvoir être exploitables par d&#39;autres utilisateurs, les connexions nommées doivent être rendues publiques.

Dans FME, dans le Menu Outils-&gt;Options FME-&gt;Connexions aux bases de données, sélectionner les connexions nommées que vous souhaitez exporter (et les attribuer ensuite à un compte système local) puis cocher la case Public.

 ![](./)

Connexions nommées dans FME.

 ![](./)
La possibilité de rendre publique une connexion nommée a été implémentée dans la version FME 2016. Or, FME exploite des connexions nommées créées dans d&#39;anciennes versions. Dans ce cas, La colonne Public n&#39;apparaît pas dans la fenêtre des connexions. Pour contourner ce problème et afficher la colonne Public, exporter les connexions nommées dans un nouvel emplacement, supprimer les connexions initiales, puis les réimporter (Cf procédure 6.1.9.2).



Exporter des connexions nommées

Sélectionner la lou les connexions nommées que vous souhaitez exporter puis dans le menu contextuel, choisir Exporter.

 ![](./)

Export des connexions nommées.

Les connexions sélectionnées sont exportées dans un fichier xml : &#39;exportConnectionData\_x.xml&#39;. Choisir ensuite son emplacement.

 ![](./)

Dans FME, il est alors possible de modifier l&#39;emplacement du fichier des connexions nommées en indiquant le nouveau répertoire dans le menu Outils-&gt;Options FME-&gt;Chemins par défaut.

 ![](./)

Spécification du répertoire des connesions nommées.

Vous pouvez, par exemple, supprimer les connexions nommées d&#39;origine, puis importer celles que vous venez d&#39;exporter et remplacer de la sorte les connexions initiales.

Retourner dans le menu Outils-&gt;Options FME-&gt;Connexions aux bases de données et sélectionner &#39;Importer&#39; dans le menu contextuel dans la liste des connexions.

 ![](./)

Import de connexions nommées

 Sélectionner les connexions que vous souhaitez importer :

 ![](./)

Sélection des connexions nommées à importer

Les connexions nommées précédemment exportées sont à nouveau importées.

Dorénavant, 5 connexions nommées sont listées dans le menu Outils-&gt;Options FME-&gt;Connexions aux bases de données :

 ![](./)

Nouvelles connexions nommées

Création des clés de registre

 Pour pouvoir attribuer au compte système local le répertoire par défaut des connexions nommées (nouvellement importées), un fichier de registre cn32.reg (ou cn64.reg selon les versions de FME) doit être créé et contenir le chemin du répertoire stockant le fichier crypté des connexions.

---------------------------------------------------------------------------------------------------------------------------------------

Windows Registry Editor Version 5.00

[HKEY\_LOCAL\_MACHINE\SOFTWARE\WOW6432Node\Safe Software Inc.\Feature Manipulation Engine\Settings]

&quot;Named Connection Db Type&quot;=dword:00000000

&quot;Named Connection Directory&quot;=&quot;E:\\tmp\\connexion&quot;

----------------------------------------------------------------------------------------------------------------------------------------

Clé de registre cn32.reg à créer.



 ![](./)
_Les caractères &#39;\&#39;doivent être doublés._



Import de la clé de registre

Importer la clé de registre via la commande regedit-&gt;import ou par un double clic sur le fichier .reg.

- .cn32.reg contient la clé de registre pour FME 32 bits
- .cn64.reg contient la clé de registre pour FME 64 bits

 ![](./)



Test

Veremes met à disposition sur son [site de téléchargement](http://download.veremes.net/) le projet ListSettings.fmw qui génère un fichier texte (settings.txt) dans lequel sont listés les paramètres système FME du serveur tels que les builds , l&#39;interpréteur Python utilisé....

Pour vérifier l&#39;emplacement du répertoire des connexions nommés, exécuter le projet ListeSettings.fmw et s&#39;assurer que dans le fichier texte généré, le répertoire spécifié soit bien rajouté et correct :

---------------------------------------------------------------------------------

Settings:

Python:

Use Custom Python: false

Named Connection Db Type: 0

Named Connection Directory: E:\tmp\connexion

Statistics:

enabled: no

------------------------------------------------------------------------------------



Publier une connexion nommée

Un auteur de projet peut publier une connexion nommée. Avec GTF 2015 et 2016.0, pour publier une connexion nommée il est nécessaire de créer un paramètre publié de type TEXTE.

 ![](./)

Puis il faut associer ce paramètre publié au paramètre du Reader ou du Transformer concerné :

 ![](./)

 ![](./)
Avec GTF 2016.1, les paramètres publiés de type Connexion Nommée sont automatiquement reconnus et transformés en paramètre de type Texte.

Gestion des catégories

L&#39;attribution de catégorie à un traitement permet à l&#39;administrateur d&#39;organiser par thématique les traitements disponibles.

L&#39;onglet Catégorie du mode Publication permet d&#39;accéder au formulaire de création de catégorie dans lequel l&#39;administrateur nomme cette dernière et peut lui associer une description.

Gestion des dépôts (répertoire de surveillance) et des abonnements

 Abonnement à un traitement

 Un abonnement permet à un utilisateur d&#39;exécuter à fréquence régulière un projet.

Un auteur peut décider de rendre un traitement disponible pour abonnement ou pas.

Dans le menu Mon travail, onglet Abonnements, un utilisateur peut choisir de s&#39;abonner à un projet, à la fréquence de son choix, et peut choisir d&#39;être notifié par mail du bon déroulement ou pas du traitement. Il peut également saisir l&#39;adresse mail à laquelle envoyer la copie du mail.

Surveillance des dépôts

Un dépôt est un répertoire de surveillance.

Une surveillance correspond à un abonnement à un traitement en ajoutant un nouveau paramètre qu&#39;est la disponibilité d&#39;un fichier ou d&#39;un répertoire dans un dépôt préalablement défini par l&#39;administrateur.

 Ainsi, si un projet est rendu disponible pour surveillance, alors ce dernier est automatiquement exécuté (selon la période d&#39;abonnement définie) dès lors que GTF détecte la présence d&#39;un fichier dans le dépôt.

L&#39;onglet Dépôt permet à l&#39;administrateur de consulter la liste des dépôts, d&#39;en créer et d&#39;en supprimer.

 Il crée des nouveaux dépôts en spécifiant le chemin du répertoire à surveiller **qu&#39;il aura préalablement créé sur le serveur. **

La stratégie d&#39;attribution de dépôt se fait à l&#39;échelle du groupe d&#39;utilisateurs. Un utilisateur en ayant-droit,  peut alors associer à un traitement une surveillance dans un dépôt. GTF scrute la présence de fichiers dans le dépôt.  Si un fichier est présent, alors le traitement est lancé en exploitant le fichier.

Le bouton &#39;Ajouter un dépôt&#39; permet d&#39;accéder au formulaire de création de dépôt en spécifiant le chemin du répertoire à surveiller, un alias et les groupes y ayant accès. Il clique ensuite sur &#39;Créer&#39; pour valider sa création et rendre le dépôt disponible pour les groupes en ayant droit.

 ![](./)

Formulaire de création de dépôt.

 ![](./)
GTF personnalise automatiquement le dépôt en fonction du compte utilisateur de connexion en suffixant le dépôt avec la variable $user. L&#39;utilisateur final ne voit ainsi que son propre répertoire dans le dépôt. Au préalable, l&#39;administrateur doit avoir créé dans chaque dépôt, un répertoire par utilisateur (des groupes ayant accès à chaque dépôt). Le nom du répertoire doit être parfaitement identique au compte de connexion qu&#39;il s&#39;agisse d&#39;un utilisateur « PostgreSQL » ou importé d&#39;Active Directory.



Gestion des périodes

Un abonnement permet de s&#39;inscrire à un traitement répété au cours du temps selon une fréquence choisie.

Dans l&#39;onglet Périodes, l&#39;administrateur peut accéder au formulaire de définition des périodes d&#39;abonnement. Le bouton &#39;Ajouter période&#39; permet à l&#39;administrateur de définir une nouvelle période d&#39;abonnement en lui affectant un libellé puis en y insérant le code correspondant.

Il est ensuite possible de tester le bon déroulement de l&#39;ajout de Période en cliquant sur le bouton &#39;Test&#39;. Le bouton &#39;Créer&#39; finalise le processus de création d&#39;une période.

Pycron est le composant assurant l&#39;exécution des tâches à heures fixes. L&#39;instruction à saisir doit respecter la syntaxe de la fonction contrab. Pour plus d&#39;information sur le programme crontab et la syntaxe à respecter, consulter le site : http://fr.wikipedia.org/wiki/Crontab

Modèles d&#39;E-mail

L&#39;onglet Modèles-email du mode Publication permet la création de modèles d&#39;e- mail envoyé après exécution d&#39;un traitement. Via cette onglet, l&#39;administrateur (ou l&#39;auteur) a la possibilité de personnaliser un e-mail, en définissant la ou les personnes destinataires, les circonstances d&#39;envoi de ce dernier ainsi que son contenu. Il choisit ensuite pour chaque modèle, la définition à utiliser.

Chaque traitement est associé à un modèle d&#39;e-mail.

L&#39;onglet Informations générales permet de créer un nouveau modèle de mail, en le nommant et en définissant son contexte à GTF et de définir le type de définition de ce dernier :

Définition simple

 L&#39;administrateur exploite les balises disponibles pour personnaliser le corps du mail.

| Nom de la balise |  descriptif | code correspondant |
| --- | --- | --- |
| [order.order\_id] | Identifiant de la demande de traitement | $properties[&#39;order.order\_id&#39;][&#39;value&#39;] = $this-&gt;aObjects[&quot;oOrder&quot;]-&gt;aFields[&#39;order\_id&#39;]; |
| [order.order\_date] | Date et heure de la demande de traitement | $properties[&#39;order.order\_date&#39;][&#39;value&#39;] = $this-&gt;aObjects[&quot;oOrder&quot;]-&gt;aFields[&#39;order\_date&#39;]; |
| [order.execution\_date] | Date et heure de fin de traitement | $properties[&#39;order.execution\_date&#39;][&#39;value&#39;] = $this-&gt;aObjects[&quot;oOrder&quot;]-&gt;aFields[&#39;order\_execution\_date&#39;]; |
| [order.result\_url] | Adresse de téléchargement du résultat du traitement | $properties[&#39;order.result\_url&#39;][&#39;value&#39;] = $this-&gt;aObjects[&quot;oOrder&quot;]-&gt;aFields[&#39;result\_url&#39;]; |
| [order.log\_url] | Adresse du log du traitement | $properties[&#39;order.order\_log&#39;][&#39;value&#39;] = $this-&gt;aObjects[&quot;oOrder&quot;]-&gt;aFields[log\_url&#39;]; |
| [order.length\_sec] | Durée du traitement en secondes | $properties[&#39;order.length\_sec&#39;][&#39;value&#39;] = $this-&gt;aObjects[&quot;oOrder&quot;]-&gt;aFields[length\_sec&#39;]; |
| [order.email\_notifications] | Adresse Email du destinataire en copie de mail | $properties[&#39;user.email&#39;][&#39;value&#39;] = $this-&gt;aObjects[&quot;oOrder&quot;]-&gt;getUser()-&gt;aFields[&#39;email&#39;]; |
| [gtf\_engine. Name] | Nom du moteur GTF | $this-&gt;aObjects[&quot;oOrder&quot;]-&gt;getGtfEngine()-&gt;aFields[&#39;name&#39;]; |
| [fme\_engine.name] | Nom du moteur FME  utilisé | $this-&gt;aObjects[&quot;oOrder&quot;]-&gt;getFmeEngine()-&gt;aFields[&#39;name&#39;]; |
| [order.user.name] | Nom du demandeur de traitement | $properties[&#39;user.name&#39;][&#39;value&#39;] = $this-&gt;aObjects[&quot;oOrder&quot;]-&gt;getUser()-&gt;aFields[&#39;name&#39;]; |
| [order.user\_email] | Adresse mail du demandeur de traitement | $properties[&#39;user.email&#39;][&#39;value&#39;] = $this-&gt;aObjects[&quot;oOrder&quot;]-&gt;getUser()-&gt;aFields[&#39;email&#39;]; |
| [order.user.login] | Compte de connexion du demandeur | $properties[&#39;user.login&#39;][&#39;value&#39;] = $this-&gt;aObjects[&quot;oOrder&quot;]-&gt;getUser()-&gt;aFields[&#39;login&#39;]; |
| [order.worksapce.category.name] | Catégorie du traitement | $properties[&#39;catgory.name&#39;][&#39;value&#39;] = $this-&gt;aObjects[&quot;oOrder&quot;]-&gt;getWorkspace()-&gt;getCategory()-&gt;aFields[&#39;email&#39;]; |
| [order.workspace.name] | Nom du traitement | $properties[&#39;order.workspace.name&#39;][&#39;value&#39;] = $this-&gt;aObjects[&quot;oOrder&quot;]-&gt;getWorkspace()-&gt;aFields[&#39;name&#39;]; |
| [worksapce.fmw\_file] | Nom du projet FME | $properties[&#39;order.workspace.fmw\_file&#39;][&#39;value&#39;] = $this-&gt;aObjects[&quot;oOrder&quot;]-&gt;getWorkspace()-&gt;aFields[&#39;fmw\_file&#39;]; |

 ![](./)
_La balise [order.email\_notifications] doit être insérée dans les champs CC et CCi de sorte à ce qu&#39;une notification de traitement soit envoyée aux adresses mail définies dans le formulaire de demande de traitement dans le champ &#39;Envoyer une copie de l&#39;e-mail à&#39; :_

 ![](./)

 ![](./)
_Lorsque plusieurs destinataires doivent être en copie du mail de notification, séparer les adresses mail par un retour charriot._



Définition avancée

L&#39;administrateur saisit directement le code du mail. Il peut, pour cela, utiliser le code généré via l&#39;édition simple en cliquant sur le bouton Générer le code à partir de l&#39;édition simple.



 Exemples de publication de traitements

Traitement de conversion d&#39;un fichier statique sur le serveur

**Objectif **

Création d&#39;un traitement simple de conversion d&#39;un fichier Shape, disponible sur le serveur, en fichier MapInfo, avec publication du répertoire destination à créer.

Le fichier source est statique (toujours le même) et il se trouve à un emplacement quelconque du serveur. L&#39;emplacement du jeu de données sur le serveur est défini dans le paramètre source dans FME et ce paramètre est dépublié.

  Création du projet FME

- .Lancer FME Workbench
- .Cliquer sur Fichier &gt; Nouveau&gt; Générer un projet
- .Indiquer le fichier Shape en source et le format Mapinfo en sortie. Cocher Schéma statique puis cliquer sur OK.

 ![](./)

Après validation, un projet simple de conversion d&#39;un fichier Shape vers un fichier MapInfo est généré.

 ![](./)

Par défaut, deux paramètres sont publiés : &#39;sourceDataset\_SHAPE&#39; et &#39;DestDataSet\_MAPINFO&#39;.

 ![](./)

**Chaque paramètre publié d&#39;un projet FME génère une entrée dans le formulaire GTF.** Dans cet exemple, le formulaire GTF permet de modifier le répertoire source et le répertoire destination. Or nous souhaitons que GTF ignore la publication des données sources, empêchant les utilisateurs finaux  de sélectionner et modifier les fichiers sources.

- .Supprimer la publication du paramètre [SourceDataset\_SHAPE] pour forcer les utilisateurs à utiliser le fichier Shape mis à disposition sur le serveur.
- .Editer si désiré, le paramètre publié DestDaraset\_MAPINFO

  ![](./)

- .Enregistrer le projet, par exemple sous le nom &#39;extraction\_departements.fmw&#39;.

Avant de publier ce projet dans GTF, il convient de le tester localement. Lancer le traitement depuis FME Workbench, vérifier le bon déroulement du traitement et s&#39;assurer que  le résultat soit correctement généré.

Publication du traitement dans GTF

- .Se connecter à GTF.
- .Dans le menu Publication, cliquer sur « Ajouter Projet FME ». Donner un nom au traitement, par exemple, &#39;Conversion\_dept\_shp2mapinfo&#39;.Cliquer sur **Parcourir** et charger le projet FME. Choisir de ne pas  rendre ce traitement disponible sur abonnement et ni pour une surveillance. Sélectionner le mot clé associé au moteur GTF désiré. Cliquer sur « Créer ».

 ![](./)

- .Dans la section  &#39;Droits&#39;, associer un groupe au traitement et cliquer sur « Mettre à jour ».
- .Dans la section Formulaire, visualiser le formulaire publié par défaut. Constater que le paramètre publié source du projet FME n&#39;est pas publié et que  seul le paramètre «Nom du dossier Destination MapInfo » est publié. La valeur par défaut configurée dans FME a été importée.

 ![](./)

  Exécution du traitement

- .Dans le Mode &#39;Mon travail&#39;  cliquer sur &#39;Ajouter demande&#39;, et choisir le traitement préalablement publié « Extraction Départements».

 ![](./)

- .Cliquer sur &#39;Demander&#39;. La demande de traitement est créée et celle-ci est en attente de traitement.

- .Une fois traité, le voyant passe au vert. Le résultat est téléchargeable.

 ![](./)

Le fichier ZIP généré contient un répertoire «Mon résultat» contenant les fichiers MapInfo générés par le traitement.

  Ajout de Paramètres publiés supplémentaires

**Objectif **

Compléter le projet exemple n°1. Publication d&#39;un paramètre publié supplémentaire pour spécifier une emprise d&#39;extraction de données.

 Création du projet FME

- .Ouvrir le précédent projet &#39;extraction-departements.fmw&#39; dans FME Workbench. Dans le Navigateur, publier les 4 paramètres : X minimum, Y minimum, X maximum et Y maximum des données sources. Entrer les valeurs par défaut correspondant à l&#39;emprise de l&#39;ensemble des données, par exemple : X minimum = 50000 ; X maximum = 1 200 000 ; Y minimum = 1 700 000 ; et Y maximum = 2 700 000.

 ![](./)

- .Enregistrer le projet **extraction\_depts\_emprise.fmw**

 Publication du traitement dans GTF

- .Se connecter à GTF.
- .Dans le menu Publication, cliquer sur « Ajouter Projet FME ». Donner un nom au traitement GTF, par exemple, &#39;extraction depts emprise&#39;. Aucune ressource complémentaire ne doit être chargée puisque la donnée source est intégrée dans le projet FME. Choisir de ne pas  rendre ce traitement disponible sur abonnement ni pour une surveillance. Sélectionner le mot clé associé au moteur GTF désiré. Cliquer sur « Créer ». Dans la section  &#39;Droits&#39;, associer un groupe au traitement et cliquer sur « Mettre à jour ».

 ![](./)

- .Dans la section Formulaire, visualiser le formulaire publié par défaut. Constater que les 4 paramètres de l&#39;emprise apparaissent dans le formulaire avec les valeurs par défaut définies dans le projet FME.

 ![](./)

 Exécution du traitement

- .Dans le mode &#39;Mon travail&#39;  cliquer sur &#39;Ajouter demande&#39;, et choisir le traitement préalablement publié « Extraction Département emprise».
- .Indiquer comme valeurs d&#39;emprise X min = 500 000, Y min = 2  000 000, X max = 1 000 000 et Y max = 2 500 000, et &#39;Mon\_résultat\_emprise&#39; comme nom de répertoire destination.

 ![](./)

- .Cliquer sur &#39;Créer la Demande&#39;.
- .Une fois la demande traitée (voyant vert), télécharger le ZIP généré.

 ![](./)
Remarquer que le nom ZIP correspond à l&#39;identifiant de la demande de traitement : par exemple 19.zip pour la demande n°19. Ce numéro est unique car issu d&#39;une séquence PostgreSQL.



- .Ouvrir le fichier MapInfo généré dans FME Data Inspector et constater que les données ont été extraites selon l&#39;emprise spécifiée.

 ![](./)

 Conversion de fichiers sources statiques chargés sur le serveur lors du chargement du projet FME

**Objectif**

Le fichier source est statique et il est chargé sur le serveur par GTF comme ressource du projet FME. Les utilisateurs finaux n&#39;uploadent pas de fichiers sources, ils se trouvent sur le serveur au même endroit que le projet FME.

Il s&#39;agit ainsi de reconstituer la même arborescence que celle du poste de développement.

 Création du projet FME

- .Créer un nouveau projet FME pour convertir un fichier Shape vers un fichier MIF/MID.

  ![](./)



- .Deux paramètres doivent être publiés : la source et la destination. La source pointe vers un fichier Shape en local. Pour que GTF puisse accéder à ce fichier, il faut uploader le fichier shape et ses dépendances sur le serveur GTF. Ces données seront stockées dans le même répertoire que le projet FME lors de la création du traitement dans GTF.
- .Modifier le chemin de la source comme tel :

  ![](./)

 ![](./)



- .Les données sources étant fixes, il convient de dépublier ce paramètre, en cliquant sur Supprimer le lien du paramètre publié.

 ![](./)

- .Enregistrer le projet.

  Publication du traitement dans GTF

- .Se connecter à GTF.
- .Dans le menu Publication, cliquer sur « Ajouter Projet FME ». Donner un nom au traitement GTF, par exemple &#39;Conversion\_dept\_shp2mif&#39;.Charger le projet FME. Choisir de ne pas  rendre ce traitement disponible sur abonnement ni pour une surveillance. Sélectionner le mot clé associé au moteur GTF désiré puis dans la section Droits associer un groupe au projet.
- .Pour uploader le fichier Shape et ses dépendances, compresser les fichiers dans un fichier ZIP. Dans le champ &#39; **Ressources complémentaires**&#39; cliquer sur Parcourir et chercher le fichier ZIP précédemment créé. Cliquer sur « Créer ».

 ![](./)



**Ces ressources complémentaires sont décompressées dans le répertoire contenant le projet .fmw.** L&#39;arborescence du poste de développement est ainsi reconstituée sur le serveur.

 La section Répertoire Projet permet de visualiser l&#39;intégralité du répertoire projet du serveur :

 ![](./)

- .Dans la section Formulaire, visualiser le formulaire publié par défaut. Constater que seul le fichier destination est paramétrable. Le fichier des départements dpts.shp est automatiquement associé au projet.

 ![](./)

 Exécution du traitement

- .Dans le Mode &#39;Mon travail&#39;  cliquer sur &#39;Ajouter une demande&#39;, et choisir le traitement préalablement publié « conversion\_dept\_shp2mif».
- .Indiquer le nom répertoire à créer en destination. Cliquer sur Créer la demande.
- .Une fois la demande traitée (voyant vert), télécharger le ZIP généré.

 ![](./)
Remarquer que le nom ZIP correspond à l&#39;identifiant de la demande de traitement : par exemple 19.zip pour la demande n°19. Ce numéro est unique car issu d&#39;une séquence PostgreSQL.



  Traitement de conversion avec sortie générique

**Objectif **

Publication d&#39;un traitement de conversion d&#39;un fichier dont le format destination est générique. L&#39;utilisateur final choisit le format destination. Le fichier source au format shape est statique.

 Création du projet FME

- .Ouvrir le traitement créé dans l&#39;exercice n°2 &#39;extraction\_depts\_emprise.fmw&#39; dans FME Workbench. Supprimer le jeu de données destination MapInfo et ajouter un nouveau jeu de données au format &#39;Generic&#39;. Indiquer une destination temporaire.

 ![](./)

- .Cliquer sur le bouton **Paramètres** et choisir le format de sortie MapInfo :

 ![](./)

- .Dupliquer le type d&#39;entités source, par un clic droit en choisissant l&#39;option &quot;Dupliquer&quot;
- .Publier le paramètre « Système de coordonnées » du jeu de données Generic.

 ![](./)



Le format Generic permet de spécifier le format de destination via un paramètre. Le paramètre « GENERIC\_OUT\_FORMAT\_GENERIC » est publié par défaut. GTF ne supporte pas ce paramètre car tous les formats supportés par FME devraient être listés.

- .Dans un premier temps, il faut donc dépublier ce paramètre par un clic droit &gt; Supprimer.

 ![](./)

- .Il faut ensuite créer sa propre liste de formats dans un nouveau paramètre publié : ajouter un nouveau paramètre publié que vous nommerez &#39;FORMAT&#39; de type &#39;choix&#39; et saisir les formats destination désirés.

 ![](./)

 ![](./)



- .Associer ensuite le paramètre &#39;FORMAT&#39; au jeu de données générique. Faire un clic droit sur le paramètre &#39;Format en sortie&#39; et choisir &#39;Lier au paramètre publié&#39;.

 ![](./)



- .Enregistrer le projet, par exemple « shape2generic.fmw »

Publication du traitement dans GTF

- .Se connecter à GTF.
- .Dans le menu Publication, cliquer sur « Ajouter Projet FME ». Donner un nom au traitement GTF, par exemple &#39;Extraction départements avec choix de l&#39;emprise et du format destination&#39;. Aucune ressource complémentaire ne doit être chargée puisque la donnée source est intégrée dans le projet FME. Choisir de ne pas  rendre ce traitement disponible sur abonnement et ni pour une surveillance. Sélectionner le mot clé associé au moteur GTF désiré. Cliquer sur « Créer ». Dans la section  &#39;Droits&#39;, associer un groupe au traitement et cliquer sur « Mettre à jour ».

 ![](./)

- .Dans la section Formulaire, visualiser le formulaire publié par défaut. Constater que  le paramètre Format destination est bien associé au projet.

 ![](./)

 Exécution du traitement

- .Dans le mode &#39;Mon travail&#39;, cliquer sur &#39;Ajouter demande&#39;, et choisir le traitement préalablement publié « Extraction départements avec choix de l&#39;emprise et du format destination».
- .Indiquer le fichier ZIP source et le répertoire destination. Cliquer sur Créer la demande.
- .Une fois la demande traitée (voyant vert), télécharger le ZIP généré.

 ![](./)
Remarquer que le nom ZIP correspond à l&#39;identifiant de la demande de traitement : par exemple 19.zip pour la demande n°19. Ce numéro est unique car issu d&#39;une séquence PostgreSQL.



 Personnalisation de formulaire : exploitation du contrôle de type Carte OSM.

**Objectif**

Extraction de types d&#39;entités à partir d&#39;une zone d&#39;emprise saisie graphiquement sur une carte OSM par l&#39;utilisateur final. Modification du formulaire directement dans GTF.

 Création du projet FME

Créer un nouveau projet FME pour extraire un fichier GeoFla au format Esri Shape avec un paramètre qui permet de choisir une zone d&#39;extraction sous la forme d&#39;un polygone décrit par une chaîne WKT.

 ![](./)

Dans FME, 3 paramètres sont publiés :

- .Zone d&#39;extraction WKT : chaîne de caractères WKT pour définir la zone d&#39;extraction. (Paramètre publié de type Texte)
- .Couches à extraire : choix du type d&#39;entités à extraire (COMMUNES, CANTONS, DEPARTEMENTS…). (Paramètre publié de type Choix)
- .Nom du Répertoire Destination à créer. (Paramètre publié de type Répertoire en sortie)

 ![](./)

 Publication du traitement dans GTF

- .Se connecter à GTF.
- .Dans le menu Publication, cliquer sur « Ajouter Projet FME ». Donner un nom au traitement GTF, par exemple &#39;Extraction GeoFla&#39;. Entrer ensuite une description et attribuer une catégorie. Choisir de ne pas  rendre ce traitement disponible sur abonnement et ni pour une surveillance.
- .Pour uploader les fichiers GeoFla au format Shape, compresser les fichiers dans un fichier ZIP. Dans le champ &#39;Ressources complémentaires&#39; cliquer sur Parcourir et chercher le fichier ZIP précédemment créé. Cliquer sur « Créer ». Dans la section  &#39;Droits&#39;, associer un groupe au traitement et cliquer sur « Mettre à jour ».

 ![](./)

- .Dans la section Formulaire, visualiser le formulaire publié par défaut. Constater que les 3 paramètres sont bien affichés.

 ![](./)

Personnalisation du formulaire

La saisie de la zone d&#39;extraction sous la forme d&#39;une chaîne de caractères WKT n&#39;est pas simple. Une alternative serait de proposer à l&#39;utilisateur final la possibilité de saisir manuellement la zone d&#39;extraction de son choix en dessinant ses contours directement sur une carte. GTF permet l&#39;exploitation de contrôles de type carte :

- .Carte OSM
- .Carte Bing
- .Carte Veremap

Dans notre exemple, nous proposons d&#39;exploiter la carte OSM qui ne nécessite pas de clé.

Il est donc nécessaire de personnaliser le formulaire en cliquant sur le bouton ![](./)
 dans la fenêtre Formulaire.



- .Dans la fenêtre Paramètres publiés, sélectionner ensuite le paramètre &#39;wktPolygon&#39; de type Texte que vous souhaitez convertir en contrôle de type Carte OSM.
- .Dans la fenêtre Définition, sélectionner dans la liste, le contrôle de type &#39;Carte OSM&#39;.

 ![](./)

- . Ajuster les paramètres d&#39;affichage de la carte en définissant un libellé, par exemple &quot;Dessiner la zone d&#39;extraction&quot;, la largeur/hauteur de la carte, son échelle et projection, les coordonnées de son centre, ainsi que les outils qui seront affichés dans le formulaire de demande.

-
.Cliquer ensuite sur le bouton &#39;Sauvegarder le formulaire personnalisé&#39; ![](./)
 puis sur le bouton de publication de ce dernier
 ![](./)
.
 puis sur le bouton de publication de ce dernier ![](./)
.
.
- .S&#39;assurer que le formulaire a bien été mis à jour et que le paramètre &#39;Zone d&#39;extraction WKT&#39; a été remplacé par un paramètre permettant la saisie du périmètre d&#39;extraction directement sur une carte OSM.

Exécution du traitement

- .Dans le Mode &#39;Mon travail&#39;  cliquer sur &#39;Ajouter demande&#39;, et choisir le traitement préalablement publié « Extraction GeoFla ».
- .Indiquer les couches à extraire, le  répertoire destination et saisir directement sur la carte la zone d&#39;extraction. Cliquer ensuite sur Créer la demande.
- .Une fois la demande traitée (voyant vert), télécharger le ZIP généré.

 ![](./)

Supervision

On entend par &#39;supervision&#39; le suivi des demandes de traitements, des abonnements et des surveillances de tous les utilisateurs GTF. A tout moment, l&#39;administrateur doit pouvoir consulter la liste des demandes de projets émises par tous les utilisateurs, en supprimer certaines, identifier les erreurs et obtenir une vision synthétique de l&#39;utilisation de l&#39;application.

Il dispose pour cela du mode &#39;Supervision&#39; dans lequel est listé l&#39;ensemble des traitements demandés, des abonnements et des surveillances.

 Supervision des Demandes

L&#39;onglet &#39;Demandes&#39; offre à l&#39;administrateur une vision de l&#39;état du serveur. Il a une connaissance fine de l&#39;ensemble des traitements demandés par utilisateur, des dates de demandes, des priorités ainsi que le numéro de moteur ayant traité chaque projet. Il peut télécharger les résultats des traitements, consulter les paramètres des traitements et consulter les logs FME associés. Le champ &#39;Supprimé&#39; lui permet d&#39;être informé de la suppression d&#39;une demande par un utilisateur et le champ &#39;Etat&#39; permet, via un code couleur, d&#39;identifier si une demande est en attente, en erreur, traitée, non traitable, en cours de traitement ou non autorisée.

 ![](./)

L&#39;administrateur dispose de différents boutons d&#39;administration : le bouton &#39;Réinitialiser&#39;  lui permet de relancer un (ou des) traitement(s) sélectionné(s).

 Suppression des demandes

L&#39;administrateur est responsable de la suppression définitive des demandes une fois que ces dernières ont été supprimées par les utilisateurs. Il existe ainsi deux niveaux de suppression :

- .La suppression utilisateurs
- .La suppression définitive par l&#39;administrateur

Le bouton &#39;Purger les demandes&#39; permet à l&#39;administrateur de procéder à la suppression définitive d&#39;une demande de traitement préalablement supprimée par un utilisateur.

Le bouton &#39;Supprimer les demandes&#39; permet de supprimer les demandes des traitements sélectionnés.

 Modification des moteurs

L&#39;administrateur peut choisir de modifier le moteur d&#39;exécution d&#39;un (ou des) traitement(s) préalablement sélectionné(s) en cliquant sur le bouton &#39;Modifier le moteur&#39;.  En cas d&#39;échec de traitement, modifier le moteur est une bonne méthode pour identifier l&#39;origine du problème et comprendre si la configuration des versions de moteurs FME en est à l&#39;origine.

 ![](./)

 Supervision des abonnements

L&#39;onglet Abonnement permet à l&#39;administrateur de consulter la liste des abonnements aux projets FME et d&#39;identifier ceux étant actifs et inactifs. Il peut choisir de supprimer définitivement un abonnement en cliquant sur « Supprimer les abonnements ».

  Supervision des surveillances

De la même façon, l&#39;onglet Surveillance permet à l&#39;administrateur de consulter la liste des demandes de surveillance créées par les utilisateurs.

Il peut choisir de supprimer définitivement une surveillance : après avoir sélectionné le ou les abonnements à supprimer, il clique sur le bouton « Supprimer les abonnements ».

 Gestion des messages

Le projet GTFMessageSender, disponible sur notre site de téléchargement [http://download.veremes.com](http://download.veremes.com/) (répertoire gtf/gex) permet à un traitement FME d&#39;envoyer un message à GTF, et de déclencher des actions via l&#39;application [Workflow Application Builder for FME](http://www.veremes.com/produits/wab).

Les messages sont destinés à être exploités par WAB mais ils sont consultables dans le mode Supervision de GTF.

Exemple

GTFMessageSender peut être utilisé pour envoyer des messages suite à un contrôle des géométries d&#39;un fichier source. En fin de traitement, un message est envoyé à GTF.

Deux types de messages peuvent être envoyés selon la présence ou non d&#39;erreur dans le fichier source. Deux classes peuvent être créées : &#39; traitement ok&#39; et &#39;traitement Ko&#39; qui enclenchent chacune des traitements spécifiques dans WAB . Dans GTF, l&#39;administrateur pourrait ainsi consulter la liste des messages envoyés par GTFMessageSender, leur classe et corps, leur date de création et l&#39;expéditeur.

  Statistiques

Le mode Statistiques permet aux administrateurs d&#39;avoir une vision graphique et synthétique de l&#39;utilisation des ressources de GTF, moteur, traitement, temps machine, par date et/ou utilisateur à travers des graphiques et des tableaux de synthèse.

L&#39;affichage des statistiques peut être graphique ou tabulaire (export dans Excel) et il est possible d&#39;obtenir une représentation journalière, hebdomadaire, mensuelle et annuelle de l&#39;activité sur le serveur à partir d&#39;une date spécifiée en paramètre.

La liste déroulante Variable permet de choisir la variable devant être représentée dans les tableaux ou graphiques :

- .Nombre de traitements exécutés
- .Temps total des traitements
- .Durée des traitements par projet FME

Pour les deux dernières variables, le temps total des traitements et le temps par projet peuvent être représentés par :

- .Seconde
- .Minute
- .Heure
- .Pourcentage  du temps total d&#39;utilisation

L&#39;administrateur choisit ensuite de regrouper ces variables par :

- .Utilisateur
- .Projet FME
- .Etat du traitement (traitement en erreur ou traité)
- .Moteur utilisé

Puis il  choisit la période d&#39;analyse et la date à partir de laquelle produire les statistiques :

- .Jour
- .Semaine
- .Mois
- .Année

Le&#39; Nombre d&#39;éléments max&#39; permet de n&#39;afficher que les éléments les plus importants en termes de durée ou de nombre, les autres étant regroupés dans  la classe Autres. Dans l&#39;exemple ci-dessous, il a été choisi de n&#39;afficher que 2 éléments maximum : les traitements &#39;Conversion de fichier&#39; et &#39;extraction ZI&#39; sont les deux traitements les plus longs, ils sont donc affichés et détaillés ; tous les autres traitements sont regroupés dans la classe &#39;autres&#39;.

 ![](./)

Il est possible de tronquer les libellés pour réduire la taille de la légende et des info-bulles.

 ![](./)
Il est possible d&#39;augmenter le niveau de détail  directement dans le graphique, en cliquant sur une barre d&#39;histogramme. Le niveau d&#39;analyse s&#39;affine, passant, selon les cas, de l&#39;année au mois, à la semaine, au jour et aux heures. Inversement, un clic droit&gt; zoom out,  sur une barre d&#39;histogramme permet de passer à une analyse statistique plus large passant, selon les cas, des heures, au jour, au mois et à l&#39;année.



 ![](./)

 ![](./)

 ![](./)

 ![](./)

  Journaux (logs)

  Consultation des fichiers de logs de l&#39;application

Le mode Logs permet d&#39;accéder à l&#39;ensemble des fichiers de logs Apache, Pycron, Php, GTF et web.

L&#39;administrateur a la possibilité de supprimer les fichiers en fonction de leur ancienneté.

 Configuration et procédures d&#39;exploitation

 Configuration de l&#39;application

Le mode Configuration permet d&#39;éditer les paramètres de configuration stockés dans des fichiers de type &quot;properties&quot; et de consulter l&#39;état de l&#39;application.

 Paramètres généraux de configuration

La section Configuration permet de consulter et modifier les paramètres généraux de l&#39;application. Organisée en rubriques cette section permet l&#39;édition des paramètres généraux de l&#39;application, des serveurs HTTP, des paramètres de gestion d&#39;écriture des logs et de sécurité, et la consultation des informations relatives à la base de données.

 ![](./)
La taille maximale de fichier uploadé est définie par défaut à 100 Mo. Pour augmenter cette valeur, il est nécessaire de modifier les 2 properties &#39;upload\_max\_filesize&#39; et &#39;post\_max\_size&#39; du fichier de configuration php.ini avant de configurer cette valeur directement dans le mode configuration de GTF.



L&#39;administrateur personnalise l&#39;application et améliore ses performances en déterminant les délais d&#39;expiration de l&#39;interface graphique, les taillles maximales des fichiers uploadés sur le serveur, ainsi que le type fichiers interdits...

 Il définit également l&#39;emplacement du répertoire temporaire exploité par GTF

 Stratégie de sécurité : configuration du compte public et gestion des groupes

La partie Sécurité de la section Configuration permet de définir un compte de connexion Public pour lequel un jeton de connexion doit être associé.

Le jeton de connexion est l&#39;identifiant de connexion appelant un service GTF, intégré directement dans une page Internet. Créer un compte public avec son jeton de connexion est un moyen simple pour un administrateur de donner accès à un formulaire GTF  à un utilisateur avec un minimum de droits.

L&#39;administrateur choisit dans la liste déroulante quel compte est le compte public, il saisit ensuite son mot de passe, puis nomme le jeton tel qu&#39;il le souhaite :

 ![](./)
Le jeton de connexion public doit être une chaîne de caractères non vide et sans espace.

 ![](./)



Le bouton &#39;Autoriser les connexions avec le compte PUBLIC&#39; permet d&#39;activer/désactiver l&#39;accès aux services GTF du compte PUBLIC.

La partie sécurité de section sécurité permet la configuration de la gestion mixte des utilisateurs.

 Gestion des journaux

Cette section permet de définir les journaux à générer, la période de journalisation ainsi que la taille maximale en Ko d&#39;un fichier de log au delà de laquelle ce dernier ne pourra s&#39;afficher dans l&#39;interface.

Version des composants

La section Version permet de consulter le numéro de version de GTF et le build installé. L&#39;état des composants installés est consultables ainsi que les informations relatives au serveur et serveur web.

 Informations PHP

La section PHP Info permet de consulter les paramètres de la version PHP installée.

Fichier de licence FME

Cette section licence permet de faire une demande de fichier de licence, de l&#39;installer puis de l&#39;activer.

Le bouton « Demande de fichier de licence » permet d&#39;envoyer au service administratif de Veremes une demande de génération de fichier de licence. Indiquer le numéro de licence fourni dans l&#39;accusé de réception de votre commande, ainsi que l&#39;adresse mail à laquelle le fichier doit être envoyé.

Une fois obtenu,  indiquer l&#39;emplacement du fichier de licence délivré par Veremes dans le champ &#39;Fichier .txt&#39;, puis cliquer sur « Activer ».

Configuration du module GTF

 Cette section permet l&#39;édition des paramètres de configuration spécifiques au module GTF.

Le répertoire du Pycron est à définir dans le champ &#39;Répertoire de Pycron&#39;, ainsi que le modèle d&#39;e-mail utilisé par défaut pour l&#39;envoi des notifications des résultats des traitements.

On peut exclure des formats de la compression en définissant les extensions de fichiers non compressibles.

 ![](./)
Les formats de fichiers uniques tels que .xls, .html, .htm sont par défaut non compressibles.



Configuration du serveur SMTP

Les paramètres du serveur SMTP sont configurables dans cette rubrique.

L&#39;adresse mail et le nom de l&#39;expéditeur des mails de notification sont définis ainsi que le nom du serveur SMTP et le port qu&#39;il utilise.

L&#39;authentification SMTP permet de définir si l&#39;expéditeur peut envoyer des mails sans avoir à s&#39;authentifier. Si une authentification est requise, alors le compte SMTP et le mot de passe SMTP doivent être renseignés.

Configuration des moteurs GTF

L&#39;administrateur de GTF peut définir les heures creuses d&#39;exécution des moteurs au format &#39;hh:mm&#39; ainsi que le nombre maximum de demandes exécutées en même temps.

Configuration des répertoires Public et Upload

Les répertoires Upload et Public, installés dans le répertoire d&#39;installation de GTF, stockent respectivement les ressources chargées avec un projet et les résultats d&#39;un traitement. Il est possible de déplacer ces deux répertoires sur un autre disque et d&#39;assurer de la sorte une répartition des données pour faciliter les processus de sauvegarde.

Pour cela, l&#39;administrateur doit opérer en deux étapes :

- .Dans le fichier de configuration properties\_post.inc du répertoire .\gtf.client, modifier les deux properties :

$properties[&#39;upload\_dir&#39;] = $properties[&#39;gtf\_home&#39;] . &#39;/upload&#39;;

$properties[&#39;dir\_export&#39;] = $properties[&#39;gtf\_home&#39;] . &#39;/public&#39;;

en indiquant le chemin complet des répertoires upload et public.

- .Dans le fichier de configuration httpd.conf du répertoire .\server\Apache2.4\conf du répertoire d&#39;installation de GTF , modifier la configuration :

Alias /public &quot;C:/serveur/gtf\_2015-01.00.b12674\_betax64/public&quot;en indiquant le chemin complet

&lt;Directory &quot;C:/serveur/gtf\_2015-01.00.b12674\_betax64/public&quot;&gt;

en indiquant le chemin complet du répertoire public.

Nettoyage et suppression des fichiers temporaires

L&#39;administrateur doit veiller à supprimer régulièrement les fichiers temporaires générés par l&#39;application.

Il dispose pour cela du projet FME &#39;nettoyage\_des\_fichiers\_temporaires.fmw&#39; contenu dans le fichier **admin.gex** , disponible sur [notre site de téléchargement.](http://download.veremes.com/) Après avoir importé et publié ce projet dans GTF, l&#39;administrateur peut s&#39;abonner au traitement et assurer de la sorte une suppression régulière des fichiers temporaires.

3 types de fichiers peuvent être supprimés :

- .Les fichiers temporaires produits par GTF
- .Les fichiers temporaires produits par FME
- .Les jeux de données sources chargés sur le serveur par les utilisateurs finaux contenus dans le répertoire &lt;gtf&gt;\upload

Le paramètre &#39;Age minimum des fichiers à supprimer&#39;  permet de définir l&#39;ancienneté minimale (en jours) des fichiers à supprimer évitant ainsi la suppression de fichiers déposés sur le serveur sans avoir été traités ou en cours d&#39;exécution.

Un rapport de nettoyage dont le nom est défini par l&#39;utilisateur est généré au format.txt.

 Support technique

 Pour toute information complémentaire, vous pouvez contacter l&#39;équipe de Veremes par mail à l&#39;adresse [support@veremes.com](mailto:support@veremes.com) ou poser votre question sur la pateforme d&#39;assistance [http://support.veremes.com/](../../C:/margot2/svn/produit/gtf/doc/gtf_manuel_utilisateur/Content/gtf_manuel_utilisateur/Annexes.htm/#http://support.veremes.com/)

Service commercial :

+33 (0)4 68 38 65 27

Support technique :

+33 (0)4 11 81 98 01

  Annexes

 Syntaxe des expressions CRON pour la définition des périodes d&#39;abonnement

Le code à saisir doit respecter la syntaxe : **mm hh jj MMM JJJ tâche**

Où

**mm** représente les minutes (de 0 à 59)

**hh** représente l&#39;heure (de 0 à 23)

**jj** représente le numéro du jour du mois (de 1 à 31)

**MMM** représente l&#39;abréviation du nom du mois (jan, feb,…) ou le numéro du mois (de 1 à 12)

**JJJ** représente l&#39;abréviation du nom du jour ou bien le numéro du jour dans la semaine (0 = dimanche, 6 = samedi)

\*Signifie à chaque unité (0,1,2,3,4…)

5,8 signifie les unités 5 et 8

2-5 signifie les unités de 2 à 5

\*/3 signifie toutes les 3 unités (0,3,6,9…)

Exemples de syntaxe :

Tous les jours à 12 h : **0 12 \*\*\***

Tous les lundis à 22h15 : **15 22 \* \*1**

Toutes les heures passées de 15 min : **15 \* \* \* \***

Tous les premiers du mois à 4h42 : **42 4 1 \* \***

Du 2 au 5 de chaque mois à 10h12 **: 12 10 2-5 \*\***

 Services web et privilèges

L&#39;accès à un service web dépend du profil du compte connecté. Ainsi par exemple, un utilisateur ayant pour privilège gtf\_user, ne peut pas accéder à la ressource &#39;Workspaces&#39; qui retourne la liste des projets puisqu&#39;un privilège gtf\_author est requis.

Le tableau ci-dessous présente les privilèges requis pour pouvoir accéder aux différents services de l&#39;API :

| service | Ressource | Privileges requis |
| --- | --- | --- |
| gtf | Categories | gtf\_user |
| gtf | EmailContexts | gtf\_user |
| gtf | EmailOptions | gtf\_user |
| gtf | EmailTemplates | gtf\_author |
| gtf | FMEEngines | gtf\_admin |
| gtf | GtfEngines | gtf\_admin |
| gtf | GTFGroups | vitis\_admin |
| gtf | Inboxes | gtf\_author |
| gtf | License | gtf\_admin |
| gtf | MessageClasses | gtf\_user |
| gtf | MessageClassTypes | gtf\_user |
| gtf | Messages | gtf\_user |
| gtf | Orders | gtf\_author |
| gtf | OrderStatutes | gtf\_user |
| gtf | Periods | gtf\_user |
| gtf | Priorities | gtf\_user |
| gtf | Servers | gtf\_admin |
| gtf | Statistics | gtf\_author |
| gtf | Subscriptions | gtf\_author |
| gtf | SupervisionStatues | gtf\_author |
| gtf | Surveys | gtf\_author |
| gtf | SurveyType | gtf\_user |
| gtf | Tags | gtf\_user |
| gtf | UserOrders | gtf\_user |
| gtf | UserSubscriptions | gtf\_user |
| gtf | UserSurveys | gtf\_user |
| gtf | Versions | gtf\_user |
| gtf | Workspaces | gtf\_author |
| vitis | Domains | vitis\_user |
| vitis | GenericQuerys | vitis\_user |
| vitis | Groups | vitis\_user |
| vitis | Logs | vitis\_admn |
| vitis | Modes | vitis\_user |
| vitis | Phpinfo | vitis\_admin |
| vitis | Privileges | vitis\_user |
| vitis | Properties | vitis\_user |
| vitis | Ressources | vitis\_user |
| vitis | Tabs | vitis\_user |
| vitis | Users | vitis\_admin |
| vitis | Versions | vitis\_user |
| vitis | VitisSections | vitis\_user |
| vitis | WebServices | vitis\_user |

Liste des contrôles GTF

| Nom du contrôle GTF |
| --- |
| Bouton radio |
| Carte Bing |
| Carte OSM |
| Carte vMap |
| Champ caché |
| Couleur |
| Curseur |
| Date et Heure |
| Décimal |
| Entier |
| Fichier local |
| Interface - Ligne de séparation |
| Label |
| Label Titre |
| Liste |
| Liste déroulante |
| Texte en édition 1 ligne |
| Texte en édition Mot de passe |
| Texte en édition Multiligne |
| Texte en édition URL |

 Projets FME intégrés

3 projets FME sont intégrés initialement à GTF :

 Projet Admin-Export

Le projet Admin export permet d&#39;exporter des projets FME au format d&#39;échange de gtf : .gex.

On peut exporter 1 à n projets FME.

 Projet Admin Import

Le projet Admin-Import permet l&#39;import dans GTF de traitements FME contenus dans un répertoire gex.

 Un projet FME dans GTF est identifié de façon unique par une clé. Le projet d&#39;import permet, en cas d&#39;import de projet dont la clé est existante en base de données, de choisir que faite de ce dernier :

- .Remplacer le projet existant : le projet est mis à jour et son nom, sa clé et son identifiant sont conservés.
- .Ne pas importer le projet
- .Importer le projet avec une nouvelle clé et un nouveau nom. On ajoute de la sorte un nouveau projet en base.

Un rapport d&#39;import est généré au format html. Il indique le nom et la clé du projet importé et le statut de l&#39;import, c&#39;est à dire &quot;Mis à jour dans GTF&quot;, &quot;Non mis à jour dans GTF&quot; ou &quot;inséré dans GTF&quot;.



 ![](./)

 Projet Vérification des formulaires

Ce traitement permet la vérification et/ou la génération des formulaires des traitements.

 Les formulaires des traitements importés depuis une version antérieure à GTF 2016 ne sont pas directement créés au format json. Ce traitement permet de définir les conditions de génération des formulaires par défaut et des formulaires publiés.

Tous les traitements sont parcourus.

2 options sont possibles :

-
.Ne pas forcer la régénération des formulaires par défaut pour tous les traitements : Ne sont traités que les traitements ne disposant pas de formulaire publié de type subform.json. Leurs formulaires sont donc invalides ![](./)
 .
 .

 si le type de formulaire publié indiqué en base est de type &#39;par défaut&#39;, alors les 3 formulaires sont générés.

 Sinon, si le formulaire source indiqué en base est de type &#39;personnalisé&#39;, alors un rapport indique que le traitement est invalide et que l&#39;auteur doit créer lui même le formulaire.

- .Forcer la régénération des formulaires par défaut pour tous les traitements. Un formulaire par défaut est regénéré pour **tous** les traitements. Les formulaires par défaut sont publiés **Si** le formulaire en base de données est de type Défaut. Sinon les formulaires publiés personnalisés sont conservés.

En savoir plus sur les formulaires dans GTF.


