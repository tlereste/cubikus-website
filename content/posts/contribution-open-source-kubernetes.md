---
title: "Mes conseils pour une 1ère contribution au projet Kubernetes"
date: 2020-04-19T16:00:00+01:00
draft: false
description: "Mes conseils pour une 1ère contribution au projet Kubernetes"

tags: ["kubernetes", "opensource"]

toc: true

featuredImage: "/images/TODO"
---

<!--more-->

## Histoire

Tout a commencé l'année dernière lors d'un entretien d'embauche pour un poste de [Site Reliability Engineer](https://landing.google.com/sre/).  
Au fil de la discussion avec le recruteur, celui-ci m'a sorti une phrase qui m'a beaucoup fait réfléchir : 
"... ici nous recherchons une personne qui, par exemple, serait capable de faire une contribution au projet Kubernetes afin d'y corriger un bug ou y ajouter une petite fonctionnalité..."

Après, une semaine de réflexion et souffrant du [syndrome de l'imposteur](https://www.duchess-france.org/jai-teste-syndrome-de-limposteur), je me suis dit, et pourquoi pas moi ?  

J'ai donc pris ça comme objectif et défi personnel et je me suis lancé dans l'aventure ! 

`<spoiler>`  
J'y suis parvenu et ma pull request (PR) a été intégrée a la version 1.18 du projet Kubernetes : https://github.com/kubernetes/kubernetes/pull/82333  
`</spoiler>`  


## Prérequis : mise en place de votre environnement

Dans cet article, je ferai un résumé des étapes pour effectuer votre première contribution au projet Kubernetes mais je ne décrirai pas l'architecture et le code du projet.  
J'ai volontairement omis ou raccourci des passages afin d'avoir un article simple.  
Vous pourrez trouver une documentation du contributeur complète et bien plus vaste ici : https://github.com/kubernetes/community/tree/master/contributors/devel#readme  

### Créer un compte Github  

Le projet Kubernetes se trouve sur Github (ainsi que tous les projets de sa fondation, la Cloud Native Computing Foundation).   
Si vous n'avez pas déjà de compte Github, il faut donc en créer un ici : https://github.com/  

### S'inscrire à Linux foundation  

Lors de la première release de Kubernetes, son créateur, Google, a créé la [Cloud Native Computing Foundation](https://www.cncf.io)(CNCF) en partenariat avec la **Fondation Linux**.
Kubernetes y fut intégré en tant que premier projet.  
Nous avons donc Kubernetes faisant partie de la **CNCF**, qui elle-même fait partie de la **Linux foundation**.  

Pour contribuer sur le projet, il faut signer une licence, la **CNCF Individual Contributor License Agreement** de la Linux foundation.
Pour cela, suivez la procédure suivante : https://github.com/kubernetes/community/blob/master/CLA.md  

### Forker le projet 

Cela consiste à faire une copie personnelle du projet sur laquelle vous pourrez créer vos propres branches, committer et pusher du code ainsi que créer des pull requests à destination du projet initial.  
À la différence d'un clone qui permettrait de récupérer le projet sur votre poste local, mais vous empêcherait de pusher des modifications sur celui-ci.   

Pour effectuer le fork, il faut aller sur le projet : https://github.com/kubernetes/kubernetes.  
Puis, cliquer sur le bouton fork en haut à droite. [IMAGE]  
Après quelques de secondes, le repository sera présent dans votre profil, exemple : https://github.com/tlereste/kubernetes  

### Cloner votre projet 

Ensuite, vous pourrez cloner votre projet précédemment forké, ce qui vous permettra d'être libre sur les modifications à y apporter.  

Si vous êtes un puriste des lignes de commande, vous pouvez cloner votre projet avec git :  
```
git clone https://github.com/tlereste/kubernetes.git .
``` 

Personnellement, j'utilise l'IDE de Jetbrains [Intellij](https://www.jetbrains.com/fr-fr/idea/) et son interface pour cette action.  
Mais vous pouvez aussi utiliser un IDE plus adapté, [Goland](https://www.jetbrains.com/fr-fr/go/) (encore chez Jetbrains).  


## Tout est en place, par où commencer ?  

Il existe de nombreuses manières de contribuer au projet Kubernetes, en voici quelques-unes :  
- développement d'une évolution
- correction d'un bug
- refactoring du code
- création de tests unitaires
- création ou mise à jour de la documentation
- traduction de la documentation en français
- mise à jour des versions des dépendances
- ...

Ce choix doit se faire en fonction de vos affinités, temps, compétences.

Pour commencer, il n'y a pas besoin de grosses contributions, les petits ruisseaux font les grandes rivières. 
La communauté encourage même les petits commits et petites pull request : [Small is better](https://github.com/kubernetes/community/blob/master/contributors/guide/pull-requests.md#2-smaller-is-better-small-commits-small-pull-requests)

Il y a des limites à tout cela, souvent sur les nouveaux projets, des personnes font la chasse aux **typos** (fautes d'orthographe) afin de devenir contributeur du projet.  

### Soumettre une nouvelle issue

Avant de créer une issue, pensez bien à vérifier qu'une issue similaire n'existe pas déjà en faisant une recherche avec les filtres.  

Puis :  
- Dans l'onglet **Issue**, cliquer sur le bouton **New Issue**.  
- Différents types d'issues seront proposés comme **Bug** ou **Enhancement**.  
- Sélectionnez le type souhaité avec le bouton **Get Started**.  
- Un template apparaitra permettant de créer l'issue. En fonction de son type, différentes informations seront demandées : 
description, version de Kubernetes utilisée... 
- Vérifiez bien en bas du template les issues similaires pour éviter les doublons : **Similar to X existing issues**

Après sa création, l'issue sera catégorisée par ([Special Interest Group](https://github.com/kubernetes/community/blob/master/sig-list.md)) ou **SIG**, c'est-à-dire des groupes fonctionnels et/ou techniques avec des leaders, newsletters, channel slack et réunions propres.  

Quelques exemples de SIG :  
- Cli : ce qui touche au client kubectl et les outils associés
- Cloud Provider : lié au cloud privé et public et notamment la neutralité envers les providers de cloud
- Storage : responsable du stockage et volumes
- ...

### Contribuer à une issue existante

Vous avez trouvé une issue qui vous plait, pensez tout d'abord à vérifier qu'elle n'est assignée à personne et que personne ne travaille dessus.
Ensuite, assignez-vous cette issue avec le commentaire `/assign`.

### La contribution    

Voici quelques conseils et astuces à utiliser lors de votre contribution.  

#### Le code

Kubernetes est développé en Golang (Go), comme c'est le cas pour la majorité des projets CNCF, par exemple [Prometheus](https://prometheus.io), [Linkerd](https://linkerd.io) ou [Helm](https://helm.sh).  
Vous trouverez ici un dashboard public Grafana listant les licences et langages utilisés par les projets CNCF :  
https://k8s.devstats.cncf.io/d/67/licenses-and-programming-languages  
N'hésitez pas à naviguer dans les autres dashboards, il y a plein d'informations intéressantes !  

Si vous n'êtes pas familier avec ce langage, un tutoriel est disponible sur le site officiel : https://tour.golang.org/  
Mais rien ne remplace un bon livre comme [Go In Action](https://www.manning.com/books/go-in-action) par exemple !

Pensez toujours à lancer les tests avant d'effectuer votre pull request avec la commande : `go test` ou `make test`

Pensez aussi à vérifier que le code est bien formaté avec l'outil à l'aide de la commande [gofmt](https://golang.org/cmd/gofmt).

Ces étapes sont décrites dans le guide du développement officiel : https://github.com/kubernetes/community/blob/master/contributors/devel/development.md  

#### La communication

Il faut savoir que toutes vos interactions doivent se faire en anglais.
Que ce soit le code, les commentaires, les échanges... 
Attention aux tournures de phrase, syntaxe et orthographe, 
n'hésitez pas à abuser des outils de traductions en ligne notamment pour communiquer avec vos interlocuteurs 
([Linguee](https://www.linguee.fr) et [DeepL](https://www.deepl.com) par exemple).

Voici un conseil qui peut paraître bateau, mais il est important de respecter les mainteneurs du projet. 
Ce sont des personnes qui prennent de leur temps libre ou du temps alloué par leur société (Redhat, Google... ) pour maintenir le projet, 
il est donc très important d'être poli, précis et clair dans les échanges que vous aurez avec eux.  

#### Git

Voici quelques commandes Git qui vous seront utiles pour la réalisation de votre pull request.  

##### Configurer votre username et email
Ce sont les mêmes qui sont utilisées sur Github et pour signer la CLA de la Linux foundation.  

```
git config --global user.name "tlereste"  
git config --global user.email lereste.thibault@gmail.com  
```

##### Maintenir votre fork à jour :
```
# A partir de votre fork cloné, ajout du "upstream" du repository distant
git remote add upstream git://github.com/tlereste/kubernetes
git fetch upstream

# Si ce n'est pas le cas, switch sur votre branche master
git checkout master

# Mise à jour de votre fork
git pull upstream master
# ou
git rebase upstream/master
```

##### Squash des commits
Il est conseillé et il vous sera probablement demandé de **squash** vos **commits**.
Cela veut dire fusionner plusieurs commits en un seul afin de garder un historique git propre.  
Voici un très bon article indiquant comment effectuer cette action : 
https://www.ekino.com/articles/comment-squasher-efficacement-ses-commits-avec-git 

## Et après la pull request ?

Le processus d'intégration / déploiement continue (CI/CD) est effectué par [Prow](https://github.com/kubernetes/test-infra/blob/master/prow/README.md).
C'est un outil dédié et développé par le projet Kubernetes. Il utilise les événements de Github pour déclencher des actions mais fonctionne aussi en mode **ChatOps**. 
Cela signifie qu'en saisissant certains mots clés dans les commentaires, Prow déclenchera des actions.  
La liste des mots clé / actions est décrite ici : https://prow.k8s.io/command-help?repo=kubernetes%2Fkubernetes  
Afin d'avoir un côté visuel à tout cela, un robot nommé [@k8s-ci-robot](https://github.com/k8s-ci-robot) fera le lien entre votre PR et Prow.
  
  
Les membres du projet peuvent obtenir 1 des 2 statuts suivants :  
- **reviewers** qui effectuent les revues de code
- **approvers** qui mergent le code (et peuvent aussi effectuer les revues de code)
  
La liste des reviewers et approvers est disponible ici :  
- [OWNERS](https://github.com/kubernetes/kubernetes/blob/master/OWNERS) pour tous les projets
- [OWNERS_ALIASES](https://github.com/kubernetes/kubernetes/blob/master/OWNERS_ALIASES) pour les SIG
  
Lorsqu'une pull request est effectuée, elle sera automatiquement assignée à 2 **reviewers** et 1 **approver** les plus à même de la traiter.
Si vous souhaitez l'assigner à une personne en plus, vous pouvez saisir le commentaire `/assign @username`.
  
Un **reviewer** doit valider la PR avec le commentaire `/lgtm` qui signifie **look good too me**.
Ensuite, un **approver** merge la PR avec le commentaire `/approve`.

Si votre PR est bloquée ou si vous avez besoin d'aide, plusieurs solutions s'offrent à vous :  
- Dans Github, vous pouvez relancer une personne en spécifiant son username préfixé d'un @ afin qu'elle soit notifiée.   
- Il existe aussi une grande communauté sur le **Slack** officiel : https://kubernetes.slack.com. Vous pouvez contacter la personne directement ou demander de l'aide ou une relecture sur le channel correspondant.

Quelques exemples de channels utiles :  
- \#announcements : les annonces des projets CNCF, nouvelles versions, failles de sécurité, événements...
- \#kubernetes-users : les utilisateurs de Kubernetes, questions variées
- \#fr-users : les utilisateurs français de Kubernetes
- \#kubernetes-docs-fr : les traducteurs de la doc Kubernetes en français
- \#kube-state-metrics : questions, pull requests, annonces liées au projet kube-state-metrics
- ...

Si vous avez des retours sur votre pull request, si celle-ci donne lieu a de nouveaux commit, pensez bien à refaire les étapes mentionnées plus haut : 
Squash des commit, relance des tests unitaires, relance du check du formatage gofmt.


## Difficultés rencontrées, retour d'expérience  

J'avais choisi de contribuer sur le repo principal du projet : [kubernetes/kubernetes](https://github.com/kubernetes/kubernetes).  
C'était une bonne expérience mais ce n'est pas ce que je conseillerais à quelqu'un qui souhaiterait effectuer sa première pull request.  

Ce repo est vertigineux, il contient de nombreuses issues, beaucoup de contributeurs et tout se passe très vite. Au moment où j'écris cet article, il y a :  
- 2003 issues ouvertes 
- 895 pull request en cours

C'est très difficile d'accéder à une nouvelle issue avant qu'une personne avec une plus grande connaissance ou plus expérimenté ne la prenne en charge.

De plus, dans mon cas, le processus de prise en charge et relecture de l'issue a été très long. Cela s'explique par le fait que les mainteneurs du projet étaient occupés à créer la release de la version 1.17 de Kubernetes et aussi au fait que mon issue concernait une fontionnalité non critique et non prioritaire.  

Pour information, ma [pull request](https://github.com/kubernetes/kubernetes/pull/82333) a été :
- créée le 4 septembre :   
- relue le 7 janvier  
- mergée le 15 janvier  

Ce qui fait une durée de 4 mois. Soyez patient !

## Conseils  

Pour débuter, et ça n'engage que moi, je vous conseillerais, plutôt que de contribuer principal, de contribuer sur d'autres repository plus petits de l'organisation Kubernetes.  

Après cette première pull request, j'ai choisi de contribuer sur d'autres projets de l'organisation :
- kube-state-metrics : génère des métriques au format Prometheus de l'état des objets Kubernetes  
- krew et krew-index : gestionnaire de paquets pour les plugins de kubectl 

Pour Krew, j'ai par exemple modifié la documentation pour y ajouter [l'outil Popeye](https://thibault-lereste.fr/2020/04/kubernetes-popeye/).  

L'organisation Kubernetes comporte 69 repository, vous avez l'embarras du choix !
Par exemple :  
- ingress-nginx
- kops
- dashboard
- ...

Des projets plus petits seront plus faciles à appréhender, aussi bien au niveau de l'architecture, qu'au niveau fonctionnel. 
De plus, vous serez moins en concurence avec d'autres personnes, vous aurez plus de temps pour choisir une issue, des feedbacks plus rapides sur vos pull requests, 
bref que des avantages !  

Une fois un projet / repository choisi, il faut sélectionner une issue.  

Je vous conseille d'effectuer une recherche sur le label `good first issue`. 
Cela correspond à des issues assez simples taggées par les mainteneurs ou contributeurs du projet.  
[IMAGE]
Le compte Twitter [goodfirstissue](https://twitter.com/goodfirstissue) tweet automatiquement les nouvelles "good first issue".

Si vous souhaitez simplement aider quelqu'un sur un problème ou une question, effectuez une recherche avec le label `help wanted`.


## D'autres moyens de contribuer

### Hacktoberfest 

C'est un événement qui a lieu du 1er au 31 octobre de chaque année.  
Il est organisé par [DigitalOcean](https://www.digitalocean.com), Github et [Dev.to](Dev.to) 
pour promouvoir l'open source aussi bien pour les débutants que pour les expérimentés.  
Les 50000 premières personnes à effectuer 4 pull requests gagnent un t-shirt !  

Voici le site de l'événément : https://hacktoberfest.digitalocean.com/ 

### Bug bounty

Pour les plus téméraires, il est possible de participer au **bug bounty**.  
La remontée de failles de sécurité peut être rémunérée en fonction de la criticité de la faille et le domaine touché.   

Plus d'information ici : https://hackerone.com/kubernetes  
