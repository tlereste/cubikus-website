---
title: "Mes conseils pour une 1ère contribution au projet Kubernetes"
date: 2020-04-19T16:00:00+01:00
draft: false
description: "Mes conseils pour une 1ère contribution au projet Kubernetes"

tags: ["kubernetes", "opensource"]

toc: true

featuredImage: "/images/contribution-open-source-kubernetes/contribution-open-source-kubernetes-featured.png"
images:
- "/images/contribution-open-source-kubernetes/contribution-open-source-kubernetes-twitter.png"
---

<!--more-->

## Histoire

Tout a commencé l'année dernière, lors d'un entretien d'embauche pour un poste de [Site Reliability Engineer](https://landing.google.com/sre).  
Au fil de la discussion avec le recruteur, celui-ci m'a sorti une phrase qui m'a beaucoup fait réfléchir :  
> ... ici nous recherchons une personne qui, par exemple, serait capable de faire une contribution au projet Kubernetes afin d'y corriger un bug ou y ajouter une petite fonctionnalité...

Après une semaine de réflexion et doutant souvent de compétence et succès (je souffre du [syndrome de l'imposteur](https://www.duchess-france.org/jai-teste-syndrome-de-limposteur)), je me suis dit, et pourquoi pas moi ?  

J'ai donc pris ça comme objectif et défi personnel et je me suis lancé dans l'aventure !  
  
{{< admonition success "Avec succès" >}}
J'y suis parvenu et ma pull request (PR) a été intégrée à la version 1.18 du projet Kubernetes : https://github.com/kubernetes/kubernetes/pull/82333  
{{< /admonition >}}
  
## Prérequis : mise en place de votre environnement

Dans cet article, je ferai un résumé des étapes pour effectuer votre première contribution au projet Kubernetes mais je ne décrirai pas l'architecture et le code du projet. 
J'ai volontairement omis ou raccourci des passages afin d'avoir un article simple.  
Vous pourrez trouver une documentation du contributeur complète et bien plus vaste ici : [Kubernetes developer guide](https://github.com/kubernetes/community/tree/master/contributors/devel#readme)  

### Créer un compte Github  

Le projet Kubernetes se trouve sur Github (ainsi que tous les projets de sa fondation, la Cloud Native Computing Foundation, dit CNCF).   
Si vous n'avez pas de compte Github, il faut donc en créer un [ici](https://github.com).  

### S'inscrire à Linux foundation  

Lors de la première release de Kubernetes, son créateur, Google, a créé la [Cloud Native Computing Foundation](https://www.cncf.io)(CNCF) en partenariat avec la **Fondation Linux**.
Kubernetes y fut intégré en tant que premier projet.  
Nous avons donc Kubernetes faisant partie de la **CNCF**, qui elle-même fait partie de la **Linux foundation**.  

Pour contribuer sur le projet, il faut signer une licence, la **CNCF Individual Contributor License Agreement** de la Linux foundation.
Pour cela, suivez la procédure suivante : [The Contributor License Agreement](https://github.com/kubernetes/community/blob/master/CLA.md)  

### Forker le projet 

Cela consiste à faire une copie personnelle du projet sur laquelle vous pourrez créer vos propres branches, committer et pusher du code ainsi que créer des pull requests à destination du projet initial.  
À la différence d'un clone qui permettrait de récupérer le projet sur votre poste local, mais vous empêcherait de pusher des modifications sur celui-ci.  

Pour effectuer le fork :
- aller sur le projet : `https://github.com/kubernetes/kubernetes`  
- cliquer sur le bouton **Fork** en haut à droite de la page
- après quelques de secondes, le repository sera présent dans votre profil, exemple : `https://github.com/tlereste/kubernetes`  

### Cloner votre projet 

Ensuite, vous pourrez cloner votre projet précédemment forké, ce qui vous permettra d'être libre sur les modifications à y apporter.  

Vous pouvez cloner votre projet avec git avec la commande:  
```
git clone https://github.com/tlereste/kubernetes.git .
``` 

Personnellement, j'utilise l'IDE de Jetbrains [Intellij](https://www.jetbrains.com/fr-fr/idea/) et son interface pour cette action.  
Mais vous pouvez aussi utiliser un IDE plus adapté, [Goland](https://www.jetbrains.com/fr-fr/go/) (encore chez Jetbrains).  
  
  
## Tout est en place, par où commencer ?  

Voici quelques manières de contribuer au projet Kubernetes :   
- développement d'une évolution
- correction d'un bug
- création de tests unitaires
- création, mise à jour ou traduction de la documentation
- ...

Ce choix doit se faire en fonction de vos affinités, temps, compétences.

Pour commencer, il n'y a pas besoin de grosses contributions, "les petits ruisseaux font les grandes rivières". 
La communauté encourage même les petits commits et petites pull request : [Small is better](https://github.com/kubernetes/community/blob/master/contributors/guide/pull-requests.md#2-smaller-is-better-small-commits-small-pull-requests).

Certains, sur les nouveaux projets, font même la chasse aux **typos** (fautes d'orthographe) afin de devenir contributeur du projet !  

### Soumettre une nouvelle issue

Avant de créer une issue, pensez bien à vérifier qu'une issue similaire n'existe pas déjà en faisant une recherche avec les filtres.  

Puis :  
- dans l'onglet **Issue**, cliquer sur le bouton **New Issue**.  
- différents types d'issues seront proposés comme **Bug** ou **Enhancement**.  
- sélectionnez le type souhaité avec le bouton **Get Started**.  
- un template apparaitra permettant de créer l'issue. En fonction de son type, différentes informations seront demandées : 
description, version de Kubernetes utilisée... 
- vérifiez bien en bas du template les issues similaires pour éviter les doublons : **Similar to X existing issues**

Après sa création, l'issue sera catégorisée par [Special Interest Group](https://github.com/kubernetes/community/blob/master/sig-list.md) ou **SIG**, c'est-à-dire des groupes fonctionnels et/ou techniques avec des leaders, newsletters, channel slack et réunions propres.  

Quelques exemples de SIG :  
- sig cli : traite tout ce qui est lié au client kubectl et ses outils associés
- sig intrusmentation : couvre les meilleures pratiques pour l'observabilité des clusters
- sig release : assure la qualité des releases
- ...

### Contribuer à une issue existante

Vous avez trouvé une issue qui vous plait, pensez tout d'abord à vérifier qu'elle n'est assignée à personne et que personne ne travaille dessus.
Ensuite, assignez-vous cette issue avec le commentaire `/assign`.
  
  
## La contribution    

Voici quelques conseils et astuces à utiliser lors de votre contribution.  

### Le code

Kubernetes est développé en [Golang](https://golang.org) (Go).  
C'est aussi le cas pour la majorité des projets CNCF comme on peut le voir [ici](https://k8s.devstats.cncf.io/d/67/licenses-and-programming-languages).

Si vous n'êtes pas familier avec ce langage :
- le tutoriel [A Tour of Go](https://tour.golang.org) est disponible sur le site officiel  
- mais rien ne remplace un bon livre comme [Go In Action](https://www.manning.com/books/go-in-action) par exemple !

Lors du développement et avant d'effectuer votre PR, pensez à :  
- lancer les tests avec la commande : `go test` ou `make test`
- vérifier que le code est bien formaté avec l'outil [gofmt](https://golang.org/cmd/gofmt).
Ces étapes sont décrites dans [le guide du développement officiel](https://github.com/kubernetes/community/blob/master/contributors/devel/development.md).

### La communication

Il faut savoir que toutes vos interactions doivent se faire en anglais.
Que ce soit le code, les commentaires, les échanges... 
Attention aux tournures de phrase, syntaxe et orthographe, 
n'hésitez pas à abuser des outils de traductions en ligne notamment pour communiquer avec vos interlocuteurs 
([Linguee](https://www.linguee.fr) et [DeepL](https://www.deepl.com) par exemple).

Cela peut paraître bateau, mais il est important de respecter les mainteneurs du projet. 
Ce sont des personnes qui prennent de leur temps libre ou du temps alloué par leur société (Redhat, Google... ) pour maintenir le projet, 
il est donc très important d'être poli, précis et clair dans les échanges que vous aurez avec eux.  

### Git

Voici quelques commandes utiles pour la réalisation de votre PR.  

#### Configurer votre username et email
Il faut configurer les mêmes utilisées sur Github (et pour signer la CLA de la Linux foundation).  
```
git config --global user.name "tlereste"  
git config --global user.email lereste.thibault@gmail.com  
```

#### Maintenir votre fork à jour :
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

#### Squash des commits
Il est conseillé, et il vous sera probablement demandé de **squasher** vos **commits**.
Cela veut dire fusionner plusieurs commits en un seul afin de garder un historique git propre.  
Voici un très bon article indiquant comment effectuer cette action : [comment squasher ses commits](https://www.ekino.com/articles/comment-squasher-efficacement-ses-commits-avec-git).
 

## Et après la pull request ?

### CI / CD

Le processus d'intégration / déploiement continue (CI / CD) est effectué par [Prow](https://github.com/kubernetes/test-infra/blob/master/prow/README.md).
C'est un outil dédié et développé par le projet Kubernetes.  
Il fonctionne notamment en mode **ChatOps**. 
Cela signifie qu'en saisissant certains mots clés dans les commentaires, Prow déclenchera des actions qui sont décrite ici : [Commandes Prow](https://prow.k8s.io/command-help?repo=kubernetes%2Fkubernetes).  
Afin d'avoir un côté visuel à tout cela, un robot nommé [@k8s-ci-robot](https://github.com/k8s-ci-robot) fera le lien entre votre PR et Prow.
  
{{< image src="/images/contribution-open-source-kubernetes/prow-robot-kubernetes.png" title="Kubernetes prow robot" >}}
  
### Le traitement de la PR

Les membres du projet peuvent avoir les statuts suivants :  
- **members** qui n'ont pas de droits particuliers
- **reviewers** qui effectuent les revues de code
- **approvers** qui mergent le code (et peuvent aussi effectuer les revues de code)
  
La liste des reviewers et approvers est visible ici :  
- [OWNERS](https://github.com/kubernetes/kubernetes/blob/master/OWNERS) pour tous les projets
- [OWNERS_ALIASES](https://github.com/kubernetes/kubernetes/blob/master/OWNERS_ALIASES) pour les SIG
  
Lorsqu'une pull request est effectuée, elle sera automatiquement assignée à 2 **reviewers** et 1 **approver** les plus à même de la traiter.
Si vous souhaitez l'assigner à une personne en plus, vous pouvez saisir le commentaire `/assign @username`.
  
Un **reviewer** doit valider la PR avec le commentaire `/lgtm` qui signifie **look good too me**.
Ensuite, un **approver** merge la PR avec le commentaire `/approve`.

### Faire vivre la PR

Si votre PR est bloquée ou si vous avez besoin d'aide, vous pouvez :  
- dans Github, relancer une personne en spécifiant son username préfixé d'un @ afin qu'elle soit notifiée     
- il existe aussi une grande communauté sur le **Slack** officiel : https://kubernetes.slack.com. Contacter la personne directement ou demander de l'aide ou une relecture sur le channel correspondant.

Quelques exemples de channels utiles :  
- \#announcements : les annonces des projets CNCF, nouvelles versions, failles de sécurité, événements...
- \#fr-users : les utilisateurs français de Kubernetes
- \#kubernetes-docs-fr : les traducteurs de la doc Kubernetes en français
- \#kube-state-metrics : questions, pull requests, annonces liées au projet kube-state-metrics
- ...

Si vous avez des retours sur votre PR et si celle-ci donne lieu a de nouveaux commits, pensez bien à refaire les étapes mentionnées plus haut : 
squash des commits, relance des tests unitaires, vérification du formatage du code.


## Retour d'expérience

### Difficultés rencontrées

J'avais choisi de contribuer sur le repo principal du projet : [kubernetes/kubernetes](https://github.com/kubernetes/kubernetes).  
C'était une bonne expérience mais ce n'est pas ce que je conseillerais à quelqu'un qui souhaiterait effectuer sa première pull request.  

Ce repo est vertigineux, il contient de nombreuses issues, beaucoup de contributeurs et tout se passe très vite. Au moment où j'écris cet article, il y a :  
- 2003 issues ouvertes 
- 895 pull request en cours

C'est très difficile d'accéder à une nouvelle issue avant qu'une personne avec une plus grande connaissance ou plus expérimenté ne la prenne en charge.

De plus, dans mon cas, le processus de prise en charge et relecture de l'issue a été très long. Cela s'explique par le fait que les mainteneurs du projet étaient occupés à créer la release de la version 1.17 de Kubernetes et aussi au fait que mon issue concernait une fontionnalité non critique et non prioritaire.  

Pour information, ma [pull request](https://github.com/kubernetes/kubernetes/pull/82333) a été :
- créée le 4 septembre  
- relue le 7 janvier  
- mergée le 15 janvier  

Ce qui fait une durée totale de 4 mois. Soyez patient !

### Conseils  

#### Choix du repository

Pour débuter, et ça n'engage que moi, contribuez sur des repos plus petits de l'organisation Kubernetes plutôt que sur le principal.  
Après cette 1ère PR, j'ai choisi de contribuer sur ces autres projets :  
- kube-state-metrics : génére des métriques au format Prometheus de l'état des objets Kubernetes  
- krew et krew-index : gestionnaire de paquets pour les plugins de kubectl 

Pour Krew, j'ai par exemple modifié la documentation pour y ajouter [l'outil Popeye](https://thibault-lereste.fr/2020/04/kubernetes-popeye/).  

L'organisation Kubernetes comporte 69 repository, vous avez l'embarras du choix !
Par exemple :  
- ingress-nginx : le Nginx Ingress Controller
- kops : l'outil de provisionning de clusters
- dashboard : le tableau de bord (UI) de Kubernetes
- ...

Des projets plus petits seront plus faciles à appréhender, aussi bien au niveau de l'architecture, qu'au niveau fonctionnel. 
De plus, vous serez moins en concurence avec d'autres personnes, vous aurez plus de temps pour choisir une issue, des feedbacks plus rapides sur vos pull requests, 
bref que des avantages !  

#### Sélection de l'issue

Je vous conseille d'effectuer une recherche sur le label `good first issue`. 
Cela correspond à des issues assez simples taggées par les membres du projet.  
  
![kubernetes good first issue](images/contribution-open-source-kubernetes/good-first-issue-kubernetes.png)  
  
Il existe aussi un compte Twitter [goodfirstissue](https://twitter.com/goodfirstissue) qui tweet automatiquement les nouvelles `good first issue` de certains projets.

Si vous souhaitez simplement aider quelqu'un sur un problème ou une question, effectuez une recherche avec le label `help wanted`.  

## A vous !

J'espère que cet article vous a donné les bases pour commencer à contribuer et qu'il vous donnera du courage pour vous lancez ! :(fas fa-rocket):  