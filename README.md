### Apache Nifi pour des TPs de formation dans un environnement Linux ou virtualisé ou en ligne "Gitpod"

### Rappel pour retrouver les environnements Gitpod éventuellement précédemment instanciés : [ https://gitpod.io/workspaces ](https://gitpod.io/workspaces)

Nous allons installer un serveur stand alone Nifi sur un environnement virtuel accessible à partir d'un simple navigateur web, à des fins de développement et de formation. 

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/crystalloide/Nifi
)

__________________________________________________________________________________
______________________________________
#### TP : Installation Apache Nifi 2.3.0 sur Linux : 
#### 		   https://nifi.apache.org/documentation/v2/
______________________________________

## JDK Java 21
## Les proccesseurs basés sur Python nécessitent: Python 3.9, 3.10, 3.11, ou 3.12

## VM à charger dans VirtualBox : Ubuntu_24.04.2_java_docker_python_2025-02-20.ova

______________________________________
## I°) 	Installation mode stand alone sans zookeeper : 
##	Site : https://nifi.apache.org/download/
##      https://dlcdn.apache.org/nifi/ 
______________________________________
## Aller sur le paragraphe "binaries" et cliquer sur la ligne "NiFi Standard 2.3.0" 
## Nous arrivons sur la page : https://www.apache.org/dyn/closer.lua?path=/nifi/2.3.0/nifi-2.3.0-bin.zip
## Ce qui nous donne finalement le lien de téléchargement suivant qu'on utilisera plus loin : 
## https://dlcdn.apache.org/nifi/2.3.0/nifi-2.3.0-bin.zip
______________________________________

______________________________________
## Dans un terminal :
______________________________________

## Se connecter avec le user "user" ou sinon : 
su - user


______________________________________
## On se place sur le répertoire souhaité pour faire l'installation : 
______________________________________

cd ~

pwd

## Affichage répertoire par défaut et courant : 
## /home/user


______________________________________
## Choix de la version du JDK : ici JDK 21 : 
______________________________________
## Installation d'OpenJDK 21 à partir des repository :
sudo apt-get update && sudo apt-get -y install openjdk-21-jdk 


## Configuration pour choisir la version Java par défaut : 
sudo update-alternatives --config java

## Il existe 3 choix pour l'alternative java (qui fournit /usr/bin/java).

  Sélection   Chemin                                       Priorité  État
------------------------------------------------------------
  0            /usr/lib/jvm/java-21-openjdk-amd64/bin/java   2111      mode automatique
* 1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java   1111      mode manuel
  2            /usr/lib/jvm/java-17-openjdk-amd64/bin/java   1711      mode manuel
  3            /usr/lib/jvm/java-21-openjdk-amd64/bin/java   2111      mode manuel


## On choisit "3" pour le jdk 21 ici : 

## Appuyez sur <enter> pour conserver le choix actuel [*], ou tapez le numéro de sélection : 3
## update-alternatives: utilisation de « /usr/lib/jvm/java-21-openjdk-amd64/bin/java » pour fournir « /usr/bin/java » (java) en mode manuel


## Configuration pour choisir la version Javac par défaut : 
sudo update-alternatives --config javac

## Il existe 3 choix pour l'alternative javac (qui fournit /usr/bin/javac).

  Sélection   Chemin                                        Priorité  État
------------------------------------------------------------
  0            /usr/lib/jvm/java-21-openjdk-amd64/bin/javac   2111      mode automatique
* 1            /usr/lib/jvm/java-11-openjdk-amd64/bin/javac   1111      mode manuel
  2            /usr/lib/jvm/java-17-openjdk-amd64/bin/javac   1711      mode manuel
  3            /usr/lib/jvm/java-21-openjdk-amd64/bin/javac   2111      mode manuel

## On choisit "3" pour le jdk 21 ici : 

## Appuyez sur <enter> pour conserver le choix actuel [*], ou tapez le numéro de sélection : 3
## update-alternatives: utilisation de « /usr/lib/jvm/java-21-openjdk-amd64/bin/javac » pour fournir « /usr/bin/javac » (javac) en mode manuel


## On vérifie : 

