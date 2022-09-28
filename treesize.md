# Afficher la taille de chaque sous dossier en commande sans GUI

**Créer le fichier treesize.sh**
```
#/bin/sh
du -k --max-depth=1 | sort -nr | awk '
     BEGIN {
        split("KB,MB,GB,TB", Units, ",");
     }
     {
        u = 1;
        while ($1 >= 1024) {
           $1 = $1 / 1024;
           u += 1
        }
        $1 = sprintf("%.1f %s", $1, Units[u]);
        print $0;
     }
    '
```

Il ne vous reste qu'a copier le fichier dans un endroit ou le path vous permettra de lancer treesize, ou l'appeler par son chemin complet.. 
Ou sinon, pour faire simple et rapide.. (pas forcément très sécure) créer un alias dans le fichier .bashrc 

**Créer un alias dans .bashrc**

Editer avec vi, ou nano /home/pi/.bashrc et ajouter 

```alias treezise=/home/pi/./treesize.sh)```
