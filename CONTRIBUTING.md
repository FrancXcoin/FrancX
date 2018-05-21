Contribuer à FRAX Core
============================

Le projet FRAX Core exploite un modèle de contributeur ouvert où tout le monde est
bienvenue à contribuer au développement sous la forme d'examen par les pairs, de tests
et de correctifs. Ce document explique le processus pratique et les directives pour les
contribuants.

Premièrement, en termes de structure, il n'y a pas de concept particulier de "Core 
développeurs "dans le sens de personnes privilégiées. L'Open source offre 
naturellement un système de méritocratie où, les contributeurs les plus actifs 
gagnent la confiance de la part de la communauté des développeurs. Cependant, une certaine 
hiérarchie est nécessaire. En tant que tel, il y a des "responsables" du référentiel 
qui sont responsables de fusionner les demandes d'extraction ainsi qu'un «responsable 
principal» qui s'occupe du cycle de publication, fusion globale et de la modération 
et nomination des responsables.

Flux de travail du contributeur
--------------------

La base de code est maintenue en utilisant le "workflow du contributeur" et où tout le monde
sans exception apporte des propositions de patch en utilisant "pull requests". Ceci
facilite la contribution sociale, les tests faciles et l'évaluation par les pairs.

Pour contribuer aux patchs, le flux de travail est le suivant:

  - Dépôt sur un Fork
  - Création d'un branche du sujet
  - Application des correctifs

Les conventions de codage du projet dans les [notes développeur] (doc/developer-notes.md)
doivent être respectées.

