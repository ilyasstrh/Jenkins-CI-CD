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
