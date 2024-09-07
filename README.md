# Apache Nifi pour des TPs de formation dans un environnement Linux ou virtualisé ou en ligne "Gitpod"


## Rappel pour retrouver les environnements Gitpod éventuellement précédemment instanciés : [ https://gitpod.io/workspaces ](https://gitpod.io/workspaces)

Nous allons installer un serveur stand alone Nifi sur un environnement virtuel accessible à partir d'un simple navigateur web, à des fins de développement et de formation. 

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/crystalloide/Nifi
)

###########################################################################################################
### 0°) Installation de JDK Java 21 LTS  :
###########################################################################################################

## On installe le JDK 21 LTS via la commande : 

sudo apt-get install openjdk-21-jdk

###########################################################################################################
## 1°) Vérifions que Java est bien installé : 
###########################################################################################################

java -version

## Affichage : 

	java version "17.0.3.1" 2022-04-22 LTS
	Java(TM) SE Runtime Environment (build 17.0.3.1+2-LTS-6)
	Java HotSpot(TM) 64-Bit Server VM (build 17.0.3.1+2-LTS-6, mixed mode, sharing)
 
###########################################################################################################
## I°) 	Installation mode stand alone sans zookeeper : 
##		Site : https://nifi.apache.org/download/
###########################################################################################################

## Aller sur le paragraphe "binaries" et cliquer sur la ligne "NiFi Standard 2.0.0-M3" (car M3 disponible au 31-05-2024)

## A savoir : "M" = Milestone

## Nous arrivons sur la page : https://www.apache.org/dyn/closer.lua?path=/nifi/2.0.0-M3/nifi-2.0.0-M3-bin.zip

## Ce qui nous donne finalement le lien de téléchargement suivant : 
https://dlcdn.apache.org/nifi/2.0.0-M3/nifi-2.0.0-M3-bin.zip



###########################################################################################################
## On se place sur le répertoire souhaité d'installation : 
## Dans un terminal Git Bash : 
###########################################################################################################

cd a:

pwd




###########################################################################################################
## I.1°) Pre-requis : Installation de Java 21 : 
###########################################################################################################

###########################################################################################################
## Installation jdk Java 21 : 
## https://www.oracle.com/java/technologies/downloads/#java21
## Pour windows : https://www.oracle.com/java/technologies/downloads/#jdk21-windows
###########################################################################################################


## Archive à décompresser : https://download.oracle.com/java/21/latest/jdk-21_windows-x64_bin.zip

## On décompresse et on obtient dans notre cars un répertoire "jdk-21.0.3" dans a:


## On va exporter un JAVA_HOME dans le terminal Git Bash : 

export JAVA_HOME='/a/jdk-21.0.3'

echo $JAVA_HOME
## Affichage : 
	/a/jdk-21.0.3


/a/jdk-21.0.3/bin/java -version
## Affichage : 
	java version "21.0.3" 2024-04-16 LTS
	Java(TM) SE Runtime Environment (build 21.0.3+7-LTS-152)
	Java HotSpot(TM) 64-Bit Server VM (build 21.0.3+7-LTS-152, mixed mode, sharing)


export PATH=$JAVA_HOME/bin:$PATH

echo $PATH

java -version
## Affichage : 
	java version "21.0.3" 2024-04-16 LTS
	Java(TM) SE Runtime Environment (build 21.0.3+7-LTS-152)
	Java HotSpot(TM) 64-Bit Server VM (build 21.0.3+7-LTS-152, mixed mode, sharing)
	


###########################################################################################################
## I.2°) Nettoyage des installations précédentes éventuelles :  
###########################################################################################################
rm -Rf /Nifi

###########################################################################################################
## I.3°) Installation de Nifi 2.0 :  
###########################################################################################################
## Wget pour windows : http://gnuwin32.sourceforge.net/packages/wget.htm

wget https://dlcdn.apache.org/nifi/2.0.0-M3/nifi-2.0.0-M3-bin.zip

unzip nifi-2.0.0-M3-bin.zip
mv nifi-2.0.0-M3 Nifi
ls a:/Nifi 

## Affichage : 
	bin/  conf/  docs/  extensions/  lib/  LICENSE  NOTICE  python/  README

## On constate quà l'issue de la toute 1ère installation, il y a peu de répertoires présents.
## Certains répertoires/fichiers seront crées au tout 1er lancement (d'où le délai nécessaire constaté au 1er lancement de Nifi ) :


export PATH=/a/Nifi/bin:$PATH

echo $PATH

###########################################################################################################
## I.4°) Lancement de Nifi :  
###########################################################################################################

cd a:
cd /Nifi/bin

