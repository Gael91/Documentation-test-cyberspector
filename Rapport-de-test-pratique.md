# Rapport de test Pratique

## Préparation et Endurcissement du Serveur

## Installation d'un nouveau serveur linux. Dans mon cas j'ai opté pour Ubuntu Server 22.04.1 LTS.

![](RackMultipart20240111-1-js3yln_html_11bc99c7401a2ce.png)


## Check-list de sécurisation d'un serveur linux

## Faire des mises à jour régulières du système.

## Changement du port SSH.

## Installer et configurer un pare-feu histoire de limiter les accès sur le serveur.

## Désactiver la connexion SSH pour les utilisateurs root.

## Endurcir la sécurité du serveur en se basant sur la check-list


## Faire des mises à jour régulières du système : Pour ce faire il suffit d'exécuter un apt-update.

![](RackMultipart20240111-1-js3yln_html_f4059c226f86c086.png)


## Changement du port SSH

## Pour cela on se rend dans le fichier de configuration de SSH et on remplace le port par défaut (22) par 2022 :

![](RackMultipart20240111-1-js3yln_html_50aedf8f73e5189c.png)


## Installer et configurer un pare-feu histoire de limiter les accès sur le serveur

## Dans mon cas ici j'ai choisi comme gestionnaire de pare-feu "UFW". Il est préinstallé sur ubuntu server. Par défaut il est down. Nous pouvons vérifier son status avec cette commande : "ufw status ou service ufw status".

![](RackMultipart20240111-1-js3yln_html_f89de0845d06f2b2.png)

## Pour activer le pare-feu il suffit de faire un "sudo ufw enable ou sudo service ufw enable". J'ajoute maintenant mon port ssh (2022) sur mon pare-feu :

![](RackMultipart20240111-1-js3yln_html_20478e565bb958aa.png)


## Désactiver la connexion SSH pour les utilisateurs root.

## Dans le fichier de configuration SSH sshd\_config nous allons modifier la ligne PermitRootLogin yes en remplaçant yes par no pour désactiver les connexions SSH pour l'utilisateur root :

![](RackMultipart20240111-1-js3yln_html_71b02f0be1de5994.png)


## Mise en Place du Serveur Web Sécurisé

1.
## Installez et cofigurez un serveur web

## Dans mon cas j'ai opté pour le serveur nginx. Ce dernier est installable en exécutant la commande "sudo apt-get install nginx".

## Je peux maintenant accéder à mon serveur web en faisant par une requête http "http://gael-srv-test.cyberspector.xyz/".

![](RackMultipart20240111-1-js3yln_html_98f76a8a255e7e34.png)

## Petit rappel j'ai dû ajouter le port http par défaut (80) a mon pare-feu pour que les requêtes aillent sur mon serveur.

1.
## Sécurisez le serveur web.

## Dans un premier temps je vais changer le port par défaut (80 -\> 8080) pour les requêtes http vers le serveur nginx en modifiant la ligne "listen port" du fichier de configuration de nginx.

![](RackMultipart20240111-1-js3yln_html_a93cd07d0279cc7.png)

## Il faudra aussi ajouter le nouveau port (8080) au pare-feu.

![](RackMultipart20240111-1-js3yln_html_e54f00f6d30d0628.png)

## Dans un second temps je vais sécuriser le site web avec HTTPS, en faisant la demande d'un certificat SSL/TLS gratuit avec Let's Encrypt à partir de Certbot :

## D'abord je vais commencer par installer Certbot avec la commande : sudo apt install certbot.

![](RackMultipart20240111-1-js3yln_html_b91fd2dcf57789fc.png)

## Ensuite il me faut exécuter cette commande "sudo certbot –nginx -d gael-srv-test.cyberspector.xyz" et suivre ensuite les instructions de Certbot pour obtenir un certificat sécuriser pour mon site web.

![](RackMultipart20240111-1-js3yln_html_ce7244098f7c41b8.png)

![](RackMultipart20240111-1-js3yln_html_86a3200904baccaf.png)

## Nous pouvons voir que le site est bel et bien sécurisé à présent.
