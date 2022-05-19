# SERVEUR SAMBA

## I- Présentation
Une des méthodes les plus courantes pour mettre Ubuntu et Windows en réseau est de configurer Samba en serveur de fichiers.     

La licence publique générale GNU permet l’implantation du protocole SMB (Server Message Block), qui a donné le nom à la suite Samba, dans les systèmes d’exploitation Linux et Unix.  Ce protocole de partage des ressources (SMB), aussi connu dans sa version plus récente CIFS pour Common Internet File System ou système de fichier Internet commun, était à l’origine utilisé comme réseau local Windows établissant des interactions avec des serveurs de fichiers, d’imprimantes et autres services.Grâce à une telle mise en œuvre des ordinateurs sous Windows, Linux et Unix peuvent être connectés, de manière à pouvoir échanger des données ou utiliser conjointement des imprimantes et autres services. Peu importe si le serveur est installé sous Linux ou Unix, car la quatrième version du logiciel prend en charge le rôle d’Active Directory Domain Controllers, par lequel une autorisation et authentification centralisée des différents ordinateurs et des utilisateurs est possible.

## II- INSTALLATION
### 1- Installation
pour installer Samba, écrivons sur la ligne de commande :
```
$sudo apt update
$sudo apt install samba
```
Ensuit, vérifions si l'installation est réussi:
```
$sudo whereis samba
```
Qui devrait sortir:
```
samba: /usr/sbin/samba /usr/lib/samba /etc/samba /usr/share/samba /usr/share/man/man7/samba.7.gz /usr/share/man/man8/samba.8.gz
```

### 2- Configuration
Maintenant, créant le répertoire qui sera partagé:
```
$sudo mkdir /home/herilala/sambashare/
```

Le fichier de configuration pour Samba se trouve dans: **/etc/samba/smb.conf**.

Pour ajouter le nouveau répertoire sous forme de partage, nous modifions le fichier "/etc/samba/smb.conf" :

```
$sudo nano /etc/samba/smb.conf
```

Ajoutons les lignes suivantes :
```
[sambashare]
    comment = Samba on Linux
    path = /home/<username>/sambashare
    read only = no
    browsable = yes
```

Le dossier est maintenant partagé par le serveur, redémarrons Samba pour qu'il prenne effet ;
```
$sudo service smbd restart
```
Mettons à jour le pare-feu ufw pour autoriser Samba :
```
$sudo ufw enable   
$sudo ufw allow samba   
$sudo ufw reload   
```

### 3- Configuration de sécurité
Pour plus de sécurité, ous devons configurer un mot de passe Samba pour notre compte utilisateur :
```
$sudo smbpasswd -a username
```
Et ne jamais oublier de redémarré le serveur   

Maintenant notre serveur est bien en marche





[revenir_sur_la_liste_des_servers](https://github.com/heiherilala/servers)