En général [les commits seront sur atomic](https://en.wikipedia.org/wiki/Atomic_commit#Atomic_commit_convention)
et les diffs seront facile à lire. Pour cette raison, ne mélangez aucun formatage
corrigé ou changement de code avec les changements réels.

Les messages de validation doivent être verbeux par défaut et comporter une courte 
ligne d'objet(50 caractères maximum), une ligne blanche et un texte explicatif détaillé
paragraphe (s), à moins que le titre ne soit explicite (comme "Typo corrigé
dans init.cpp ") auquel cas une seule ligne de titre est suffisante. Les messages 
de validation doivent êtreutile aux personnes lisant votre code à l'avenir, alors 
expliquez le raisonnement de vos décisions. 
Plus d'explications [ici] (http://chris.beams.io/posts/git-commit/).

Si un commit particulier fait référence à un autre problème, veuillez ajouter la référence, par
exemple `refs #1234`, ou` corrections #4321`. Utiliser les mots clés `résolus` ou` clos`
provoquera la fermeture du problème et la requête de fusion.

Veuillez vous référer au [Manuel Git] (https://git-scm.com/doc) pour plus d'informations
à propos de Git.

  - Dépose des commits sur un fork
  - Créer une requête de fusion

Le titre de la requête doit être préfixé par le composant ou la zone que
la demande de fusion affecte. Zones valides :

  - *Consensus* pour les modifications du code critique consensuel
  - *Docs* pour modifier la documentation
  - *Qt* pour modifier frax-qt
  - *Minting* pour modifier le code du minting
  - *Net* ou *P2P* pour les modifications du code de réseau pair-à-pair
  - *RPC/REST* pour les modifications des API RPC ou REST
  - *Scripts et outils* pour les modifications des scripts et des outils
  - *Tests* pour les modifications apportées aux tests unitaires frax ou aux tests QA
  - *Trivial*  devrait **seulement** être utilisé pour les PR qui ne changent pas le code 
    executablex.néré. Notamment, les refacteurs (changement d'arguments de fonction et code
    réorganisation) et les changements de comportement ne devraient pas être marqués comme insignifiants.
    Des exemples de PR banales sont des changements comme :
    - commentaires
    - les espaces
    - noms de variables
    - consignation et messages
  - *Utils et bibliothèques * pour les modifications apportées aux utilitaires et aux bibliothèques
  - *Wallet* pour les modifications du code du portefeuille

Exemples:

    Consensus: Ajouter un nouvel opcode pour BIP-XXXX OP_CHECKAWESOMESIG
    Net: créer automatiquement un service caché en passant par Tor
    Qt: Ajouter un bouton d'alimentation
    Trivial: Correction d'une faute de frappe dans init.cpp

Si une demande d'extraction ne doit pas être considérée pour fusionner (pour l'instant)
préfixez le titre avec [WIP] ou utilisez [Liste des tâches](https://help.github.com/articles/basic-writing-and-formatting-syntax/#task-lists) dans le corps de la requête de tirage pour 
indiquer que des tâches sont en attente.

Le corps de la demande d'extraction doit contenir suffisamment de description 
de ce que le patch fait avec toute justification / raisonnement. Vous devriez 
inclure des références à des discussions (par exemple d'autres billets ou une 
liste de discussion).

À ce stade, il faut s'attendre à des commentaires et à des retours d'autres 
contributeurs. Vous pouvez ajouter plus de commits à votre demande d'extraction 
en les ex.geant localement et en les déposants sur votre fork jusqu'à ce que vous 
ayez satisfait tous les commentaires.

Ecrasement des correctifs
---------------------------
Si votre demande d'extraction est acceptée pour la fusion, un mainteneur peut vous 
demander d'écraser et ou [rebaser] (https://git-scm.com/docs/git-rebase) vos corrections
avant qu'elles ne soit fusionné. 
Le flux de travail d'écrasement de base est illustré ci-dessous.

    git checkout votre_id_branche
    git rebase -i TITRE~n
    # n est le nombre de correctifs dans la requête
    # définir les commits depuis 'pick' à 'squash', sauvegardez et quittez
    # sur l'écran suivant, éditez/affinez les messages de commits
    # sauvegardez et quittez
    git push -f # (force la requête sur GitHub)

Si vous avez des problèmes avec l'écrasement (ou d'autres workflows avec `git`), 
vous pouvez alternativement activer "Autoriser les modifications des responsables" 
dans le bon GitHub, barre latérale et demander de l'aide dans la demande d'extraction.

Veuillez ne pas créer plusieurs demandes d'extraction pour le même commit.
Utilisez la requête de tirage déjà ouverte (ou créée précédemment) pour modifier des
commits. Cela préserve la discussion et l'examen qui ont eu lieu plus tôt pour
l'ensemble des modifications respectives.

Le temps requis pour l'évaluation par les pairs est imprévisible et variera de requête
en requête.

Philosophie des requêtes
-----------------------
Les jeux de patchs doivent toujours être ciblés. Par exemple, une requête de fusion 
pourrait ajouter, fonctionnalité, corriger un bug, ou réaffacturer le code; mais pas 
un mélange. Merci également d'éviter les demandes qui tentent d'en faire trop, sont 
trop grandes ou trop complexes car cela rend l'examen difficile.


### Fonctionnalités

Lors de l'ajout d'une nouvelle fonctionnalité, il faut penser à la dette technique à 
long terme et la maintenance que cette fonctionnalité peut nécessiter après l'inclusion. 
Avant de proposer une nouvelle fonctionnalité qui nécessitera un entretien, veuillez 
considérer si vous êtes prêt à le maintenir (y compris la correction de bogues). Si les 
fonctionnalités sont orphelines sans mainteneur à l'avenir, ils peuvent être supprimés 
par le mainteneur du référentiel.

### Réaffacturage

Le réaffacturage est une partie nécessaire de l'évolution de tout projet logiciel. Les 
directives suivantes couvrent les demandes de réaffacturage pour le projet.

Il existe trois catégories de réaffacturage, les mouvements de code, les corrections 
de style du code et le réaffacturage du code. En général, les demandes d'extraction 
de réaffacturage ne doivent pas mélanger les trois types d'activité afin de rendre 
les demandes de réaffacturage facile à examen et non controversé. Dans tous les cas, 
les PR réaffacturés ne doivent pas modifier le comportement du code dans la requête de 
tirage (les bogues doivent être conservés tels quels).

Les mainteneurs de projet visent un redressement rapide sur les demandes d'extraction 
de refactoring, donc si possible, gardez-les courts, non complexes et faciles à vérifier.


Processus de prise de décision
-------------------------

Ce qui suit s'applique aux modifications de code au projet FRAX Core et ne doit 
pas être confus avec les changements de consensus globaux du protocole FRAX.

Si une requête d'extraction est fusionnée dans FRAX Core, la fusion du projet
passe par les mainteneurs et finalement, le chef de projet.

Les responsables prendront en considération si un patch est en corrélation avec
les principes généraux du projet; répond aux normes minimales d'inclusion; et va
juger le consensus général des contributeurs.

En général, toutes les demandes d'extraction doivent:

  - Avoir un cas d'utilisation clair, corriger un bug démontrable ou servir le 
    plus grand bien du projet (par exemple réaffacturage pour la modularisation);
  - être bien évalué par les pairs;
  - suivre les directives de style du code;

Les correctifs qui changent les règles de consensus de FRAX sont considérablement 
plus impliqués que la normale car ils affectent l'ensemble de l'écosystème et doivent 
donc être précédés par des discussions approfondies et des détails clairs. Alors que 
chaque cas sera différent, on devrait être prêt à dépenser plus de temps et d'efforts 
que pour d'autres types de correctifs en raison de l'augmentation de l'examen par les 
pairs et des exigences de consensus.

### Examen par les pairs

Tout le monde peut participer à l'examen par les pairs qui est exprimé par des 
commentaires dans le tirage demandé. En règlex.nérale, les réviseurs examinent 
le code pour détecter les erreurs évidentes. Les responsables du projet tiennent 
compte de l'examen par les pairs pour déterminer s'il y a consensus pour fusionner 
une demande d'extraction (rappelez-vous que les discussions ont pu être répartis 
sur GitHub, les forums, les e-mails et les discussions Discord).  Le langage suivant
est utilisé dans les commentaires "pull-request":

  - ACK signifie "J'ai testé le code et je suis d'accord qu'il devrait être fusionné";
  - NACK signifie "Je ne suis pas d'accord, cela devrait être fusionné", et doit être 
    accompagné d'une justification technique solide (ou dans certains cas, de droit 
    d'auteur / brevet / questions / justification légale).Les NACKs sans motifs ne 
    seront pas traités;
  - utACK signifie "Je n'ai pas testé le code, mais je l'ai examiné et il semble
    OK, je suis d'accord qu'il soit fusionné";
  - Concept ACK signifie "Je suis d'accord sur le principex.néral de cette demande d'extraction";
  - Nit fait référence à des problèmes triviaux, souvent non bloquants.

Les évaluateurs doivent inclure le hash de validation qu'ils ont examiné dans leurs commentaires.

Les responsables du projet se réservent le droit de peser les opinions des pairs 
évaluateurs en utilisant le jugement de bon sens et peuvent aussi peser sur la 
base de la méritocratie:qui ont démontré un ex.gement et une compréhension plus 
profonde envers le projet (au fil du temps) ou avoir une expertise claire du domaine 
peut naturellement avoir plus de poids, comme on s'attendrait dans tous les domaines de la vie.

Lorsqu'un patch affecte le code critique du consensus, la barre sera beaucoup plus élevé 
en termes de discussion et d'examen par les pairs, en gardant à l'esprit que les erreurs 
peuvent être très coûteuses pour la communauté au sens large. Cela inclut le réaffacturage
du code critique du consensus.

Lorsqu'un patch propose de modifier le consensus FRAX, il doit avoir été
discuté longuement sur les forums et Discord, être accompagné d'une large
discussion de proposition et un consensus techniquex.néralement largement 
perçu, un changement valable basé sur le jugement des mainteneurs.

### Trouver des réviseurs

Comme la plupart des critiques sont eux-mêmes des développeurs avec leurs propres projets, 
la revue du processus peut être assez longue, et une certaine patience est nécessaire. 
Si vous trouvez que vous avez attendus trop longtemps pour une requête, cela peut être dûs
à de multiples raisons. En voici quelques unes afin de contribuer au projet dans ces cas :
about:

  - Il se peut que ce soit à cause d'un gel des fonctionnalités dû à une prochaine version. 
    Pendant ce temps, seules les corrections de bugs sont prises en compte. Si votre requête 
    est une nouvelle fonctionnalité, il ne sera pas prioritaire tant que la publication ne 
    sera pas terminée. Attendez la mise à jour.
  - C'est peut-être parce que les changements que vous suggérez ne plaisent pas aux gens. Ne
    le prenez pas personnellement ! Au contraire, prenez un autre regard critique sur ce que 
    vous suggérez et voir si cela: change trop, est trop large, n'adhère pas aux [notes du développeur]
    (doc / developer-notes.md), est dangereux ou non sécurisé, mal écrit, etc.
    Identifiez et résolvez les problèmes que vous trouvez. Puis demandez par ex. sur Slack si 
    quelqu'un peut donner son opinion sur le concept lui-même.
  - C'est peut-être parce que votre code est trop complexe pour tous, sauf quelques personnes. 
    Et ces gens n'ont peut-être pas réalisés que votre demande de traction existe même. Un excellent
    moyen de trouver des gens qui sont qualifiés et se soucient du code que vous touchez est la
    [Fonction Git Blame](https://help.github.com/articles/tracing-changes-in-a-file/). Trouvez
    simplement la personne qui touche le code que vous touchez avant de voir si vous pouvez trouver
    et donner un coup de pouce. Ne soyez pas incessant au sujet du coup de coude cependant.
  - Enfin, si tout le reste échoue, demandez sur Discord ou à quelqu'un d'autre de jeter un oeil
    sur votre requête. Si vous pensez avoir attendu une durée déraisonnablement longue (mois +) 
    sans raison particulière (peu de lignes changées, etc), c'est tout à fait normal. Essayez de
    retourner la faveur quand quelqu'un d'autre demande des commentaires sur son code, et l'univers 
    sera équilibré.


Politique de diffusion
--------------

Le responsable du projet est le responsable de la publication de chaque version de FRAX Core.


Droits d'auteur
---------

En contribuant à ce référentiel, vous acceptez d'autoriser votre travail à la
Licence MIT sauf mention contraire dans `contrib/debian/copyright` ou en haut
du fichier lui-même. Tout travail contribué où vous n'êtes pas l'auteur original
doit contenir son en-tête de licence avec l'auteur ou les auteurs et sa source.
