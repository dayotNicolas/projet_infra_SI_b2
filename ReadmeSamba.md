# Samba (File transfer system)


## *What's Samba ?*

Le logiciel  **Samba**  est un outil permettant de partager des dossiers et des imprimantes à travers un réseau local. Il permet de partager et d'accéder aux ressources d'autres ordinateurs fonctionnant avec des systèmes d'exploitation Microsoft® Windows® et Apple® Mac  OS® X, ainsi que des systèmes  GNU/Linux, *BSD  et Solaris dans lesquels une implémentation de Samba est installée.

Pour partager de manière simple des ressources entre plusieurs ordinateurs, l'utilisation de Samba est conseillée.
___

 **1. Installation des packages**

 **2. Mise en place de Samba**
 ___
 

## 1.  Basic installation command set ##

   ### 1.1 Pré-requis:

    #### Création d'un compte user pour le partage de fichier
    
    $ addgroup --system sharing
    
    #### Création d'un utilisateur système correspondant à l'utilisateur samba
    
    $ adduser --system sharing --ingroup sharing
    
    #### Mot de passe système unix
    
    $ passwd sharing
    
    #### Création d'un fichier partageable
    
    $ mkdir /home/sharing/public
    
    #### Mise en place des droits sur le répertoire et ses fichiers partageables
    
    $ chown -R sharing:sharing /home/hypathie/
    
    $ chmod -R 770 /home/sharing/

___
### 1.1 Installation:
À l'aide de votre  [gestionnaire de paquets](http://doc.ubuntu-fr.org/gestionnaire_de_paquets "gestionnaire_de_paquets")  préféré,  [installez le paquet](http://doc.ubuntu-fr.org/tutoriel/comment_installer_un_paquet "tutoriel:comment_installer_un_paquet")  **system-config-samba**.

Un bug empêche system-config-samba de se lancer. Il suffit de passer la commande suivante dans un terminal pour régler le problème (détails dans  [ce post](http://forum.ubuntu-fr.org/viewtopic.php?id=1819611 "http://forum.ubuntu-fr.org/viewtopic.php?id=1819611")) :

    $ sudo touch /etc/libuser.conf

Il est conseillé de le lancer comme suit dans un terminal (fonctionne parfaitement après avoir appliqué la ligne de commande ci-dessus)

    $ sudo system-config-samba


 Avec apt-get:[](http://doc.ubuntu-fr.org/tutoriel/comment_installer_un_paquet#avec_apt-get)

    $ sudo apt-get install mon_paquet

## Utilisation[](http://doc.ubuntu-fr.org/system-config-samba#utilisation)

Une fois installé, faites une recherche dans les applications avec le mot clé  _samba_  pour lancer system-config-samba (icône "Samba"). Si elle n’apparaît pas dans la liste, il faut la lancer avec  [pkexec](http://doc.ubuntu-fr.org/tutoriel/effectuer_des_taches_en_super_utilisateur#executer_une_application_graphique_sous_1404_et_versions_ulterieures "tutoriel:effectuer_des_taches_en_super_utilisateur")  suivi par :

    $ system-config-samba

## 2.  Basic Samba command set ##


