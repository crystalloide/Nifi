# Apache Nifi pour des TPs de formation dans un environnement Linux ou virtualisé ou en ligne "Gitpod"


### Rappel pour retrouver les environnements Gitpod éventuellement précédemment instanciés : [ https://gitpod.io/workspaces ](https://gitpod.io/workspaces)

Nous allons installer un serveur stand alone Nifi sur un environnement virtuel accessible à partir d'un simple navigateur web, à des fins de développement et de formation. 

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/crystalloide/Nifi
)

###########################################################################################################
## TP01 : Installation Apache Nifi 2.0 sur Linux : 
## 		  https://nifi.apache.org/documentation/v2/
###########################################################################################################

## JDK Java 21
## Les proccesseurs basés sur Python (fonctionnalité beta) nécessitent: 
## Python 3.9, 3.10, 3.11, ou 3.12

###########################################################################################################
## I°) 	Installation mode stand alone sans zookeeper : 
##		Site : https://nifi.apache.org/download/
##             https://dlcdn.apache.org/nifi/ 
###########################################################################################################

## Aller sur le paragraphe "binaries" et cliquer sur la ligne "NiFi Standard 2.0.0-M4" (M4 disponible depuis le 28-06-2024)

## A savoir : "M" = Milestone

## Nous arrivons sur la page : https://www.apache.org/dyn/closer.lua?path=/nifi/2.0.0-M4/nifi-2.0.0-M4-bin.zip

## Ce qui nous donne finalement le lien de téléchargement suivant : 
https://dlcdn.apache.org/nifi/2.0.0-M4/nifi-2.0.0-M4-bin.zip



###########################################################################################################
## On se place sur le répertoire souhaité d'installation : 
## Dans un terminal Git Bash : 
###########################################################################################################

    cd ~

    pwd

## /home/gitpod

## cd /workspace/nifi



###########################################################################################################
## I.1°) Pre-requis : Installation du JDK Java 21 : 
###########################################################################################################

###########################################################################################################
## Installation jdk Java 21 : 
## Pour Linux : OpenJDK https://jdk.java.net/archive/
##		https://download.java.net/java/GA/jdk21.0.2/f2283984656d49d69e91c558476027ac/13/GPL/openjdk-21.0.2_linux-x64_bin.tar.gz
##
## Pour linux : JDK ORACLE : https://www.oracle.com/java/technologies/downloads/#java21
##		https://download.oracle.com/java/21/latest/jdk-21_linux-x64_bin.tar.gz
###########################################################################################################

    cd ~

    sudo rm jdk-21_linux-x64_bin.tar.gz

    sudo wget https://download.oracle.com/java/21/latest/jdk-21_linux-x64_bin.tar.gz

    ll *.gz


## Archive à décompresser : jdk-21_linux-x64_bin.tar.gz

## On décompresse :

    sudo tar -xzvf jdk-21_linux-x64_bin.tar.gz

## On obtient dans notre cas un répertoire "jdk-11.0.1" dans notre répertoire courant :

    ls

    sudo rm -Rf ~/jdk

    mv jdk-21.0.4 jdk

## sudo chmod -Rf 775 /jdk
## sudo chown -Rf gitpod:gitpod /jdk

## On vérifie que notre installation opérationnelle : 

    ~/jdk/bin/java -version

## Affichage : 
	Picked up JAVA_TOOL_OPTIONS: -XX:+UseContainerSupport -XX:ActiveProcessorCount=1
	java version "21.0.4" 2024-07-16 LTS
	Java(TM) SE Runtime Environment (build 21.0.4+8-LTS-274)
	Java HotSpot(TM) 64-Bit Server VM (build 21.0.4+8-LTS-274, mixed mode, sharing)


## Il nous reste à définir ou enrichir les variables : 
## export JAVA_HOME=jdk-install-dir
## export PATH=$JAVA_HOME/bin:$PATH

## Ajout du répertoire dans le PATH :

    export JAVA_HOME=~/jdk 
    
    export PATH=~/jdk/bin:$PATH


    java -version
    
## Affichage : 
	Picked up JAVA_TOOL_OPTIONS: -XX:+UseContainerSupport -XX:ActiveProcessorCount=1
	java version "21.0.4" 2024-07-16 LTS
	Java(TM) SE Runtime Environment (build 21.0.4+8-LTS-274)
	Java HotSpot(TM) 64-Bit Server VM (build 21.0.4+8-LTS-274, mixed mode, sharing)

	


