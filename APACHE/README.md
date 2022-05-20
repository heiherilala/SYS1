# Instalatin du serveur APACHE2
## Présentation du serveur APACHE2
Apache est un serveur Web multiplateforme open source populaire et  le serveur Web le plus populaire en nombre. Il est activement maintenu par l'Apache Software Foundation.            
Non seulement il est populaire, mais c'est aussi l'un des plus anciens serveurs Web, sa première version remontant à 1995. De nombreux hébergeurs cPanel utilisent désormais Apache. Comme tout serveur Web, Apache gère  la gestion des fichiers dans les coulisses du site Web pour les visiteurs.     
## INSTALLATION du serveur
### Installation du service apache2
Pour installer le serveur, il faut taper la linge de commande:
```
apt update
apt install apache2
```
Pour voir l’état du service:
```
systemctl status apache2
```
### Configuration du serveur apache2
#### Les fichiers de configuration du serveur 
Elle est séparée en plusieurs dossiers qui se trouvent dans "/etc/apache2/".
* **apache2.conf** : configuration principale
* **mods-enabled** : configuration des différents modes
* **conf-enabled** : configuration supplémentaire
* **sites-enabled** : configuration des virtualhost 

pour pouvoir y revenir en cas d'erreur, sauvegardons tout d'abord le fichier dans un autre a de le modifier   
```
cp /etc/apache2/apache2.conf /etc/apache2/apache2.conf.defaut
```

#### Ports
Les ports utilisés par apache sont accessibles par la commande : 
```
nano /etc/apache2/ports.conf
```
* **80** : port par défauts pour les sites http
* **443** : port pour les sites https

#### Configuration du virtualhost
Pour modifier la configuration du virtualhost par défaut:
```
nano /etc/apache2/sites-enabled/000-default.conf
```
Voici les paramètres de base de la configuration d'un virtualhost:
* **<VirtualHost *:80>** => l’adresse IP et le port 80
* **ServerAdimin : webmaster@localhost** => l’email à contacter en cas de problème "webmaster@localhost"
* **DocumentRoot : /var/www/html** dossier où se situent les fichiers du sit "/var/www/html"
* **ErrorLog** et **CustomLog** dossiers d’emplacement des fichiers log

Il faut spécifier le chemin "/home/herilala/www/" dans le fichier de configuration 
```
nano /etc/apache2/apache2.conf
```
Puis ajouter dans la partie **directory** :
```
<Directory /home/herilala/www/>
    Options -Indexes +FollowSymLinks
    AllowOverride None
    Require all granted
</Directory>
```
Puis modifier le configuration du virtualhost evec:
```
nano /etc/apache2/sites-enabled/000-default.conf
```
Dans ce fichier de configuration, changer le chemin du dossier contenant les fichiers du site par :
```
DocumentRoot : /home/herilala/www/
```
À chaque modification, ne jamais oublier de redémarré le serveur:
```
systemctl reload apache2 #ou systemctl restart apache2
```
Pour vérifier l’état du service apache2:
```
systemctl status apache2 #ou service apache2 status
```
#### Créer une nouvelle configuration virtualhost
Supposons que nous possédons le nom de domaine "siteherilala.mg".
Pour créer une nouvelle configuration virtualhost:
```
nano /etc/apache2/sites-enabled/001-siteherilala.conf
```
Utilisons la configuration suivante:
```
<VirtualHost *:80>
        ServerAdmin hei.herilala.31@gmail.com
        ServerName siteherilala.mg  #si possède le nom de domaine, déjà hébergé sur un serveur
        DocumentRoot : /var/www/siteherilala
<Directory /var/www/siteherilala>
        Options -Indexes +FollowSymLinks
        AllowOverride all
</Directory>

</VirtualHost>
```
Pour activer la configuration virtualhost:
```
a2ensite /etc/apache2/sites-enabled/001-siteherilala.conf
```

À chaque modification, ne jamais oublier de redémarré le serveur:
```
systemctl restart apache2
```

#### Outil de vérification d’erreur de configuration
Pour afficher les erreurs de configuration, nous avons l’outil configtest d’apache2:
```
/user/sbin/apache2ctl configtest
```

## Partie 3 - ACCÈS AU SITE WEB 
Il sufi de saisir l'adresse IP et le port du serveur (80 par défaut) ou le nom du domaine




[revenir_sur_la_liste_des_servers](https://github.com/heiherilala/servers)