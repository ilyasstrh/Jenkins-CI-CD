# Atelier Jenkins [GL] 
![License](https://img.shields.io/badge/jenkins-miola-green)  
Merci de suivre ces étapes pour réaliser le tp.
## Fork the project

Cliquer sur le bouton Fork pour créer une copie du projet sur votre compte.


## Créer un nouveau projet Jenkins

Sous "Source Code Management", sélectionnez Git et fournissez le lien vers le référentiel Github dans "URL du référentiel". Laisser la branche master, car laquelle qu'on va utiliser pour accéder au référentiel.  
Dans la section "Build", choisissez "Invoke top-level Maven target" dans le menu déroulant "Add build step".  
Goals: 
```bash
clean package
```
Pour tester, veuillez lancer le build manuellement.


## Build automatique
Maintenant on va automatiser le process de build de notre application. 

Aller à la page de configuration de notre projet, dans la section "Build Triggers", cochez les deux cases "Build periodically" et "Poll SCM" et mettez les valeurs cron pour réaliser le build à chaque minute:
```bash
* * * * *
``` 

## Continous Delivery
Dans cette étape, on va réaliser le déploiement de notre application sur un serveur distant, l'@IP, username et password, seront mis à votre disposition lors de l'atelier, ou vous pouvez même deployer l'application localement sur votre serveur [Tomcat](tomcat.apache.org) si il'est déjà installé. Sinon pas de soucis !  
Pour réaliser cette partie, nous aurons besoin du plugin "Deploy to container". Retournons à la page de configuration de notre projet, défilez à la section "Post-build actions", et ajouter une étape "Archive the artifacts". "Files to archive":

```bash
**/*.war
```
Pour automatiser le déploiement, et sur la même section, ajouter une autre étape Deploy war/ear to a container.  

WAR/EAR files:
```bash
**/*.war
```  

Context path:  
```bash
MiolaApplication
```  

Containers:
```bash
# Séléctionner Tomcat 8.x, vous mettez vos credentials d'authentification, sinon on vous donnez ceux de notre serveur.
```  

Sauvegardez, et vérifiez les changements !
## Pipeline
Pour la partie pipeline, veuillez copier ce code:
```pipeline
#Atelier Jenkins - MIOLA
pipeline {
    agent any
        stages {
                stage ('Git-Checkout') {
                    steps {
                            echo "checking";
                            git 'https://github.com/chayma981217/miola_at.git'
}
}
        stage ('Testing Stage') {
                steps {
                    echo "Build";
                    sh label: '', script: 'javac Helloworld.java';
                    sh label: '', script: 'java Helloworld'
                                       
          

}
}
stage ('Unit-test') {
steps {
echo "running junit tests";
}
}
stage ('Quality-Gate') {
steps {
echo "verify";
}
}
stage ('Deploy') {
steps {
echo "Deploy tests";
}
}
}
  
}
```

Enjoy!  
Miola, chaque jour une belle histoire. :smiley:
