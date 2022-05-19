# Installation te configuration server NFS

## Présentation NFS
NFS (Network File System) est un protocole permettant de monter des disques en réseau. Il est basé sur le principe de client/serveur.     

Le NFS permet à un utilisateur d'accéder, grâce à son ordinateur (le client), aux fichiers stockés sur un serveur distant. Il est possible de consulter mais aussi mettre à jour ces fichiers, comme s’ils étaient présents sur l’ordinateur client (c’est-à-dire comme des fichiers locaux classiques). Ceci permet de stocker des ressources sur un serveur et d'accéder à un réseau par une multitude d'ordinateurs connectés. Le NFS permet aussi le travail collaboratif sur le même document, ainsi que l'enregistrement et la centralisation des documents sur le même serveur. Ce système a été développé par l'ancien fabricant informatique Sun Microsystems en 1984, maintenant fusionné avec Oracle. Le NFS a été conçu sur les systèmes Unix. Il y a maintenant des versions pour les systèmes d'exploitation Windows et Mac. NFS est un standard ouvert, défini danse « Request for Comments » (RFC) permettant à quiconque de mettre en œuvre le protocole.          

## Installation et configuration coté server
Avant tout pour ne pas confronté a des problèmes éventuels mettant à jour le système avec :
```
$sudo apt update
```
### Installation
Pour installer le server utilisant :
```
$ apt-get install nfs-kernel-server -y
```
Ensuit construisant un dossier qui sera le dossier a partager (ici en va lui donner le nom de partage)
```
$ mkdir partage
```

### Configuration
Pour spécifier les autorisation et le dossier à partager, il faut modifier le dossier : /etc/exports :
```
$ cd /etc/
$ nano exports 
```
Ou en va ajouter : /home/herilala/partage/ *(sync,no_root_squash,rw)             
Avec :            
/home/herilala/partage/ => est le chemin du dossier à partager             
-"*" => liste des adresse IP qui pourront y accéder (ici « * » veut dire tout le monde)                 
-"Sync" => permet au server NFS de répondre au demande juste après que la requête soit pris en charge par l’unité de stockage. C’est le contraire de "async"                
-"no_root_squash" => stipule que le root de la machine sur laquelle le répertoire est mont a le doit root sur le répertoire                  
-"rw" => donne le droit lire et écrire sur les clients               

Démarré le server              
Pour démarrer :           
```
$ systemctl start nfs-kernel-server -y    
```
Maintenant le serveur marche.             

## Installation coté client
### Installation
Pour pouvoir utiliser un server nfs :
```
$ apt-get install nfs-common
```
Ensuit construisant un dossier où on va monter le dossier
```
$ mkdir estpartager
```

### Monter le dossier
Tout d’abord, vérifiant s’il existe un disque à monter venant du server :
```
$ showmount -e 192.168.227.3 (c’est l’IP du server)
```
Si le server a bien été installer, bien configuré et en marche, la réponse devrai montrer :
/home/herilala/partage *              

Pour le monté :            
```
$ mount -t nfs 192.168.227.2:/home/herilala/partage /home/herilala/estpartager
```
Ou:            
*192.168.227.2 est l’adresse IP du serveur            
*:/home/herilala/partage: est l’emplacement du dossier a partager dans le server             
*/home/herilala/estpartager est l’emplacement client où on va monter de dossier           

##Vérification
Maintenant faisons une vérification :             
Dans le serveur : construisant un fichier texte dans le dossier à partager         
```
$ cd /hom/herilala/partage/
$ toush essai.text
```
Maintenant si on regarde le dossier dans la machine client, nous pouvons bien voir qu’un fichier nommé « essai.tex » a bien été ajouter             

Ensuit, dans la machine client, modifions le fichier « essai.tex »:              
```
$ nano essai.tex
```
Ajouton « voici une phrase » dedans           

Si on revient dans l’ordinateur serveur, on voit bien que le fichier a été modifier, avec :             
```
$ cat essai.tex 
```
Maintenant on peut affirmer que le server marche bien            




[revenir_sur_la_liste_des_servers](https://github.com/heiherilala/servers)