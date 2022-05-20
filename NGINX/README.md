# Installation te configuration server Nginx
## Présentation
Le Nginx (prononcé comme Engine-X) est un logiciel qui peut agir à la fois comme un serveur Web et un serveur proxy. Vous pouvez diffuser du contenu Web via le serveur Nginx. Grâce aux fonctionnalités de proxy et de proxy inverse du serveur Nginx, vous pouvez également l’utiliser comme routeur. L’équilibrage du trafic, la mise en cache et d’autres opérations du serveur peuvent être effectués par le serveur Nginx. Vous pouvez installer le serveur Nginx sur n’importe quel serveur cloud, moteur docker ou machine Linux locale. L’algorithme du serveur Nginx est très bénéfique pour ceux qui ont un serveur commercial. Comme Ubuntu exécute la plupart des serveurs Web dans le monde, vous pouvez installer le serveur Nginx sur votre machine Ubuntu pour de meilleures performances.

## INSTALLATION
### Installation
Avant tout pour ne pas se confronter à des problèmes éventuels mettant à jour le système avec :
```
$ apt updat
```
Pour installer le serveur utilisant :
```
$ apt install nginx
```
Normalement, le serveur démarrera automatiquement, mais s’il ne se démarre pas il faut le faire manuellement avec :
```
$ systemectl restart nginx
```

### Configuration
Les configurations se trouvent dans : /etc/nginx/sites-enabled/ nom « default »
```
$ cd /etc/nginx/sites-enabled
$ nano default
```

Si on enlève les commentaires, on trouvera : 

```
server {
       listen 80 default_server;
       listen [::]:80 default_server;

       server_name _;

       root /var/www/html;
       index index.html index.nginx-debian.html;

       location / {
               try_files $uri $uri/ =404;
       }
}
```

Explication :

* **listen 80;** => il écoute par défaut sur le port 80    
* **server_name _;** => c’est le nom du serveur, qui peut aussi être un nom de domaine.     
* **root /var/www/html;** => indique où est le fichier à ouvrir.    
* **index index.html index.nginx-debian.html;** => ouvrire “intex” , si on ne le trouve pas, ouvrière « index.html », sinon, ouvrir « index.nginx-debian.html »     

## Modification du site :
Si on ne change pas « root /var/www/html; », alors, il faut mettre nos dossiers dans « /var/www/html » et les modifier      

On n’oublie pas de redémarrer le serveur      

```
$ systemectl restart nginx 
```
Et voilà notre serveur est terminé et nous savons où modifier notre site

## Modifier nom de domaine :
Modifions de fichier **/etc/hosts**     

Et ajouton **« 127.0.0.1       monsite.mg »**       

Maintenant si on écrit « monsite.mg » il nous dirigera automatiquement ver notre site        

Si on regarde aussi le fichier /etc/nginx/nginx.conf ; on voit que dans http il y est écrit : « include /etc/nginx/sites-enabled/*; »       

Cela veut dire que tous les fichiers qui se trouvent dans le dossier « /etc/nginx/sites-enabled/ » seront pris en compte par le serveur pour la configuration du http ;             

Donc créant un nouveau serveur qui prend en compte seulement notre nom de domaine :               

Dans ce dossier, créons un nouveau fichier ou on va éditer un serveur :             

```
$toush autreserver.conf
$ nano autreserver.conf
```
On va écrire :
```
server {
        listen 80;
        root /var/www/html;
        index index.html index.htm index.nginx-debian.html;
        server_name monsite.mg;
        location / {
                try_files $uri $uri/ =404;
        }
```

Ici, dans server_name monsite.mg => on a défini notre nom de domaine                   

Et dans root /var/www/html; => on a pointé une autre emplacement               

Par conséquent :              

* Si on entre dan notre url Adress IP : il nous enverra dans la page qui se trouve dans l’emplacement définit par /etc/nginx/sites-enabled/default                          
* Si on entre dans notre url monsite.mg: il nous enverra dans la page qui se trouve dans l’emplacement définit par /etc/nginx/sites-enabled/ autreserver.conf                   





[revenir_sur_la_liste_des_servers](https://github.com/heiherilala/servers)