## Pour lancer Jenkins:
Lancer Jenkins

    java -jar jenkins.war
    
Ensuite se rendre sur 

    localhost:8080
       
Login/Mdp: admin admin

## Dossier de config de Jenkins + workspace deployment:

	/Users/florentin/.jenkins
	
(dossier généré au moment du lancement du WAR si il n'existe pas)
Le dossier workspace contient la derniere version de chaque projet configuré sur Jenkins.

## Liste de tous les jobs de chaque projet/item:

	/Users/florentin/.jenkins/jobs
	
Accès à tous les projet
On a accès à tous les jobs et dans le dossier archive de chaque jobs, ce que l'on a spécifier comme archive dans Jenkins ou dans le pipeline

## Emplacement de la documentation/logs des plugins:

    target/site 