ls
## Affichage : 
	dump-nifi.bat  nifi.cmd  nifi.sh*  nifi-env.bat  nifi-env.cmd  nifi-env.sh*  run-nifi.bat  status-nifi.bat
	
	
run-nifi.bat

## Affichage : 
2024-05-31 11:00:43,000 INFO [main] org.apache.nifi.bootstrap.Command Generated Self-Signed Certificate Expiration: 2024-07-30
2024-05-31 11:00:43,003 INFO [main] org.apache.nifi.bootstrap.Command Generated Self-Signed Certificate SHA-256: 8A942A3EA32435BA6A1A717395E7BFDFEAEFA8BD2F511B5B8A0EA308D0B7BA3B
2024-05-31 11:00:43,103 INFO [main] org.apache.nifi.bootstrap.Command Starting Apache NiFi...
2024-05-31 11:00:43,103 INFO [main] org.apache.nifi.bootstrap.Command Working Directory: A:\Nifi
2024-05-31 11:00:43,104 INFO [main] org.apache.nifi.bootstrap.Command Command: A:\jdk-21.0.3\bin\java.exe -classpath A:\Nifi\.\conf;A:\Nifi\.\lib\jcl-over-slf4j-2.0.13.jar;A:\Nifi\.\lib\jul-to-slf4j-2.0.13.jar;A:\Nifi\.\lib\log4j-over-slf4j-2.0.13.jar;A:\Nifi\.\lib\logback-classic-1.5.6.jar;A:\Nifi\.\lib\logback-core-1.5.6.jar;A:\Nifi\.\lib\nifi-api-2.0.0-M3.jar;A:\Nifi\.\lib\nifi-framework-api-2.0.0-M3.jar;A:\Nifi\.\lib\nifi-nar-utils-2.0.0-M3.jar;A:\Nifi\.\lib\nifi-per-process-group-logging-2.0.0-M3.jar;A:\Nifi\.\lib\nifi-properties-2.0.0-M3.jar;A:\Nifi\.\lib\nifi-property-utils-2.0.0-M3.jar;A:\Nifi\.\lib\nifi-python-framework-api-2.0.0-M3.jar;A:\Nifi\.\lib\nifi-runtime-2.0.0-M3.jar;A:\Nifi\.\lib\nifi-server-api-2.0.0-M3.jar;A:\Nifi\.\lib\nifi-stateless-api-2.0.0-M3.jar;A:\Nifi\.\lib\slf4j-api-2.0.13.jar -Xmx1g -Djava.awt.headless=true -Xms1g -Djavax.security.auth.useSubjectCredsOnly=true -Dsun.net.http.allowRestrictedHeaders=true -Djava.protocol.handler.pkgs=sun.net.www.protocol -Dcurator-log-only-first-connection-issue-as-error-level=true -Dnifi.properties.file.path=A:\Nifi\.\conf\nifi.properties -Dnifi.bootstrap.listen.port=54906 -Dapp=NiFi -Dorg.apache.nifi.bootstrap.config.log.dir=A:\Nifi\bin\..\\logs org.apache.nifi.NiFi
2024-05-31 11:00:43,112 WARN [main] org.apache.nifi.bootstrap.Command Failed to set permissions so that only the owner can read pid file A:\Nifi\bin\..\run\nifi.pid; this may allows others to have access to the key needed to communicate with NiFi. Permissions should be changed so that only the owner can read this file
2024-05-31 11:00:43,115 WARN [main] org.apache.nifi.bootstrap.Command Failed to set permissions so that only the owner can read status file A:\Nifi\bin\..\run\nifi.status; this may allows others to have access to the key needed to communicate with NiFi. Permissions should be changed so that only the owner can read this file
2024-05-31 11:00:43,122 INFO [main] org.apache.nifi.bootstrap.Command Application Process [2844] launched

...


###########################################################################################################
## I.5°) Connexion à l'UI de Nifi :  
###########################################################################################################

## Sur le navigateur web du poste : https://localhost:8443/nifi  ( Attention : Pas 127.0.0.1)
## Remarque : il s'agit de l'URL de l'interface web traditionnelle, une nouvelle étant disponible

## On arrive ici : https://localhost:8443/nifi/login

## Nifi génère un login / mot de passe sécurisé par défaut, et que l'on peut retrouver ici :

## Dans un nouveau terminal : 
cd a:
cat /a/Nifi/logs/nifi-app.log | grep 'Generated'

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

## Voir plus d'information ici : https://community.cloudera.com/t5/Support-Questions/Testing-Nifi-2-0-0M3-New-UI-Initial-Comments-amp/m-p/388032


## 17°) Pour arrêter le cluster :

    docker compose down


# Have fun !
