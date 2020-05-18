---
title: "Comment j'ai obtenu la certification Kubernetes CKAD"
date: 2020-05-18T16:00:00+01:00
draft: false
description: "Ma préparation pour réussir la certification Kubernetes CKAD"

tags: ["kubernetes", "ckad", "cncf", "certification"]

toc: true

featuredImage: "/images/certification-kubernetes-ckad/certification-kubernetes-ckad-featured.png"
images:
- "/images/certification-kubernetes-ckad/certification-kubernetes-ckad-twitter.png"
---

<!--more-->

## Pourquoi j'ai passé cette certif ?  

Après 2 ans de pratique de Kubernetes dans le cadre de mon travail et [avoir contribué à ce projet](https://thibault-lereste.fr/2020/04/contribution-open-source-kubernetes/),
j'ai décidé de passer les certifications [CKAD](https://www.cncf.io/certification/ckad/) et [CKA](https://www.cncf.io/certification/cka/) de la CNCF afin de valider mes compétences.

Cet article concerne uniquement la certification **CKAD**.  

Il existe beaucoup d'autres articles de blog traitant de ce sujet, mais ils sont principalement en anglais. J'ai donc choisi de rédiger cet article pour vous partager mon expérience, en français et sur la dernière version de la certification (avec Kubernetes 1.18).  

{{< image src="/images/certification-kubernetes-ckad/certificat-ckad-thibault-lereste.png" title="Certificat CKAD Thibault Le Reste" >}}


## Description de l'examen

### Détails pratiques

Depuis le 9 janvier 2020, cette certification [est valable 3 ans](https://www.cncf.io/blog/2020/01/09/certified-kubernetes-application-developer-ckad-certification-is-now-valid-for-3-years) au lieu de 2 ans auparavant.   
Après s'y être inscrit, vous avez 1 an pour choisir une date de passage.  
Si vous échouez, **vous aurez le droit à un nouvel essai** sans repayer l'inscription.  
Le tarif à l'inscription est de **300$**. Cependant, il y a souvent des réductions disponibles, pour ma part j'ai eu 30% de réduction.   

Il faut au maximum 36 heures pour obtenir les résultats de l'examen.     
De mon côté, je les ai obtenu un peu avant, mais tout de même au bout de 33 heures.  

### Aspect technique

Depuis le 23 avril 2020, l'examen se déroule avec la [version 1.18 de Kubernetes](https://github.com/cncf/curriculum/blob/master/CKAD_Curriculum_V1.18.pdf). 
Cela a quelques impacts au niveau des commandes à utiliser que je décrirai plus tard.  

Côté système d'exploitation, c'est **Ubuntu 16 (Xenial)** qui est utilisé.

### Contenu 

L'examen dure **2 heures** et comporte **19 questions** qui sont pondérées par un pourcentage. 
Il faut obtenir au minimum le **score de 66%** pour obtenir la certification.  

Voici les domaines traités durant l'examen :  
- Core Concepts (13%)
- Configuration (18%)
- Multi-Container Pods (10%)
- Observability (18%)
- Pod Design (20%)
- Services & Networking (13%)
- State Persistence (8%)

Par exemple : 

Core Concepts (13%)  
- Understand API Primitives
- Create and configure basic pods

Le temps étant compté, il faudra donc bien choisir par quelles questions commencer, en fonction de leur pourcentage et complexité. 
Vous pouvez, par exemple, répondre aux questions dans le désordre ou revenir sur une question que vous avez laissée de côté.

Lors de l'examen, vous aurez le droit à deux onglets sur votre navigateur :
 - Un onglet pour les questions / terminal
 - Un autre onglet pour la [documentation officielle de Kubernetes](https://kubernetes.io/docs/home/)
 
Il est donc nécessaire de bien connaitre cette documentation et d'utiliser au maximum les commandes impératives avec le client `kubectl`.  
Un bloc-note est aussi disponible, utilisez-le à bon escient pour noter les questions que vous avez réussies, esquivées, 
celles pour lesquelles vous êtes bloquées ainsi que le pourcentage des questions associé. 

La durée limitée de l'examen vous obligera à maitriser toutes vos actions sur le bout des doigts, 
c'est pourquoi vous trouverez plus tard une partie "Conseils et astuces" pour vous faire gagner le maximum de temps.

## Inscription

Il faut se rendre sur le site de la [Linux foundation](https://training.linuxfoundation.org/certification/certified-kubernetes-application-developer-ckad/).  

Après l'inscription, vous aurez une check-list à parcourir avec notamment : 
- **Check System Requirements :** lance une liste de vérification, indiquant si votre configuration système, navigateur, webcam... 
est compatible pour l'examen. A savoir qu'il est nécessaire d'installer un plugin sur votre navigateur afin de partager votre écran. 
De plus, il est indiqué une résolution d'écran minimale de 1280 x 800 mais la mienne de 1366 x 768 ne m'a pas posé problème.

- **Schedule Exam :** permet de planifier la date et heure de passage de son examen. 
Dans mon cas, beaucoup de créneaux étaient disponibles, j'ai pu planifier une date 2 jours avant.  

{{< admonition info "Info" >}}
J'ai par contre eu un léger problème pour choisir l'horaire de passage, au moment de sélectionner une timezone UTC.
En choisissant Paris, le site m'indiquait une timezone UTC+1. 
Cette timezone aurait du être UTC+2, car nous étions en heure d'été. 
En réalité, l'heure UTC+2 été bien prise en compte, mais l'affichage était incorrect.
{{< /admonition >}}

- **Get Candidate Handbook :** document qui référence toutes les informations pratiques de la certification. 
Notamment avoir une pièce d'identité non périmée.  

{{< admonition info "Info" >}}
Ma carte identité datait de plus de 10 ans, mais la [dérogation de validité de 15 ans](https://www.interieur.gouv.fr/Actualites/L-actu-du-Ministere/Duree-de-validite-de-la-CNI) a bien été prise en compte.
{{< /admonition >}}

## Configuration de l'environnement 

Au début, de l'examen, vous devrez prendre quelques petites minutes pour configurer votre environnement.  

### Éditeur de texte et configuration

J'ai utilisé l'éditeur **Vim** étant plus à l'aide avec celui-ci. 
Il est bien sûr possible d'utiliser d'autres éditeurs comme Nano.  

Avant d'utiliser Vim, il faut le paramétrer afin d'éditer au mieux les fichiers YAML.

On édite le fichier vimrc :  
 ```
vi ~/.vimrc  
```

Et on y ajoute la ligne suivante :  
```
set ts=2 sts=2 sw=2 et 
```

On applique ensuite la configuration :  
```
. ~/.vimrc
```

Explication des paramètres : 
- `set ts=2` : ts signifie tabstop : Fixe la largeur affichée d'une tabulation à 2 espaces
- `set sts` : sts signifie softtabstop : Insère ou supprime 2 espaces avec la touche tabulation ou retour arrière
- `set sw=2` : sw signifie shiftwidth :  Nombre d'espaces utilisés lors de l'indentation > ou < 
- `set et` : et signifie expandtab : En mode insertion : Remplace les tabulations par des espaces

Il existe différents modes d'édition dans Vim, voici les 3 principaux :  
- Mode normal : c'est le mode par défaut.
- Mode insertion : on y entre avec la touche `i` et le quitte avec la touche `ESC`. Ce mode permet de saisir du texte.  
- Mode ligne de commande : il faut être en mode interactif et taper la touche `:`. Ce mode permet d'exécuter des commandes.

Voici les principales commandes que j'utilise qui vous seront utiles. 
Ces commandes se font en mode interactif :  

| Action                             | Commande                     |
| -----------------------------------|------------------------------|
| Rechercher un mot                  | /mot puis n                  |
| Aller au début d'une ligne         | 0                            |
| Aller à la fin d'une ligne         | $                            |
| Insérer du texte après le curseur  | a                            |
| Remplacer un mot                   | cw                           |
| Supprimer une ligne                | dd ou d (nombre de lignes) d |
| Copier une ligne                   | yy ou y (nombre de lignes) y |
| Coller du texte                    | p                            |
| Remplacer un mot                   | cw                           |
| Remplacer un caractère             | r                            |
| Supprimer un caractère             | x                            |
| Indenter du texte                  | > à droite ou < à gauche     |
| Sélectionner du texte              | v (sélection) v              |
| Annuler la dernière commande       | u                            |
| Enregistrer et quitter             | :wq!                         |

Pour un aperçu global des commandes, vous pouvez prendre connaissance du [vim cheatsheet](https://devhints.io/vim).

Pour la mise en pratique, il existe ce [tutoriel interactif](https://www.openvim.com/tutorial.html) !

### Alias et autocomplétion pour Kubectl

Je vous conseille de créer un alias pour le client **Kubectl** et activer l'autocomplétion [comme décrit dans la documentation officielle](https://kubernetes.io/docs/tasks/tools/install-kubectl/#enable-kubectl-autocompletion).

Création d'un alias pour Kubectl :  
```
echo 'alias k=kubectl' >>~/.bashrc
```

Activation de l'autocomplétion sur cet alias :  
```
echo 'complete -F __start_kubectl k' >>~/.bashrc
```

Vous pouvez aussi créer d'autres alias, comme :  
`kgp` pour `kubect get pods`  
`kgd` pour `kubectl get deploiement`  
...

## Conseils et astuces

### Changement de contexte et namespace

Il vous sera demandé à chaque question de changer de contexte, pour changer de noeud. 
Pas de panique, la commande permettant de faire cela est affichée au début de chaque question :  
```
kubectl config use-context <context>
```

Chaque question se déroule dans un namespace particulier.  
Afin d'éviter d'utiliser le paramètre `-n <namespace>` lors de chaque commande, 
je vous conseille de changer le namespace courant avec la commande :  
```
kubectl config set-context --current --namespace <namespace>
```

### Création des ressources

Afin de gagner du temps, utilisez les alias abrégés des ressources, par exemple :
```
kubectl get ns
```
plutôt que :  
```
kubectl get namespaces
```

La liste des alias abrégés est disponible avec :  
```
kubectl api-resources
```

Dans le cadre de cette certification, voici les principaux noms abrégés que j'utilise :  

| nom                                | nom abrégé                   |
| -----------------------------------|------------------------------|
| configmaps                         | cm                           |
| cronjobs                           | cj                           |
| deployment                         | deploy                       |
| namespaces                         | ns                           |
| persistentvolumeclaims             | pvc                          |
| persistentvolumes                  | pv                           |
| pods                               | po                           |
| services                           | svc                          |

Depuis le **23 avril 2020**, l'examen se déroule sur la version de **Kubernetes 1.18**. 
Voici une liste des principales commandes qui ont évolué :  

| Action                             | Commande k8s 1.18                                                  | Commande k8s 1.17                                       |
| -----------------------------------|--------------------------------------------------------------------|---------------------------------------------------------|
| Créer un pod                       | ```kubectl run sample-pod```                                       | ```kubectl run sample-pod --restart=Never```            |
| Créer un deployment                | ```kubectl create deploy sample-deploy```                          | ```kubectl run sample-deploy```                         |
| Créer un job                       | ```kubectl create job sample-job```                                | ```kubectl run sample-job --restart=OnFailure```        |
| Créer un cronjob                   | ```kubectl create cronjob sample-cronjob --schedule="* * * * *"``` | ```kubectl run sample-cronjob --schedule="* * * * *"``` |


Plutôt que de créer les ressources directement, 
il est préférable de générer le template et de l'exporter dans un fichier YAML. 
Cela a plusieurs avantages : 
- Si l'on nomme le template avec le nom de la question, exemple 08-pod.yaml, 
on peut revenir plus tard dessus si on laisse la question de côté.
- On peut éditer les templates facilement avant de créer la ressource.
- On peut dupliquer et réutiliser les templates entre les questions.

Pour exporter le template au format YAML sans créer la ressource, il faut utiliser les paramètres suivants :  
```
--dry-run -o yaml > fichier.yaml  
```

Attention, la commande précédente [est dépréciée](https://kubernetes.io/docs/setup/release/notes/#kubectl-1), mais elle fonctionne toujours avec la version Kubernetes 1.18 (celle de l'examen).  
Cependant, un message de warning apparaîtra lors de son exécution. Vous pouvez l'ignorer ou utiliser la "nouvelle commande" :  
```
--dry-run=client -o yaml > fichier.yaml  
```

Exemple :  
```
kubectl create deploy --image=nginx --dry-run -o yaml > deploy-template.yaml
kubectl create -f deploy-template.yaml
```

### Suppression rapide d'une ressource

Lors de la suppression d'un pod ou deployement, 
vous pouvez utiliser les paramètres suivants afin d'avoir une suppression instantanée :  
```
--force --gracefull=0  
```

Exemple : 
```
kubectl delete pod sample-pod --force --gracefull=0  
```

### Utilisation des templates de la documentation

Il est parfois nécessaire d'utiliser les templates d'exemples de la documentation Kubernetes.  
Par exemple, les persistents volumes ne peuvent pas être créés directement avec le client Kubectl.
Pour simplifier cette création, vous pouvez copier l'url du template et lancer la commande suivante :  
```
wget -O- <url> > fichier.yaml  
```

Exemple :  
```
wget -O- https://raw.githubusercontent.com/kubernetes/website/master/content/en/examples/pods/storage/pv-volume.yaml > pv-volume-template.yaml
```

### Utilisation d'explain pour afficher les champs disponibles 

Afin de connaitre les champs à utiliser dans le template d'une ressource,
je vous conseille d'utiliser la commande `kubectl explain` par itérations.  

Exemple pour un job, on commence par :  
```
kubectl explain job
```

Qui affiche :  
```
apiVersion   <string>
kind <string>
metadata     <Object>
spec <Object>
status       <Object>
```

On continue, en sélectionnant le champ `spec` avec :  
```
kubectl explain job.spec
```

Qui affiche :  
```
activeDeadlineSeconds        <integer>
backoffLimit <integer>
completions  <integer>
manualSelector       <boolean>
parallelism  <integer>
selector     <Object>
template     <Object> -required-
ttlSecondsAfterFinished      <integer>
```

Finalement, cela permet de savoir, par exemple, 
qu'on peut utiliser le champ `parallelism` pour lancer des jobs en parallèle.

Exemple :  
```
apiVersion: batch/v1
    kind: Job
    metadata:
      name: sample-job
    spec:
      parallelism: 2
```

Pour afficher tous les champs directement, on peut utiliser aussi la commande :  
```
--recursive
```

Exemple :  
```
kubectl explain job --recursive
```

### Recherche dans les logs et évènements 

Pour rechercher rapidement dans les logs ou évènements,
je vous conseille d'utiliser la commande `grep` avec les paramètres suivants :
- `i` : pour ignorer la casse
- `A` suivi d'un nombre : pour afficher les <nombre> lignes qui suivent le mot recherché

Par exemple, pour rechercher les 3 annotations d'un pod :
```
kubectl describe pod sample-pod | grep -iA 3 'annotations'
```

### Fréquence des cronjobs

La fréquence des cronjobs est définie au format cron.  

Par exemple :  
`* * * * *` correspond à toutes les minutes  
`0 */2 * * *` correspond à toutes les 2 heures  

{{< admonition tip "Conseil" >}}
Si vous ne connaissez pas ou ne maitrisez pas le format cron, 
le site [crontab.guru](https://crontab.guru) vous sera utile.
{{< /admonition >}}
   
### Format des requests et limits

Concernant les requests et limits d'un container : 
- Pour le CPU, elles sont indiquées en millicpus (ou millicores). Un CPU équivaut à 1000 millicores. Exemple: `500m`
- Pour la mémoire, elles sont indiquées en mebibytes. Exemple : `128MiB` 

{{< admonition warning "Attention" >}}
Pour la mémoire, il ne faut pas confondre **MiB** avec **Mb** ou **Mo**
{{< /admonition >}}

## Se préparer et s'entrainer

### Cluster Kubernetes  

Pour vous exercer, il faut faudra un cluster Kubernetes. Différentes solutions s'offrent à vous :  

#### Les géants du cloud

- [Google cloud GKE](https://cloud.google.com/kubernetes-engine) :  
Crédit gratuit de 300 dollars valable pendant 12 mois. 
De mon côté, un cluster d'un noeud n1-standard-1 me coûte 30 dollars / mois.
- [Amazon AWS EKS](https://aws.amazon.com/eks) :  
L'offre gratuite d'AWS n'inclut pas EKS.
- [Microsoft Azure AKS](https://azure.microsoft.com/services/kubernetes-service) :  
Crédit gratuit de 170 euros valable pendant 30 jours.  

#### Les cloud providers "made in France"

- [OVH Cloud Managed Kubernetes Service](https://www.ovhcloud.com/fr/public-cloud/kubernetes/) : 
Cette solution est assez récente (un peu plus d'un an) et a un coût inférieur aux "géants du cloud". Crédit gratuit de 30 euros.
- [Scaleway Kubernetes Kapsule](https://www.scaleway.com/fr/kubernetes-kapsule/) :  
Cette solution, depuis récemment en version finale (moins de 2 mois), est la moins chère des offres que j'ai listées.

#### Le cluster local

Pour monter facilement un cluster en local, je vous conseille le combo **K3S / K3D**.
- [K3S](https://k3s.io) est une version allégée de Kubernetes et est développé par Rancher.
- [K3D](http://k3d.io) est un outil permettant de lancer K3S dans un container Docker : il s'agit d'un projet forké et maintenu par Rancher.

Vous pouvez aussi utiliser [Minikube](https://kubernetes.io/docs/setup/learning-environment/minikube) pour déployer un cluster à un noeud unique.

### Livres

Pour avoir une vision d'ensemble du système Kubernetes, je vous conseille la lecture de deux livres très complets :    

- [Kubernetes in Action](https://www.manning.com/books/kubernetes-in-action) 
écrit par Marko Luksa aux éditions Manning.  
La [deuxième édition](https://www.manning.com/books/kubernetes-in-action-second-edition) est en cours de rédaction.  

{{< image src="/images/certification-kubernetes-ckad/kubernetes-in-action.png" title="Kubernetes in action" >}}

- [Kubernetes Up and Running](https://www.oreilly.com/library/view/kubernetes-up-and/9781491935668) 
écrit par Kelsey Hightower, Brendan Burns et Joe Beda aux éditions Oreilly.  

{{< image src="/images/certification-kubernetes-ckad/kubernetes-up-and-running.png" title="Kubernetes up and running" >}}

### Exercices gratuits

Pour se faire la main, voici une liste de quelques exercices gratuits que j'ai utilisé.

- **"CKAD exercises" de Dimitris-Ilias Gkanatsios :**  
Les exercices incontournables recommandés par tous. Ils couvrent la majorité de l'examen.
Vous devez être capables de les faire sans réfléchir : 
https://github.com/dgkanatsios/CKAD-exercises  

- **"Kubernetes CKAD weekly challenges" :**  
Une liste de 13 "challenges" plus complets :  
https://codeburst.io/kubernetes-ckad-weekly-challenges-overview-and-tips-7282b36a2681  

- **"CKAD practice exam" de Matthew Palmer :**  
Un avant-goût de 5 questions d'un examen blanc payant :  
https://matthewpalmer.net/kubernetes-app-developer/articles/ckad-practice-exam.html  

### Formation et exercices payants

Je me suis exercé sur des examens blanc payant et c'est vraiment quelque chose que je conseille. 
Pour 20 à 30 euros, on peut avoir accès à des exercices de qualité, soit à peine 10% du coût de la certification.  

En voici quelques-un :  

- **[Killer.sh](https://killer.sh/ckad)** :  
C'est le simulateur d'examen que j'ai utilisé.
Il y a 20 questions / problèmes et 2 heures pour les résoudre. 
Ce simulateur ressemble beaucoup à l'examen réel et est parfait pour s'entraîner.  
De plus, le cluster fourni est disponible durant 3 jours ce qui vous laisse le temps de faire et refaire les exercices.  
Le tarif est de 29.99 euros mais vous avez une réduction de 20% à l'inscription.  

- **[Kodekloud](https://kodekloud.com/courses/kubernetes-certification-course/lectures/6731363)** :  
C'est une formation vidéo avec des 2 examens de tests. 
Je ne connais pas le contenu de la formation, mais j'ai eu l'occasion de faire les tests et ils sont très pertinents. 
Un abonnement au mois ou à l'année est disponible pour bénéficier de toutes les formations du site. 

- **[Linux academy](https://linuxacademy.com/course/certified-kubernetes-application-developer-ckad/)** :  
Cette formation est unanimement conseillée. Elle contient 3 examens de tests. Je n'ai pas eu l'occasion de la tester.
Il est possible de s'abonner au mois ou à l'année afin de bénéficier des formations de la Linux academy.

### Communauté CKAD

De [nombreux articles de blog](https://lmgtfy.com/?q=ckad+exam+blog) sont disponibles 
principalement en anglais avec des retours d'expérience et conseils pour passer la certification.  

Pour poser des questions, ou être tenu informé des derniers articles de la communauté, 
il existe un [Slack officiel](https://slack.k8s.io) channel #ckad-exam-prep .

## Le jour de l'examen 

Voici les choses à savoir :  
- Il est possible de démarrer l'examen à partir de 15 min avant l'horaire prévu et jusqu'à 15 min après.  
- Il faut préparer sa pièce d'identité, avoir un bureau vide, 
vous aurez juste le droit d'avoir une bouteille d'eau sans étiquette/inscription et un verre d'eau.  
- La pièce doit être fermée et vous devez être tout seul (les chats sont autorisés :(fas fa-cat):) 
- Il ne faut pas masquer sa bouche, ni parler à voix haute.
- La communication avec l'examinateur se fait en anglais, entièrement par chat.
- L'examinateur vous demandera de montrer la pièce dans laquelle vous vous trouvez avec la webcam. 
- Un récapitulatif de tout ce que vous devez savoir sera affiché dans le terminal. 
Par exemple, il faut savoir que lors de l'examen, sur Windows il faut utiliser ctrl+insert pour copier et shift+insert (ou clic droit coller) pour coller. 
- Le temps restant n'est pas affiché précisément. 
Il apparaît sous la forme d'une barre de progression qui décroît et change de couleur : verte puis orange et enfin rouge. 
L'examinateur vous indiquera dans le chat quand il vous restera 1 h, 30 min et 10 min.

## Conclusion

Vous l'aurez compris, le meilleur moyen de se préparer est de refaire encore et encore les exercices 
afin de pouvoir les réussir les yeux fermés ! 
Ne pas céder au stress et bien choisir les questions en fonction du pourcentage / complexité.

Bon courage si vous souhaitez le passer, je me prépare déjà pour l'étape suivante, la [certification CKA](https://www.cncf.io/certification/cka/) !

N'hésitez pas à partager vos trucs et astuces, ou à échanger avec moi sur Twitter [@thibaultlereste](https://twitter.com/thibaultlereste) !