---
title: "Désinfecter votre cluster Kubernetes avec Popeye !"
date: 2020-04-07T14:00:00+01:00
draft: false
description: "Popeye est un outil permettant de diagnostiquer rapidement des cluster Kubernetes"

tags: ["kubernetes", "tool"]

toc: true

featuredImage: "/images/kubernetes-popeye/kubernetes-popeye-featured.png"
images:
- "/images/kubernetes-popeye/kubernetes-popeye-featured.png"
---

## Présentation de l'outil

En cherchant un outil me permettant de diagnostiquer rapidement un de mes cluster Kubernetes, je suis tombé, un peu par hasard, sur Popeye !  

[Popeye](https://popeyecli.io) est un outil qui analyse un cluster Kubernetes et qui en remonte les problèmes potentiels de ressources et configurations.
Il peut aussi alerter sur la sous-capacité CPU et mémoire du cluster en s'appuyant sur le serveur de métriques déployé sur celui-ci.
Pour information, cet outil communique avec le cluster uniquement en lecture seule, il n'y a donc pas de risques à l'utiliser.

Popeye est open source et a été créé par [Fernand Galiana](https://github.com/derailed) qui aussi à l'initiative du client de gestion de cluster Kubernetes [K9S](https://k9scli.io) (que j'évoquerai dans un futur article).

Actuellement, il est compatible avec les versions de Kubernetes 1.13 et +.

## Et on l'installe comment ?

Il y a plusieurs manières d'installer / déployer Popeye :
- En clonant le repository git et en lançant la commande `go install`
- En déployant un **CronJob** sur le cluster Kubernetes à l'aide d'un `kubectl apply` (Attention de bien appliquer les **RBAC** afin de donner à Popeye les droits en lecture sur les ressources Kubernetes)
- En l'installant sous forme de plugin kubectl avec **Krew**

C'est cette dernière solution que j'ai choisie et que je vais décrire pour sa simplicité et rapidité d'utilisation.

## Krew : à quoi ça sert ?

[Krew](https://github.com/kubernetes-sigs/krew) est un gestionnaire de paquets pour les plugins de kubectl.  
Il permet de simplifier la gestion de plugins kubectl en permettant leur recherche et installation.
Actuellement, il y a plus de 80 plugins kubectl accessibles via Krew.

Par chance Popeye est [depuis peu](https://github.com/kubernetes-sigs/krew-index/pull/521) disponible comme plugin de kubectl !

## Installation de Krew

J'ai installé Krew sur une distribution Debian pour les autres OS, la procédure est [ici](https://krew.sigs.k8s.io/docs/user-guide/setup/install/).

Prérequis : git doit être installé

Lancer cette commande pour installer la dernière version de Krew :
```
(
  set -x; cd "$(mktemp -d)" &&
  curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/krew.{tar.gz,yaml}" &&
  tar zxvf krew.tar.gz &&
  KREW=./krew-"$(uname | tr '[:upper:]' '[:lower:]')_amd64" &&
  "$KREW" install --manifest=krew.yaml --archive=krew.tar.gz &&
  "$KREW" update
)
```

Ajouter `$HOME/.krew/bin directory` à votre variable d'environnement PATH.   
Pour cela, mettez à jour votre fichier `.bashrc` et ajoutez-y la ligne suivante :  
`export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"`  
puis redémarrez votre shell.

Lancer la commande `kubectl krew version` afin de vérifier l'installation.


## Installation du plugin kubectl Popeye

La première étape consiste à mettre à jour la liste des plugins en local :  
```
kubectl krew update
```

Ensuite, installer le plugin Popeye :  
```
kubectl krew install popeye
```

Puis, lancer la commande `kubectl popeye version` pour vérifier l'installation.

## Utilisation de l'outil Popeye  

Lancer la commande suivante :
```
kubectl popeye help
```

De nombreuses options sont disponibles, je vais ici vous en décrire quelques unes.
```
Usage:
  popeye [flags]
  popeye [command]

Available Commands:
  help        Help about any command
  version     Prints version/build info

Flags:
  -A, --all-namespaces                 Sanitize all namespaces
      --as string                      Username to impersonate for the operation
      --as-group stringArray           Group to impersonate for the operation
      --certificate-authority string   Path to a cert file for the certificate authority
  -c, --clear                          Clears the screen before a run
      --client-certificate string      Path to a client certificate file for TLS
      --client-key string              Path to a client key file for TLS
      --cluster string                 The name of the kubeconfig cluster to use
      --cluster-name string            Specificy a cluster name when running popeye in cluster
      --context string                 The name of the kubeconfig context to use
  -f, --file string                    Use a spinach YAML configuration file
  -h, --help                           help for popeye
      --insecure-skip-tls-verify       If true, the server's caCertFile will not be checked for validity
      --kubeconfig string              Path to the kubeconfig file to use for CLI requests
  -l, --lint string                    Specify a lint level (ok, info, warn, error) (default "ok")
  -n, --namespace string               If present, the namespace scope for this CLI request
  -o, --out string                     Specify the output type (standard, jurassic, yaml, json, html, junit, prometheus, score) (default "standard")
      --over-allocs                    Check for cpu/memory over allocations
      --pushgateway-address string     Address of pushgateway e.g. http://localhost:9091
      --request-timeout string         The length of time to wait before giving up on a single server request
      --s3-bucket string               Specify to which S3 bucket you want to save the output file
      --save                           Specify if you want Popeye to persist the output to a file
  -s, --sections strings               Specifies which resources to include in the scan ie -s po,svc
      --token string                   Bearer token for authentication to the API server
      --user string                    The name of the kubeconfig user to use
```

La commande la plus simple est :
```
kubectl popeye
```

Elle permet de lancer un scan complet de votre cluster en utilisant la configuration `kubeconfig.yml` définie dans la variable d'environnement `KUBECONFIG`.   
Plus simplement, cette commande lance un scan sur votre cluster actif.  

Le résultat du scan sera directement affiché dans votre terminal.  
La majorité des ressources du cluster est analysée : roles, configmap, deployement, pods, services...  
Au final, un nombre de points et une note sont donnés à votre cluster : la meilleure note étant A, et la moins bonne note F. Les points vont également de 0 (moins bon score) à 100 (meilleur score).

Voici 2 exemples ("bon" cluster et "mauvais" cluster) tirés de la documentation officielle de l'outil. Je n'utilise pas ici mes propres résultats pour des questions de confidentialité.  
La dernière version de Popeye remonte plus d'informations sur plus de resources que ces exemples.  
 
### Cluster avec un score D

![cluster score d](images/kubernetes-popeye/d_score.png)

Ici, des recommandations sont remontées concernant les **Pods** :  
- pas de **resource limits** définies
- pas de **probes** définis
- utilisation d'une image taggée **latest**  
- ...

{{< admonition tip "Conseil" >}}
L'utilisation d'une image taggée **latest** est un [anti-pattern](https://vsupalov.com/docker-latest-tag/).
{{< /admonition >}}

### Cluster avec un score A

![cluster score a](images/kubernetes-popeye/a_score.png)
 
  
Voici quelques options à passer à votre commande `kubectl popeye` :
- `--kubeconfig` pour spécifier un autre fichier de configuration kubeconfig  
 - `-n` pour spéficier le namespace sur lequel effectuer le scan  
 - `-l` le niveau de scan effectué : ok, info, warn, error ("ok" par défaut)  
 - `-o` le mode d'affichage des résultats (standard, jurassic, yaml, json, html, junit, prometheus, score) ("standard" par défaut)  
 - ...  
 
## Pour aller plus loin...

Si vous avez plus de temps et d'envie, voici quelques cas d'utilisation plus poussés de l'outil :  
- Sauvegarde des résultats dans un stockage **S3 AWS** (paramètre `s3-bucket`)  
- Utilisation d'un fichier de configuration `spinach.yml` afin de paramètrer le scan : paramètrage des cpu et mémoire alloués, exclusion de règles et/ou ressources...
- Lancer les scans via un **CronJob**  
- Export des résultats dans [Prometheus](https://prometheus.io/) en combinant les 2 paramètres suivants : `-o prometheus` et `--pushgateway-address`  

## Les problèmes rencontrés
 
De mon côté, les couleurs ne s'affichaient pas dans le terminal.  
Afin de corriger ce souci, j'ai soumis une [pull request](https://github.com/derailed/popeye/pull/89) qui résoud désormais ce problème.  

Si les emojis reste en noir et blanc, vous pouvez installer la police [Noto Color Emoji](https://www.google.com/get/noto/help/install). 

## Convaincu ?

Pour résumer, Popeye est un outil sans prétention, simple d'utilisation et qui donne rapidement un aperçu de l'état d'un cluster Kubernetes.  
Pour ma part, je l'utilise à la demande et il me donne entièrement satisfaction !  

C'est un outil open source, n'hésitez donc pas à collaborer [ici](https://github.com/derailed/popeye).

Et vous, l'utilisez vous ? L'avez-vous testé ? Qu'en pensez-vous ?  