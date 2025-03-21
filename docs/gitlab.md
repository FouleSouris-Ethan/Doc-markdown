# Doc pour Gitlab

>Note a moi même: Premier repos avec pipeline du sysadmin/devOps pour créer et gérer l'infrastructure avec terreform/ansible par exemple. Les devs vont ensuite déployer leurs applis sur un autre repos en pipeline sur l'infra. 

Création de compte GitLab [ici](https://gitlab.com/users/sign_in)

Le pipeline est décrit dans le fichier **.gitlab-ci.yml**, dans le repo, il contient des stages, qui contiennent eux des jobs. 

**Runners**: Serveurs qui vont servir a exécuter les pipelines.

**Les artifacts** :
Un artifact peut contenir des fichiers et/ou dossiers qui vont être stockés au sein des pipelines pour être utilisé par d’autres taches.

### Les Jobs 
 Tâches qui vont être exécutées en parallèle dans un **stage**.
On retrouve dans un job: 
Des images docker appropriées pour chaque job.
Des scripts (commandes) qui vont être exécutées dans le conteneur docker.
Des services, qui vont être lancé en parallèle du job.

Paramètres utiles:
 
 * **When** : Quand le job va être déclanché ? ex: on_success (par défaut), on_failure, always, manual. 
 * **branches** : Sur quelle branche le job va être déclanché. (Défaut: n'importes quels branches)
 * **only** : Sur quel événement le job va être déclanché. ex: push, merge_request, tag.
 * **except** : Sur quel événement le job ne va pas être déclanché.
 * **variable** : Les variables d'environnement qui vont être injectées dans le job. Dans gitlab, on les retrouve dans Settings > CI/CD > Variables.  


#Fichier .gitlab.ci.yml

L'ordre du stage est important. 
On vient d'abord déclarer les stages: 

	stages:
	   - test
	   - build
	   - deploy
 
Ensuite les jobs :

	Nom du job:
	    stage: nom du stage (le premier (test))
	    image: nom de l'image docker
		script: 
			- les commandes

Ainsi de suite.

On met le when a la fin 


##CI/CD (Continuous Integration / Continuous Deployment)   

 

Le Continuous Integration (CI), ou intégration continue, est une pratique clé du DevOps qui vise à automatiser l’intégration du code source dans un dépôt central. À chaque modification, le code est testé et validé avant d’être fusionné, garantissant ainsi une base de code toujours fonctionnelle. 

 

Fonctionnement du Continuous Integration 

L’idée du CI est simple : dès qu’un développeur apporte une modification au code, un processus automatisé se déclenche pour s’assurer que tout fonctionne correctement. Ce processus comprend généralement : 

1.Récupération du code : Vérification des nouvelles modifications depuis le dépôt Git. 

2.Compilation et Build : Construction de l’application pour s’assurer qu’elle est fonctionnelle. 

3.Exécution des tests : 

- Tests unitaires pour vérifier les fonctionnalités isolées. 

- Tests d’intégration pour s’assurer que les modules fonctionnent ensemble. 

- Tests statiques (linting, analyse de sécurité).x 

4.Analyse du code : Vérification des standards de qualité (ex: SonarQube, ESLint, Pylint). 

5.Rapport et feedback : Les résultats sont envoyés aux développeurs (succès ou échec). 

![pyramid](/home/rat/images/pyramid1.jpg)

 **Test unitaires (Unit Tests)** Très rapide ! : Différent cas de tests pour chaque fonction, cas bizarre qu’il peut se passer. Ex : Fonction qui divise a par b, que se passe-t'il si a est un une lettre, si a est un 0, que retourne la fonction ?