###########################################################################################################
## I.2°) Nettoyage des installations précédentes éventuelles :  
###########################################################################################################

    cd ~
    
    rm -Rf nifi



###########################################################################################################
## I.3°) Installation de Nifi 2.0 :  
###########################################################################################################

    cd ~

    rm nifi-2.0.0-M4-bin.zip

    wget https://dlcdn.apache.org/nifi/2.0.0-M4/nifi-2.0.0-M4-bin.zip

    ll *.zip

    unzip nifi-2.0.0-M4-bin.zip

    mv nifi-2.0.0-M4 nifi

    cd nifi


## cd ~
## sudo chown user:user -Rf nifi/
## sudo chmod 777 -Rf nifi/


ls ~/nifi/
## Affichage : 
	bin/  conf/  docs/  extensions/  lib/  LICENSE  NOTICE  python/  README

## On constate qu'à l'issue de la toute 1ère installation, il y a peu de répertoires présents.

## Certains répertoires/fichiers seront crées au tout 1er lancement 

## (d'où le délai nécessaire constaté au 1er lancement de Nifi ) 

## On ajoute les binaires nifi au PATH : 
export PATH=~/nifi/bin:$PATH

echo $PATH


## Version de python installée : 
    python --version
    
## Affichage : 
	Python 3.12.4



## Etape optionnelle avant lancement  :

ls ~/nifi/conf 

## On peut préciser un password dans le fichier de configuration nifi.properties 
## au niveau du paramètre "nifi.sensitive.props.key" (ligne 186)

vi ~/nifi/conf/nifi.properties 


## On remarque au passage l'emplacement où l'URL et le port sont indiqués :
## (Ligne 161 et 162)
nifi.web.https.host=localhost
nifi.web.https.port=8443








###########################################################################################################
## I.4°) Lancement de Nifi :  
###########################################################################################################

cd ~/nifi/bin

ls
## Affichage : 
	dump-nifi.bat  nifi.cmd  nifi.sh  nifi-env.bat  nifi-env.cmd  nifi-env.sh  run-nifi.bat  status-nifi.bat
	
	
	
###########################################################################################################
## Informations pratiques : 
## https://nifi.apache.org/docs/nifi-docs/html/getting-started.html#downloading-and-installing-nifi	
###########################################################################################################

#####################################
## Pour lancer nifi au 1er plan : 
~/nifi/bin/nifi.sh run

## Faire "Ctrl+C" pour arrêter nifi
#####################################

#####################################
## Pour lancer nifi en tâche de fond : 
~/nifi/bin/nifi.sh start

## Pour arrêter nifi dans ce cas :
~/nifi/bin/nifi.sh stop
#####################################


#####################################
## Pour vérifer si nifi est en cours d'exécution ou non : 
~/nifi/bin/nifi.sh status 
#####################################


#####################################
## Reprenons : 
#####################################

## On lance donc nifi au 1er plan : 
~/nifi/bin/nifi.sh run

