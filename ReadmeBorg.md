# BORG (BorgBackup)


## *What's Borg ?*

L'objectif principal de Borg est de fournir un moyen efficace et sécurisé de sauvegarde des données. La technique de déduplication des données utilisée rend Borg adapté aux sauvegardes quotidiennes car seules les modifications sont stockées. La technique de cryptage authentifiée la rend appropriée pour les sauvegardes vers des cibles non totalement fiables.
___

 **1. Installation**

 **2. Mise en place du système de Backup**
 ___
 

## 1.  Basic installation command set ##

    sudo apt-get install python3 python3-dev python3-pip python-virtualenv
    libssl-dev openssl
    libacl1-dev libacl1
    build-essential

___

## 2.  Basic Borg comand set ##

Initialize a new backup repository (see  `borg  init  --help`  for encryption options):

    $ borg init -e repokey /path/to/repo

Create a backup archive:

    $ borg create /path/to/repo::Saturday1 ~/Documents

Now deduplication example:

    $ borg create -v --stats /path/to/repo::Saturday2 ~/Documents
    -----------------------------------------------------------------------------
    Archive name: Saturday2
    Archive fingerprint: 622b7c53c...
    Time (start): Sat, 2016-02-27 14:48:13
    Time (end):   Sat, 2016-02-27 14:48:14
    Duration: 0.88 seconds
    Number of files: 163
    -----------------------------------------------------------------------------
                   Original size      Compressed size    Deduplicated size
    This archive:        6.85 MB              6.85 MB             30.79 kB  <-- !
    All archives:       13.69 MB             13.71 MB              6.88 MB
    
                   Unique chunks         Total chunks
    Chunk index:             167                  330

____
*All required command:*

   **Création d'un dépôt pour gérer les sauvegardes :**
        
    
    $ borg init /path-to-repo
    
   **Sauvegarde des répertoires ~/src et ~/Documents dans une archive appelée :**
        
    
    $ borg create /path-to-repo::Archive ~/src ~/Documents
    
 **Le lendemain, créez une nouvelle archive appelée Mardi :**
        
    
    $ borg create -v --stats /path-to-repo::Mardi ~/src ~/Documents
    
  Cette sauvegarde sera beaucoup plus rapide et beaucoup plus petite puisque seules les nouvelles données jamais vus auparavant sont stockées. L'option –stats demande à Borg les statistiques de sortie sur l'archive nouvellement créée, comme la quantité de données uniques (non partagé avec d'autres archives).
    
  **Affiche la liste de toutes les archives dans le dépôt :**
        
    
    $ borg list /path-to-repo
     Lundi lun, 15/04/2016 19:14:44 Mardi mar, 16/04/2016 19:15:11_
    
   **Affiche le contenu de l'archive Lundi :**
        
    
    $ borg list /path-to-repo::Lundi
    
    _drwxr-xr-x user group 0 Mon, 2016-02-15 18:22:30 home/user/Documents  
    -rw-r–r– user group 7961 Mon, 2016-02-15 18:22:30 home/user/Documents/Important.doc_
    
   **Restore l'archive Lundi :**
        
    
    $ borg extract /path-to-repo::Lundi
    
   **Monte une archive comme un système de fichier FUSE :**
        
    
    $ borg mount /path-to-repo::Lundi /tmp/mymountpoint
    
   ensuite on peut très facilement y accéder:
    
    $ ls /tmp/mymountpoint
    
   puis démonter le système de fichier
    
    $ fusermount -u /tmp/mymountpoint
    
   **On peut aussi optimiser les sauvegardes en supprimant toutes les archives qui ne correspondent pas l'une des options de rétention spécifiées :**  
        
    
Cette commande est normalement utilisée par les scripts de sauvegarde automatisés qui souhaitent garder un certain nombre de sauvegardes historiques.
Par exemple, garder les 7 dernières archives journalières ainsi que 4 sauvegardes additionnelles de fin de semaine
    
    $ borg prune --keep-daily=7 --keep-weekly=4 /path-to-repo
    
Garder 7 jours de sauvegarde, 4 sauvegardes de fin de semaines et toutes les sauvegardes de fin de mois (Vous remarquerez le "-" devant les sauvegardes mensuelles, spécifier un nombre négatif de sauvegardes signifie qu’on conserve une sauvegarde indéfiniment):
    
    $ borg prune --keep-daily=7 --keep-weekly=4 --keep-monthly=-1 /path-to-repo
    
Garder toutes les sauvegardes des 10 derniers jours, 4 sauvegardes additionelles de fin de semaine et toutes les sauvegardes mensuelles
    
    $ borg prune --keep-within=10d --keep-weekly=4 --keep-monthly=-1 /path-to-repo
    
  **Faire des sauvegardes, c'est bien mais les vérifier, c'est encore mieux :**
        
    
   Tester tout (dépôt et fichiers sauvegarde) ⇒ Attention : peut prendre un certain temps en fonction de la taille de la sauvegarde…
    
    $ borg check  /path-to-repo
    
   Tester juste la cohérence du dépôt (plus rapide)
    
    borg check --repository-only /path-to-repo


____

[Usage](https://borgbackup.readthedocs.io/en/stable/usage.html)

-   [General](https://borgbackup.readthedocs.io/en/stable/usage/general.html)
-   [borg init](https://borgbackup.readthedocs.io/en/stable/usage/init.html)
-   [borg create](https://borgbackup.readthedocs.io/en/stable/usage/create.html)
-   [borg extract](https://borgbackup.readthedocs.io/en/stable/usage/extract.html)
-   [borg check](https://borgbackup.readthedocs.io/en/stable/usage/check.html)
-   [borg rename](https://borgbackup.readthedocs.io/en/stable/usage/rename.html)
-   [borg list](https://borgbackup.readthedocs.io/en/stable/usage/list.html)
-   [borg diff](https://borgbackup.readthedocs.io/en/stable/usage/diff.html)
-   [borg delete](https://borgbackup.readthedocs.io/en/stable/usage/delete.html)
-   [borg prune](https://borgbackup.readthedocs.io/en/stable/usage/prune.html)
-   [borg info](https://borgbackup.readthedocs.io/en/stable/usage/info.html)
-   [borg mount](https://borgbackup.readthedocs.io/en/stable/usage/mount.html)
-   [borg umount](https://borgbackup.readthedocs.io/en/stable/usage/mount.html#borg-umount)
-   [borg key change-passphrase](https://borgbackup.readthedocs.io/en/stable/usage/key.html)
-   [borg key export](https://borgbackup.readthedocs.io/en/stable/usage/key.html#borg-key-export)
-   [borg key import](https://borgbackup.readthedocs.io/en/stable/usage/key.html#borg-key-import)
-   [borg upgrade](https://borgbackup.readthedocs.io/en/stable/usage/upgrade.html)
-   [borg recreate](https://borgbackup.readthedocs.io/en/stable/usage/recreate.html)
-   [borg export-tar](https://borgbackup.readthedocs.io/en/stable/usage/tar.html)
-   [borg serve](https://borgbackup.readthedocs.io/en/stable/usage/serve.html)
-   [borg config](https://borgbackup.readthedocs.io/en/stable/usage/config.html)
-   [borg with-lock](https://borgbackup.readthedocs.io/en/stable/usage/lock.html)
-   [borg break-lock](https://borgbackup.readthedocs.io/en/stable/usage/lock.html#borg-break-lock)
-   [borg benchmark crud](https://borgbackup.readthedocs.io/en/stable/usage/benchmark.html)