java -version
## Affichage : 
## 	openjdk version "21.0.6" 2025-01-21
## 	OpenJDK Runtime Environment (build 21.0.6+7-Ubuntu-124.04.1)
## 	OpenJDK 64-Bit Server VM (build 21.0.6+7-Ubuntu-124.04.1, mixed mode, sharing)


javac -version
## Affichage : 
##	javac 21.0.6




export JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64/ 

echo $JAVA_HOME 
## Affichage :
## /usr/lib/jvm/java-21-openjdk-amd64/


sudo vi /etc/profile
## Rajouter à la fin : 
JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64/

## 
source /etc/profile


vi ~/.bashrc 
export JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64/
export PATH=/usr/lib/jvm/java-21-openjdk-amd64/bin:$PATH
## export JAVA_HOME=~/jdk
## export PATH=~/jdk/bin:$PATH

source ~/.bashrc


su - user

echo $JAVA_HOME 
echo $PATH 



______________________________________
## I.2°) Nettoyage des installations précédentes éventuelles :  
______________________________________
cd ~
rm -Rf ~/nifi



______________________________________
## I.3°) Installation de Nifi 2.3.0 :  
______________________________________
cd ~

rm ~/nifi-2.3.0-bin.zip

wget https://dlcdn.apache.org/nifi/2.3.0/nifi-2.3.0-bin.zip

ll *.zip

unzip nifi-2.3.0-bin.zip

mv nifi-2.3.0 nifi

rm ~/nifi-2.3.0-bin.zip

cd nifi

ls ~/nifi/
## Affichage : 
	bin/  conf/  docs/  extensions/  lib/  LICENSE  NOTICE  python/  README

## On constate qu'à l'issue de la toute 1ère installation, il y a peu de répertoires présents.
## Certains répertoires/fichiers seront en effet créés au tout 1er lancement 
## (d'où le délai nécessaire constaté au 1er lancement de Nifi ) 


## On ajoute les binaires nifi au PATH : 
vi ~/.bashrc

export PATH=~/nifi/bin:$PATH

## Prise en compte :  
source ~/.bashrc


## Version de python installée : 
python --version
## Affichage : 
	Python 3.12.3



## Etape optionnelle avant lancement  :

ls ~/nifi/conf 

## Affichage : 
##		authorizers.xml  bootstrap.conf  logback.xml  login-identity-providers.xml  nifi.properties  state-management.xml  zookeeper.properties
##

## On peut préciser un password dans le fichier de configuration nifi.properties 
## au niveau du paramètre "nifi.sensitive.props.key" (ligne 186)

vi ~/nifi/conf/nifi.properties 


## On remarque au passage l'emplacement où l'URL et le port sont indiqués :
## (Ligne 161 et 162)
nifi.web.https.host=localhost
nifi.web.https.port=8443



______________________________________
## I.4°) Lancement de Nifi :  
______________________________________

cd ~/nifi/bin

ls
## Affichage : 
	nifi.cmd  nifi-env.cmd  nifi-env.sh  nifi.sh

	
	
______________________________________
## Informations pratiques : 
## https://nifi.apache.org/docs/nifi-docs/html/getting-started.html#downloading-and-installing-nifi	
______________________________________

______________________________________
## Pour lancer nifi au 1er plan : 
~/nifi/bin/nifi.sh run

## Faire "Ctrl+C" pour arrêter nifi
______________________________________

______________________________________
## Pour lancer nifi en tâche de fond : 
~/nifi/bin/nifi.sh start

## Pour arrêter nifi dans ce cas :
~/nifi/bin/nifi.sh stop
______________________________________


______________________________________
## Dans un autre terminal : 
______________________________________
## Pour vérifer si nifi est en cours d'exécution ou non : 
~/nifi/bin/nifi.sh status 

## Affichage : 
## 
## 	JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64/
## 	NIFI_HOME=/home/user/nifi
## 
## 	2025-02-28 16:47:02,208 INFO [main] org.apache.nifi.bootstrap.Command Application Process [23184] Management Server [http://127.0.0.1:52020/health] communication failed
## 

## > Le service n'est probablement pas encore démarré : 


## Si besoin, sur un autre terminal, on regarde les ports à l'écoute : 
sudo netstat -anl | grep 8443

