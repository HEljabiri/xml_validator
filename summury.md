#Introduction

L'objectif de ce travail est la création d'un outil qui permet de valider un fichier xml par rapport à un schéma de définition xsd.

Pour ce faire, on propose de monter une image Docker qui exposera le service de validation portable sur les différents systèmes d'exploitation: Windows, Mac Os, Linux. 

L'image hanane/xml_validator est donc la solution proposée dans ce projet.

Nous détaillons dans cette page la méthodologie de création de cette image ainsi que la façon de l'utiliser.

# Les étapes de création de l’image hanane/xml_validator :v3

1)	Récupération de l’image ubuntu :14.04 du dépôt Git de Docker 

2)	Création d’une image propre au validateur à partir de l’image ubuntu :14.04

- Création d’un nouveau répertoire : mkdir xml_validator
- Se positionner dans le répertoire créé : cd xml_validator
- Création d’un fichier Dockerfile contenant les intructions à faire pour la création de la nouvelle étape :

**FROM ubuntu:14.04
MAINTAINER Hanane Eljabiri <hanane.eljabiri@gmail.com>
RUN apt-get update && apt-get -y install libxml2-dev**

- Construction de la nouvelle image :

**Build –t hanane/xml_validator :v3**
 
3)	Sauvegarde de l’image construite et export

**Docker save –o xml_validator.tar hanane/xml_validator:v3**

#Les étapes d’utilisation de l’image hanane/xml_validator:v3

1)	Import de l’image

**Docker load –i xml_validator.tar**

2)	Création d’un container en lui allouant un volume

**Docker run –t –i –v  chemin_host:chemin_container hanane/xml_validator :v3**

#####Remarque : 

le template du chemin du dossier host  dépend du système d’exploitation host, par exemple sur windows, le chemin doit respecter le template suivant :

//c/Users/user/chemin

3)	Valider le XML à l’aide d’un xsd

**Xmllint –schema annuaire.xsd annuaire.xml D:\3eme_ENSG\xml_validator**

#####Exemple:

![Exmple d'utilisation du container pour la validation du fichir annuaire.xml](ressources/exemple.png "")