## Affichage : 
2024-05-31 11:00:43,000 INFO [main] org.apache.nifi.bootstrap.Command Generated Self-Signed Certificate Expiration: 2024-07-30
2024-05-31 11:00:43,003 INFO [main] org.apache.nifi.bootstrap.Command Generated Self-Signed Certificate SHA-256: 8A942A3EA32435BA6A1A717395E7BFDFEAEFA8BD2F511B5B8A0EA308D0B7BA3B
2024-05-31 11:00:43,103 INFO [main] org.apache.nifi.bootstrap.Command Starting Apache NiFi...
2024-05-31 11:00:43,103 INFO [main] org.apache.nifi.bootstrap.Command Working Directory: A:\Nifi
2024-05-31 11:00:43,104 INFO [main] org.apache.nifi.bootstrap.Command Command: A:\jdk-21.0.3\bin\java.exe -classpath A:\Nifi\.\conf;A:\Nifi\.\lib\jcl-over-slf4j-2.0.13.jar;A:\Nifi\.\lib\jul-to-slf4j-2.0.13.jar;A:\Nifi\.\lib\log4j-over-slf4j-2.0.13.jar;A:\Nifi\.\lib\logback-classic-1.5.6.jar;A:\Nifi\.\lib\logback-core-1.5.6.jar;A:\Nifi\.\lib\nifi-api-2.0.0-M4.jar;A:\Nifi\.\lib\nifi-framework-api-2.0.0-M4.jar;A:\Nifi\.\lib\nifi-nar-utils-2.0.0-M4.jar;A:\Nifi\.\lib\nifi-per-process-group-logging-2.0.0-M4.jar;A:\Nifi\.\lib\nifi-properties-2.0.0-M4.jar;A:\Nifi\.\lib\nifi-property-utils-2.0.0-M4.jar;A:\Nifi\.\lib\nifi-python-framework-api-2.0.0-M4.jar;A:\Nifi\.\lib\nifi-runtime-2.0.0-M4.jar;A:\Nifi\.\lib\nifi-server-api-2.0.0-M4.jar;A:\Nifi\.\lib\nifi-stateless-api-2.0.0-M4.jar;A:\Nifi\.\lib\slf4j-api-2.0.13.jar -Xmx1g -Djava.awt.headless=true -Xms1g -Djavax.security.auth.useSubjectCredsOnly=true -Dsun.net.http.allowRestrictedHeaders=true -Djava.protocol.handler.pkgs=sun.net.www.protocol -Dcurator-log-only-first-connection-issue-as-error-level=true -Dnifi.properties.file.path=A:\Nifi\.\conf\nifi.properties -Dnifi.bootstrap.listen.port=54906 -Dapp=NiFi -Dorg.apache.nifi.bootstrap.config.log.dir=A:\Nifi\bin\..\\logs org.apache.nifi.NiFi
2024-05-31 11:00:43,112 WARN [main] org.apache.nifi.bootstrap.Command Failed to set permissions so that only the owner can read pid file A:\Nifi\bin\..\run\nifi.pid; this may allows others to have access to the key needed to communicate with NiFi. Permissions should be changed so that only the owner can read this file
2024-05-31 11:00:43,115 WARN [main] org.apache.nifi.bootstrap.Command Failed to set permissions so that only the owner can read status file A:\Nifi\bin\..\run\nifi.status; this may allows others to have access to the key needed to communicate with NiFi. Permissions should be changed so that only the owner can read this file
2024-05-31 11:00:43,122 INFO [main] org.apache.nifi.bootstrap.Command Application Process [2844] launched

...



## Si on est sur Gitpod, on peut rendre le port 8443 public 
## Si besoin, on regarde les ports à l'écoute : 
## sudo apt-get install net-tools
## sudo netstat -anl | grep 8443


###########################################################################################################
## I.5°) Connexion à l'UI de Nifi :  
###########################################################################################################


## Sur le navigateur web du poste : https://localhost:8443/nifi  ( Attention : Pas 127.0.0.1)
## Remarque : il s'agit de l'URL de l'interface web traditionnelle, une nouvelle étant disponible

## On arrive ici : https://localhost:8443/nifi/login


## Remarque, sur Gitpod, l'url sera différente : 
## Exemple : https://8443-crystalloide-nifi-p50dec8hrq2.ws-eu116.gitpod.io/


## Nifi génère un login / mot de passe sécurisé par défaut, et que l'on peut retrouver ici :
## Ouvrir un nouveau terminal de commande : 
cat ~/nifi/logs/nifi-app.log | grep 'Generated'

## Affichage :
Generated Username [9a2816d1-01a9-4394-9825-5b5db5ca82bf]
Generated Password [MLAKVIqLy4S6kAoBKgB/st3L+8RtPoKc]

## On indique ensuite ces informations dans la page de login de l'UI Nifi

## Remarque, on voit au début du fichier de log nifi-app.log :
...
2024-05-31 11:00:57,959 INFO [main] o.a.n.a.s.u.SingleUserLoginIdentityProvider 
Run the following command to change credentials: nifi.sh set-single-user-credentials USERNAME PASSWORD
...



###########################################################################################################
## I.6°) La nouvelle UI apportée dans Nifi 2.0 :  
###########################################################################################################

## Comme évoqué précédemment, la nouvelle UI de Nifi 2.0 peut être testée ici, avec une URL spécifique :
https://localhost:8443/nf

## Le mode "sombre" a été notamment introduit mais pas seulement :-) 

## Voir plus d'information ici : https://community.cloudera.com/t5/Support-Questions/Testing-Nifi-2-0-0M4-New-UI-Initial-Comments-amp/m-p/388032

###########################################################################################################
# Have fun !
