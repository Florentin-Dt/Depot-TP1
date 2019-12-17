## Jenkins:
### Utilité
Pour d'automatiser le processus d'intégration continue.

### Démarrage
Lancer Jenkins

    java -jar jenkins.war
    
Ensuite se rendre sur 

    localhost:8080

Identifiants : 

    Login: admin
    Mdp: admin

### Dossier de config de Jenkins + workspace deployment:

	/Users/florentin/.jenkins
	
(dossier généré au moment du lancement du WAR si il n'existe pas)
Le dossier workspace contient la derniere version de chaque projet configuré sur Jenkins.

### Liste de tous les jobs de chaque projet/item:

	/Users/florentin/.jenkins/jobs
	
Accès à tous les projet
On a accès à tous les jobs et dans le dossier archive de chaque jobs, ce que l'on a spécifier comme archive (artefact en générale) dans Jenkins ou dans le pipeline

### Emplacement de la documentation/logs des plugins:

    target/site 
    
### Plugin Jenkins requis

    - Warning Next Generation (pour Checkstyle, pmd, spotBugs)
    - Pipeline utility steps (pour la fonction readMavenPom)
    - Maven Integration Plugin
    - Pipeline

## Nexus

### Utilité
Nexus est un gestionnaire repository pour y stocker les .jar, .war ou autres des applications. Cela correspond à l'étape de publication de l'intégration continue.
Il dispose également de service permettant de contrôler la vulnérabilité/faille de sécurité de l'application.

### Configuration 
#### Jenkins

Se rendre dans l'administration générale de Jenkins, Configurer le système.
Section Sonatype Nexus.

Choisir Add Nexus Repository Manager Server

Exemple: 
        
        Display Name : Nexus_localhost
        Server ID : Nexus_localhost
        Server URL : http://localhost:8081

#### Maven 

Il est également nécessaire de configurer l'accès au repository Nexus avec Maven.

Dans le fichier setting.xml de Apache Maven, dans la balise servers, rajouter:
        
        <servers>
            <server>
                <id>nexusLocal</id>
                <username>admin</username>
                <password>admin</password>
            </server>
        </servers>
        
Cet id sera nécessaire dans le Jenkinsfile.

### Démarrage
Lancer Nexus

    cd nexus-3.20.0-04-mac/nexus-3.20.0-04/bin
    ./nexus start
    
Accéder à l'inferface web
    
    http://localhost:8081
    
Attention de bien se connecter en tant qu'admin en cliquant en haut à droite.