## Affichage attendu une fois Nifi démarré : 
	tcp6       0      0 127.0.0.1:8443          :::*                    LISTEN    


## On retente après quelques instants : 

~/nifi/bin/nifi.sh status 

## Affichage : 
## 
##	JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64/
##	NIFI_HOME=/home/user/nifi
##
##	2025-02-28 16:47:13,182 INFO [main] org.apache.nifi.bootstrap.Command Application Process [23184] Command Status [SUCCESS] HTTP 200
##	2025-02-28 16:47:13,186 INFO [main] org.apache.nifi.bootstrap.Command Status: UP
##




______________________________________
## I.5°) Connexion à l'UI de Nifi :  
______________________________________

## Sur le navigateur web du poste : https://localhost:8443/nifi  (Attention : Pas 127.0.0.1)
## Remarque : il s'agit de l'URL de l'interface web traditionnelle, une nouvelle étant disponible

## On arrive ici : https://localhost:8443/nifi/login

## Remarque, sur Gitpod, l'url sera différente : 
## Exemple : https://8443-crystalloide-nifi-p50dec8hrq2.ws-eu116.gitpod.io/

## Jetons un oeil sur les fichiers de logs : 
 
ls ~/nifi/logs/nifi*.log

/home/user/nifi/logs/nifi-app.log        /home/user/nifi/logs/nifi-deprecation.log  /home/user/nifi/logs/nifi-user.log
/home/user/nifi/logs/nifi-bootstrap.log  /home/user/nifi/logs/nifi-request.log



## Nifi génère un login / mot de passe sécurisé par défaut, et que l'on peut retrouver ici :
## Ouvrir un nouveau terminal de commande : 
cat ~/nifi/logs/nifi-app.log | grep 'Generated'
## ou :
cat ~/nifi/logs/nifi*.log | grep 'Generated'



## Affichage :
Generated Username [2d3614bf-6f45-455c-951c-7b9667e381db]
Generated Password [JR/W5BuN++2yLTIjMSZVWmtkGv6iJA3u]



## On indique ensuite ces informations dans la page de login de l'UI Nifi

## Remarque, si on regarde dans le fichier de log : 
cat /home/user/nifi/logs/nifi-app.log | grep credentials

## On trouve une indication permettant de changer le user mot de passe choisi au 1er démarrage :
## Affichage : 
...
2025-02-28 16:47:04,473 INFO [main] o.a.n.a.s.u.SingleUserLoginIdentityProvider Run the following command to change credentials: 
nifi.sh set-single-user-credentials USERNAME PASSWORD
...



______________________________________
## I.6°) La nouvelle UI apportée dans Nifi 2.0 :  https://localhost:8443
______________________________________

## Une nouvelle UI a été apportée dans Nifi 2.x :
## Le mode "sombre" a été notamment introduit mais pas seulement :-) 

## Voir plus d'information ici : https://community.cloudera.com/t5/Support-Questions/Testing-Nifi-2-0-0M4-New-UI-Initial-Comments-amp/m-p/388032



______________________________________
## I.7°) Les paramètres disponibles avec nifi.sh
______________________________________
nifi.sh

## Affichage :
	Usage nifi.sh {start|stop|decommission|run|restart|status|cluster-status|diagnostics|status-history|set-sensitive-properties-algorithm|set-sensitive-properties-key|set-single-user-credentials}



______________________________________
## I.8°) Pour arrêter nifi : 
______________________________________
nifi.sh stop

## Affichage :

## 	JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64/
## 	NIFI_HOME=/home/user/nifi
## 
## 	2025-02-28 17:03:30,413 INFO [main] org.apache.nifi.bootstrap.Command Application Process [23184] termination requested
## 	2025-02-28 17:03:31,051 INFO [main] org.apache.nifi.bootstrap.Command Application Process [23184] termination completed


nifi.sh status 

## Affichage :

## 	JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64/
## 	NIFI_HOME=/home/user/nifi
## 
## 	2025-02-28 17:04:38,407 INFO [main] org.apache.nifi.bootstrap.Command Application Process STOPPED



______________________________________
## Fin du TP02a : Nifi 2.3.0
______________________________________

______________________________________
# Have fun !
______________________________________
