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
