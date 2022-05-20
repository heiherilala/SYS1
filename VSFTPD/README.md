# Instalatin du serveur VSFTPD
## Présentation du serveur VSFTPD
VSFTPD est un server de partage de donner, Il permet de stocker ou récupérer des fichiers sur le serveur. L’avantage est que nous pourrons ainsi manipuler nos fichiers depuis n’importe quel ordinateur à travers le monde. Nous avons simplement besoin d’une connexion internet.             

Il permet donc le transfert de fichiers entre un client et un serveur. Un client FTP est une application qui s’utilise depuis un ordinateur. Elle est utilisée pour importer ou exporter des fichiers d’un serveur FTP. Un des logiciels les plus connus pour faire le rôle de client FTP est Filezilla. [A télécharger sur cette page](https://filezilla-project.org/).      

## Instlalation serveur
### Installation du service vsftpd
Pour installer le serveur, il faut taper la linge de commande:
```
apt update
apt install vsftpd
```
Pour voir la version installée:
```
vsftpd -v
```
Pour voir l’état du service vsftpd:
```
systemctl status vsftpd
```
S'il n'est pas encore actif, il n'y a qu'à le démarrer avec:
```
systemctl start vsftpd
```
### Ajout client et dossier dédié à ce client via serveur
Pour ajouter un client (ici: **clientftp**):

```
adduser clientftp
```
créons un dossier qui sera par la suite le dossier du client "clientftp"

```
mkdir /home/clientftp/ftp
```
Pour changer la permission du dossier créé:
```
chown nobody:nogroup /home/clientftp/ftp
chmod a-w /home/clientftp/ftp
```
Pour vérifier les changements effectués:
```
ls -al /home/clientftp/ftp
```

### 2.3.	Configuration du serveur vsftpd
L'emplacement du fichier de configuration du serveur vsftpd se trouve dans le chemin "/etc/vsftpd.conf".             
pour pouvoir y revenir en cas d'erreur, sauvegardons tout d'abord le fichier dans un autre a de le modifier                   
```
cp /etc/vsftpd.conf /etc/vsftpd.conf.defaut
```
Les détails sur les configurations possibles se trouve dans: [vsftpd.beasts.org](http://vsftpd.beasts.org/vsftpd_conf.html).        
Pour configurer le serveur : 
```
nano /etc/vsftpd.conf
```
À chaque modification, ne jamais oublier de redémarré le serveur:
```
systemctl reload vsftpd #ou systemctl restart vsftpd
```

## Accès au serveur pour les clients
Ou on passe par la ligne de commande.          

Ou au moyen du logiciel client FTP.          

La méthode la plus simple pour se connecter au serveur c’est de télécharger un logiciel FTP-client, par exemple le logiciel
[Client Filezilla](https://filezilla-project.org/)          

pour se connecter nous aurons besoin de:        
* l’adresse IP du serveur (obtenu via **"ip addr #ou ip a"** sur l'ordinateur serveur) 
* identifiant du client (ce que nous avons déjat défini, ici **"client FTP"**)
* mot de passe du client (ce que nous avons déjat défini)


[revenir_sur_la_liste_des_servers](https://github.com/heiherilala/servers)