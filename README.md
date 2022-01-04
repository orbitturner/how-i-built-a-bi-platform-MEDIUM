
![](https://cdn-images-1.medium.com/max/2880/1*pZ3gQtnYeK_M3Ru36XDMKA.gif)

## Comment j’ai construit une plateforme BI from Scratch sans me suicider.

### Qui suis-je d’abord ?

Avant tout, Salut l’astronaute !

![](https://cdn-images-1.medium.com/max/2000/0*V3RkpTBF-1P9TB1q.gif)

Moi c’est **Orbit Turner** (Mohamed GUEYE de mon vrai nom) je suis un jeune passionné de la technologie, de l’automobile et de design.

J’ai commencé à toucher à mes premières lignes de code quand j’avais 11 ou 12 ans et depuis lors j’ai suivi pas mal de Roadmap en autodidacte mais aussi à travers mes différentes formations avant de finir par devenir un développeur Fullstack en fin 2020 puis DevOps actuellement.



## CONTEXTE

![](https://cdn-images-1.medium.com/max/2000/0*z8adaFDhylUOwkDr.gif)

Tout a commencé en début 2021 où j’ai été contacté par une entreprise Française basée au Sénégal qui cherchait un développeur Fullstack qui pourrait répondre à leurs besoins internes.

Après un long processus habituel ainsi que des tests bizarres j’ai pu rejoindre le vaisseau qui a plus de 17 ans d’existence et près de 600 employés ainsi qu’une infrastructure informatique énorme et complexe.

Ma mission initiale était de proposer un outil capable de suivre et de gérer le workflow du département chargé d’un des clients de la boîte.

Il faut comprendre que l’entreprise est un centre d’appels émetteur  c’est à dire un centre de contact clients Télévente, Enquêtes et Prise de rendez-vous B2B. Ce qui fait que les clients sont souvent de grandes boîtes télécoms françaises ou autres qui nécessitent des métriques (*Statistiques d’appels (DMC, nombre de contacts argumentés, contacts positifs, taux de concrétisation, ventes/fiches livrées, taux de pénétration, attente moyenne, first call résolution, …): en temps réel, par heure, jour, semaine, mois et par téléconseiller / équipe, Tris partiels, suivi des KPI et quotas en cours de terrain, Edition et envoi du suivi terrain — Reporting automatisé quotidien*) et un workflow très spécifique et intensif.

Du moment où j’ai pris connaissance des besoins et une fois mon intégration terminée, le syndrome de l’imposteur s’est installé et je me suis dit : “bah, frère, là, tu es dans la merde jusqu’au cou !”.

![](https://cdn-images-1.medium.com/max/2000/0*dKyCLMV2BYsL6B67.gif)



### LES PROBLEMES

Ah bah là ils étaient nombreux 😨!

* L’entreprise pour la plupart de ses outils, est sur du **Python 2**.

* L’entreprise a une pléthore de Serveurs de Base de données avec une cinquantaine de bases dans chaque serveur ainsi que des millions d’enregistrements tout aussi sensibles.

* L’entreprise veut, en plus d’automatiser certains traitements manuels, avoir une visibilité totale et en temps réel de ce qui se passe. Ventes, temps d’appels, heures badgées, rentabilités, prévisions etc. Ce qui veut dire extraire, transformer et visualiser des rapports très épurés des millions de lignes d’informations éparpillées en moins d’une seconde.

* L’entreprise appelle çà un “***OUTIL***”. 😭😫

* POUR COURONNER LE TOUT, J‘ETAIS LE SEUL DEV 👨🏾‍🦯

![Let me die 😭](https://cdn-images-1.medium.com/max/2000/0*FZrqww3KVXmvhIQU.gif)



### FACE A L’UNIVERS

J’avais une semaine pour proposer un plan d’action et le “***Thinking***’” d’une solution.

Mon syndrome de l’imposteur me disait de faire comme tout ceux qui sont passé avant moi c’est-à-dire : **ME CASSER **!

![](https://cdn-images-1.medium.com/max/2000/0*BkjRA6Oz4j3QGzZP.gif)

Mais la part sadique en moi celle que j’appelle “**Shadow**” s’est pointé avec un sourire narcissique en me disant : “*Tu sais très bien que t’aimes ce genre de truc. On ne vit qu’une fois ! Alors ne réfléchis même pas. Fonce et casse-toi la gueule avec fierté*”. 😫

Oui, comme un idiot, j’ai sauté la tête en première !

Les deux premiers jours comme tout le monde j’étais déjà dans mon bureau à penser aux entités, à comment gérer plusieurs BDD sans tout faire péter, à la Tech Stack, au déploiement, à Docker, aux microservices, au Big O Notation etc. 

Mais, comme à chaque fois que je suis face à un nouveau défi de taille, j’ai pris le temps de me retirer et de penser en dehors des limites.

## THINKING OUT OF THE BOX !



![](https://cdn-images-1.medium.com/max/3200/0*5iukBr0wxk0IdV32.gif)

Depuis toujours j’ai été quelqu’un qui aime aller vite en prenant des raccourcis ou en utilisant ce qui existe déjà. Je refusais toujours de faire une chose deux fois car j’automatisais tout ce qui pouvait l’être. 

‘*C’est simple non ?*’ 
**NON **! Ce n’est pas aussi simple car au fil du temps, des projets et personnes rencontrées on finit par détecter rapidement ceux qui sont faits pour résoudre des problèmes et ceux qui sont faits pour coder. Pour ma part voici comment j’ai pu faire face à mon problème.



![](https://cdn-images-1.medium.com/max/2000/0*DdbAdBzXyNCP5Mfv.gif)

### REDEFINIR LES BESOINS !

Un projet est toujours la définition du besoin de quelqu’un et quand une personne vous fait part de ce qu’il veut c’est évident qu’il dira tout ce qui lui passe par la tête.

Ce qui différencie un projet de dev pour une entreprise et un projet de dev pour un client lambda, c’est que bien souvent l’entreprise veut, comme elle le surnomme, “**un outil à tout faire**” qui leur permet de travailler et de gérer leurs différentes opérations mais la différence réside dans le fait que cet outil n’a souvent pas de date de livraison ou de version finale. Aussi bien que l’entreprise vivra l’outil grandira.

Donc l’étape cruciale a été de dire à notre DSI: “*Ok cool ! Je vois ce que vous attendez de moi. Maintenant, on commence par quoi ?*”.

Cela paraît banal mais redéfinir les besoins c’est tout d’abord redécouper le besoin en plusieurs petits blocs puis les organiser par priorité. Oui, çà a un nom, c’est être : **AGILE!**

![](https://cdn-images-1.medium.com/max/2000/0*4FrvQsYDeqsV0bom.gif)

Ensuite l’étape suivante était de revoir, avec un grand recul, l’évolution sur le long terme et d’en déduire la nature même de ce qui sera réalisé.

Il faut savoir qu’en fonction des premières demandes j’ai cru qu’il s’agissait d’un *ERP*. Alors il fallait même si je savais c’était quoi un *ERP*, le redéfinir clairement et le comparer aux besoins.

Selon *Oracle* un ERP est : 
>  Un type de logiciel que les entreprises utilisent pour gérer leurs activités quotidiennes telles que la [comptabilité](https://www.oracle.com/sn/erp/financials-cloud/), les [achats](https://www.oracle.com/sn/erp/procurement-cloud/), la [gestion de projets](https://www.oracle.com/sn/erp/project-portfolio-management-cloud/), la [gestion des risques et la conformité](https://www.oracle.com/sn/erp/risk-management/), ainsi que les [opérations de supply chain](https://www.oracle.com/sn/erp/what-is-erp/). Une suite ERP complète comprend également un logiciel de [gestion de la performance](https://www.oracle.com/sn/performance-management/) (EPM) qui aide à planifier, budgétiser, prévoir et générer un rapport sur les résultats financiers d’une entreprise.

Cependant même si plusieurs modules du projet se rapprochaient de çà, ce n’était pas autant un full ERP. La partie analyse, métriques et suivi était beaucoup plus importante. Sachant aussi que la boîte avait déjà un ERP gérant tous les départements et que ses données à lui aussi seront intégrés dans la nouvelle plateforme.

Alors en faisant le dossier technique qui étudie en profondeur certains aspects des besoins et des départements pour lesquels l’outil allait être mis en place on se rapprochait de plus en plus d’une plateforme, et pas n’importe laquelle !
***Une Plateforme de Business Intelligence !***😫

Mais c’est Quoi réellement le BI ?

Alors, Selon encore *Oracle* 😅:
>  La [Business Intelligence (BI)](https://actualiteinformatique.fr/data/definition-business-intelligence) est un processus technologique d’analyse des données et de présentation d’informations pour aider les dirigeants, managers et autres utilisateurs finaux de l’entreprise à prendre des décisions business éclairées. La Business Intelligence englobe une grande variété d’outils, d’applications et de méthodologies qui permettent aux organisations de collecter des données à partir de systèmes internes et de sources externes. Ces données sont ensuite préparées pour l’analyse afin de créer des rapports, tableaux de bord et autres outils de [Data Viz](https://www.oracle.com/fr/database/data-visualization-definition.html) pour rendre les résultats analytiques disponibles aux décideurs et aux opérations.

I GOT IT 🔥 C’est de çà qu’ils ont besoin !

Oui c’est vrai Aujourd’hui, les entreprises s’appuient sur les logiciels de Business Intelligence pour identifier et extraire des informations précieuses des grands volumes de données qu’elles stockent. Ces outils permettent d’en tirer des informations tels que des veilles concurrentielles et les tendances du marché, ainsi que des informations internes telles que trouver les raisons des opportunités perdues, etc.

Cette étape est ce qui a permis de bien comprendre la direction à suivre ainsi que l’état d’esprit à avoir. 

Bien que cela fait plusieurs années maintenant que je suis dans le développement, je n’ai jamais eu à faire ce genre de truc ni eu ce genre de responsabilité d’être celui qui allait jeter les bases d’un si grand projet. Mais je me sentais capable de le faire au fond alors j’ai pris mes boules à deux mains et j’ai commencé les travaux.

## LE JEU DU LEGO

Il y a une loi que j’affectionne particulièrement. Celle de **Gall**.

![](https://cdn-images-1.medium.com/max/2000/0*JwlFs-Hai2CN3LgA)

La loi de Gall explique pourquoi le prototype et l’itération sont des méthodes de création de valeurs qui fonctionne bien. Au lieu de créer un système complexe en partant de zéro, **il est beaucoup plus facile de construire un prototype**.

La raison principale en est qu’**un système complexe est constitué d’une quantité importante de paramètres et de dépendances**. C’est la logique du mouvement *Lean-Startup* avec la création puis l’amélioration d’un *MVP*.

Je ne me suis pas dès le départ dit que j’allais construire une plateforme BI. **Je ne me suis pas dit que j’allais créer un système hyper performant** avec du load balancing, du caching, et des optimisations sur tout etc.

J’ai commencé par la construction d’un squelette rigide qui me permettrait en avançant de placer mes blocs  sans fragiliser la structure. Les décisions du départ ont été les clés de la suite.



### L’ARCHITECTURE

![](https://cdn-images-1.medium.com/max/2000/0*coLy1oCLAevNGihH)

Au départ j’étais là à me faire toutes les architectures possibles du monde BFF, Microservices, Micro-Frontend, etc.

Mais vous comprendrez bien que Rome n’a pas été fait en un jour. À cause de notre passion nous sommes bien souvent sous la “hype” de vouloir utiliser ou tester tout ce qui sort. Mais ces solutions s’appliquent à des problèmes spécifiques. Si les FAANG ou GAFAM sortent tout le temps de nouvelles architectures, frameworks, etc.; ce n’est pas par volonté mais par nécessité. Les noms viennent souvent bien après. Au cours de ce projet j’ai eu à faire certains choix, certains tweaks et résoudre certains problèmes avant de me rendre compte qu’il y avait un nom pour çà.

J’ai commencé le projet avec une architecture distribuée pour, en progressant et au fil des besoins pouvoir tendre vers de l’extrême ‘***Segregation of Principle***’ en faisant du *MICRO MICRO* 😂

## FRONT-END FIRST 

“C’est une Blague 😨?!” 
Non ! Le premier défi et le plus grand bien sûr était côté backend. 
‘*Comment me connecter à toutes ses bases et réunir toutes ces données ?*’

C’était une question à laquelle je n’avais pas encore de réponse mais je suis quelqu’un qui aime bien, comme je vous l’ai dit plutôt, aller vite. Vu que tous les yeux étaient rivés sur moi il fallait que je me montre à la hauteur et quoi de mieux que du bluff 😏.

Que ce soit en entreprise ou dehors ce que voit les utilisateurs et les demandeurs c’est le front. Alors je ne pouvais pas passer une semaine de plus à dire que je faisais des recherches. Vu que je suis très à l’aise avec le design, j’ai commencé à directement faire l’intégration de ce que j’avais faits comme mockup et proto avec ***ANGULAR ***afin que mon DSI ait au moins quelques choses à se mettre sous la dent entre-temps.

J’ai dû dès le départ déployer dans l’un de nos serveurs en interne une version de l’application et mettre en place un pipeline de CI/CD afin que chaque 02 ou 03 jours, ils puissent suivre les évolutions avec fierté.😂

Oui j’ai choisi **Angular **en front et les raisons étaient nombreuses. À mon avis quand on parle de projet d’entreprise, de plateforme ou d’outils de gestion c’est le meilleur choix en matière de **technos JS**. Son architecture orientée scalabilité, sa maturité, sa structuration et sa stabilité font qu’il facilite l’uniformisation et l’évolution de la solution construite. 
J’ai l’habitude de dire que Angular est dans les technos JS ce que JAVA est face aux autres langages. Il est strict et puissant et très orienté scalabilité.
>  Cependant ce n’est pas à cause d’Angular que la plateforme est devenue ce qu’elle est.Angular, React, Svelte, Vue, Laravel ce sont tous des outils ! 
Comme ce qu’est un crayon dans la main d’un architecte. C’est à cette main d’en faire un excellent usage et d’en créer un joyau.

En une semaine j’avais déjà le login, l’accueil ainsi que plusieurs composants UI qui rendait le projet très facile à assembler.

Dès le départ j’ai voulu trouver des raccourcis très efficaces et évolutifs. Après la redéfinition des besoins j’ai su qu’on aura beaucoup de ‘***Data Visualisation***’ sur la plateforme ainsi je me suis orienté vers les Suites ou bibliothèques de composants UI tels que*** [Syncfusion](https://www.syncfusion.com/)***, [***KendoUI](https://www.telerik.com/kendo-angular-ui)***, ***PrimeNG***, etc.

En général un seul suffit. Une fois le choix effectué, c’était autour du UI crafting. Je passais plusieurs jours à créer des composants réutilisables permettant à la demande de créer une interface, page ou module rien qu’en les appelants et les paramétrant.

### FRONT ARCHITECTURE & CODING CONVENTION

En commençant le projet j’ai su que j’aurais tôt ou tard besoin de prendre plus de gens avec moi pour aller plus vite. Mais il fallait que ces gens en arrivant comprennent facilement et rapidement comment est structuré le projet et comment y contribuer. 

Ainsi j’ai fait un document définissant les conventions de codage par rapport à Angular au niveau de la boîte. C’est un document d’environ 15 pages mis à la disposition de tous les gens de l’IT et les nouveaux dev tel que l’incroyable [Ababacar Diene Ndiaye](undefined) qui à su prendre la relève avec succès.🔥

En voici un p’tit aperçu.

### ARBORESCENCE DES DOSSIERS

Nous appliquons l’arborescence de base d’un projet Angular. Cependant le dossier ***src ***qui contient toutes les fonctionnalités de l’application nous l’avons organisé comme suit :

![](https://cdn-images-1.medium.com/max/2000/1*a1e5FVCvKqQdCyLKtDsGmw.png)

Comme vous pouvez le voir on a créé certains dossiers afin de faciliter la lisibilité du projet.

### LE DOSSIER COMPONENTS

Le dossier component contiendra toutes les vues et composants UI du projet. Nos applications la plupart du temps utiliserons un système de [Module Séparation](https://angular.io/guide/feature-modules) ([Voir ici](https://blog.angular-university.io/angular2-ngmodule/)) alors ce dossier sera organisé 
 comme suit :

![](https://cdn-images-1.medium.com/max/2000/1*aLZPwkJ1gKXopXJ_PhcQrA.png)

### Ui-elements

On y mettra tous les composants unitaires qui pourront être utilisés un peu partout indépendamment du module. Par exemple : *un DataGrid, Un Graphique, Chart Generator, Les Exporters, un bouton, une Card, un Modal*, etc.

### Layout

On y mettra tous les composants qui constituent notre “**Theme Styling”** et les différents Modules de l’application. Par exemple : Module Admin et son theme, Navbar, Module Générale, etc.

### View

Dans ce dossier on trouve toutes les pages/vues du site organisées en sous-dossier en fonction des modules auxquels elles appartiennent. Ces vues seront rattachées aux **ChildRoutes **prévu afin qu’elles passent par leurs modules respectifs lorsqu’elles sont appelées.

### LE DOSSIER CONFIG

Dans ce dossier on trouve tous les fichiers de configuration globale de l’application en cours. On y mettra par exemple : les liens vers le backend, la langue par défaut, l’état de l’appli en debug ou en prod, etc.

![](https://cdn-images-1.medium.com/max/2000/1*r-y5sHo-MfUaGB-QVostWQ.png)

### LE DOSSIER HELPER

![](https://cdn-images-1.medium.com/max/2000/1*DFl6HCDqXSf1RdoYSRgY1Q.png)

En plus de l’architecture orientée Composant d’Angular j’applique ce que j’appelle une ‘***Micro-Architecture orientée Helpers’***. On peut considérer les helpers comme des providers qui permettent à plusieurs modules de partager ou d’utiliser un moteur de traitements afin d’éviter la duplicité de code.

Pour ne pas surcharger le fichier “*components.ts*” d’un composant quand celle-ci nécessite de faire certains traitements, on lui crée un Helper ce qui permet même dans le futur si un autre module a besoin de ce traitement ou de ces données il n’appellera que l’helper.

## LE DOSSIER MODELS

Comme son nom l’indique il contiendra toutes les interfaces (types) de notre système si besoin en est.

## LE DOSSIER MODULES



![](https://cdn-images-1.medium.com/max/2000/1*hM-C6vwuDHjhmHGOeBPa3g.png)

Ce dossier contient tous les composants complexes formant à eux seuls un mini-système isolé. Exemple : le module de notification, le Logger du système, l’encoder (afin de compresser ou de crypter certains payloads parfois), etc.

Euh…😑 dès que j’ai pas de nom pour un package ou un utilitaire que je crée, je le préfixe par ‘***Orbit***’ c’est pas par narcissisme 😂😂😂. 

### LE DOSSIER ERROR

![](https://cdn-images-1.medium.com/max/2000/1*4C_zhl5MFJ9boTFrspJphQ.png)

Dans ce dossier on trouve les pages d’erreurs ainsi que le module de gestion d’erreur. Ce dernier permet d’intercepter, d’étudier et de gérer toutes les erreurs de notre application. À la fin de chaque journée les logs sont regroupés puis envoyés en Base afin de nous permettre de les étudier.

*Exemple de logs en base :*

![](https://cdn-images-1.medium.com/max/2220/1*dJqBVnt0nqrAeNmKa1PvzQ.png)

### LA SECURITE & LE MONITORING

La sécurité est l’un des aspects les plus importants de l’application. Voilà pourquoi nous disposons d’un “**encoder / decoder**” en front et Back car aucune des informations qui transite entre nos applications n’est mis en clair (Oui même le token 😂).

![](https://cdn-images-1.medium.com/max/2000/1*-8QtJ1lceSfKJvQRtwFR6g.png)

Surtout les quelques infos sauvegardées dans le *LocalStorage *bien qu’il ne soit pas sensible nous les encryptons puis les compressons afin de les rendre illisibles pour les humains 😅 ou hors de l’appli.

![](https://cdn-images-1.medium.com/max/2732/1*oUsTdZ1GM0F7wXghLacxIA.png)

En plus notre ***Encoder ***nous permet de pouvoir avoir plus d’infos dans les paramètres de certaines de nos requêtes GET tout en gardant celle-ci très courte.

![Nous avons ici une requête GET avec un payload contenant une matrice de DateRange dans ses paramètres.](https://cdn-images-1.medium.com/max/2000/1*jvsmN6TJ7MN3BYd2mWfZEg.png)

___

Nous avons aussi différents helpers de monitoring et de suivi qui nous permettent d’avoir toutes les infos sur les utilisateurs ainsi que leurs actions afin de mieux suivre l’appli ou d’éviter certaines fraudes ou réclamations mensongères😂. Exemple ci-dessous les utilisateurs peuvent avoir des infos plus poussées sur leurs IP privé dans notre réseau (*différent de l’ip publique*) ainsi que d’autres infos qui peuvent aider l’équipe SI à intervenir rapidement en cas de nécessité:

![](https://cdn-images-1.medium.com/max/3158/1*l5RDWvmWzRs7ElOwPsV85w.png)

Pour l’authentification nous utilisons aussi notre propre Package NPM basée sur [Auth0](https://auth0.com/fr) qui s’appelle :** [Orbit-JWT](https://www.npmjs.com/package/orbit-jwt)**. 😏 Il nous permet en quelques lignes de gérer l’Auth & d’attacher le token sur les headers, sans avoir à faire d’intercepteur et beaucoup d’autres choses...

Tout ceci fait que le frontend est très évolutif, claire et facile à manager ! 🥳

Par exemple pour une interface complexe comme celle-ci : 

![Ignorez le thème de Noël 😅](https://cdn-images-1.medium.com/max/2556/1*pDqveM4-0VmQ6YZi5W83pg.png)

![Ignorez encore le thème de Noël 😅](https://cdn-images-1.medium.com/max/2104/1*-uTL5Nott8I5niqswPsb9g.png)

Où nous avons principalement :

* Un Composant de filtre Global (*paramétrable avec plus de 05 filtres [date range, typeahead select, switch, etc*).

* Une DataGrid avec des filtres sur toutes les colonnes, la possibilité de trie, ainsi que la ligne des agrégations en bas.

* Un composant **d’Export **permettant d’avoir les données sous n’importe quel format.

* etc …

Aussi complexe qu’elle soit nous le construisons facilement dans l’application en moins de 50 lignes(*je sais ! 😫 le nombre de lignes ne définit pas la qualité du code*). Comme ici dans le fichier ***x.component.html ***:

![Above pages component.html](https://cdn-images-1.medium.com/max/3200/1*W3mnWz349qeVh3qAfpfnKg.png)

![SneakPeak of The Component.TS !](https://cdn-images-1.medium.com/max/3200/1*GJREJ0Fscgbaxls-y_QT_Q.png)

Exemple des *viz* dans notre Front (*Pleins de gribouillage car certaines données peuvent être sensibles*):

![](https://cdn-images-1.medium.com/max/3200/1*Umt_7ywKpjufdLYejXBhew.png)

![](https://cdn-images-1.medium.com/max/3200/1*Z-E0ahnCSQ7vlF45A0si3g.png)

![Dummy Data Inside ](https://cdn-images-1.medium.com/max/2000/1*f6WY-CbATYXCKAUar6-wKQ.png)

![](https://cdn-images-1.medium.com/max/2060/1*ZozmuPylXkyD7-WHLWFvdA.png)

![](https://cdn-images-1.medium.com/max/2000/1*yF0ZJ3xbj6EU_KyelYLgMw.png)

![](https://cdn-images-1.medium.com/max/2000/1*4is_kbgQ46_nD-pum5yAKg.png)

Tout ce qui est DataViz And So Much More !!!! :

![](https://cdn-images-1.medium.com/max/2000/0*luua9c1JnLhge-va.jpg)

![](https://cdn-images-1.medium.com/max/2388/0*gSbQMXhgh9LBJqze.jpg)

…

Lors des premiers mois le front faisait 70% du traitement à travers différents helpers car je voulais aussi voir jusqu’où je pouvais pousser Angular et aussi parce que les demandes étaient nombreuses et qu’il fallait les faire vite. Et pourtant les perfs étaient très acceptables. D’où l’importance de se concentrer sur l’architecture plus que sur les technos. Car aussi cool qu’une tech soit, c’est celui qui l’utilise qui déterminera ce qu’il en fera.

Cependant, vous vous doutez bien que les données que manipule le front viennent du back. Alors je vais vous parler de comment j’ai pu résoudre l’un de mes plus grands défi en 2021 avec une facilité incroyable !

![](https://cdn-images-1.medium.com/max/2000/1*3qN5rLjcnAmaWFn7upM31Q.gif)



![PART 2 : REBIENVENUE !](https://cdn-images-1.medium.com/max/2880/1*jEOkV21c73sA72EFFCwkUQ.gif)

## LE BACKEND 

Hooooo ! L’informatique ! ☺

Elle avance à un rythme effréné ! 
Avant, le choix de la technologie (*Langage de programmation*) était primordial avant de commencer un projet. Elle (la techno) déterminait ce qu’on pouvait faire ou non et les limites.

Je ne dis pas que ce n’est plus le cas, mais cette grande barrière entre les technos n’existe presque plus. De nos jours que ce soit Java, Python, JS/TS, ou même PHP ils sont tous capable de construire une application à très grande charge et hyper performante.

Javascript m’a toujours plus. Mais durant ce projet j’ai été ébahi de la puissance de cette technologie qu’on a tendance à sous-estimer. JS a su évoluer très vite tout en gardant sa charmante simplicité qui permet à tout le monde d’embrasser son univers sans prise de tête.

Sa mutation, **Typescript**, permet d’exploser nos limites et de le placer dans le rang du cercle restreint des langages matures tels que Java. Je ne fais pas de confrontation entre Java et JS mais c’est un fait que ce langage rivalise avec les technos compilées et continues d’être tout aussi performant et élégant.

En faisant mes recherches sur la problématique de la connexion aux multiples bases de données, j’ai testé plusieurs technos pour un ***Proof of Concept***. 


JAVA était bien trop ennuyeux avec ses très grandes fonctions pour faire de petite choses. 
DotNet était très cool mais demandait plus de ressources et pour agrandir l’équipe allait couter plus cher.
PHP j’en avais un peu marre et la mise en place pour résoudre ce problème était trop pénible.
Puis je me suis dit : “*bon voyons voir avec NodeJS*”.

**NodeJS **est la chose la plus merveilleuse qui est arrivé à JS. Elle a permis à JS d’atteindre les sommets et de conquérir le monde. Mais celui-ci est trop open dans ses implémentations et normes ce qui laisse à chaque développeur le soin de faire ce qu’il veut comme il veut.

Donc il me fallait une organisation à la Java mais  qui prendrait tous les avantages d’Angular.

Et là comme une révélation je me suis souvenu que je connaissais un truc similaire et son nom c’est : [**NEST JS](https://docs.nestjs.com/)**. 🔥🚀

### NESTJS LE SAUVEUR !

![](https://cdn-images-1.medium.com/max/2000/0*eWk8EhcO3sq7gHer.gif)

Mon choix dès le POC a été une évidence. Cette techno présentait tous les avantages d’Angular et permettait à tous ceux qui avaient souffert auparavant avec Express de découvrir les bienfaits de l’évolution et de se concentrer sur le plus important pendant que le Framework s’occupait du reste.

Je ne vous ferais pas la liste de tous ce qu’il y a à savoir sur **NestJs **mais je vous conseille cet article qui en parle plus en détails en plus de sa [Documentation Officielle](https://docs.nestjs.com/) qui est l’une des meilleures au MONDE :

[https://codeburst.io/why-you-should-use-nestjs-for-your-next-project-6a0f6c993be](https://codeburst.io/why-you-should-use-nestjs-for-your-next-project-6a0f6c993be)



### CONNECTING TO THE DATABASES 

Comme annoncé plusieurs fois l’entreprise possède des données entassées depuis plus de 17 ans dans différents serveurs et différentes bases de différents types.

Si j’avais voulu créer des entités & relations pour chaque base de chaque système j’aurais pris un an pour tout finir sans prendre en compte les erreurs et le risque de tout supprimé dans une table à cause d’une mauvaise manip.

Il fallait sortir du cadre, être ingénieux sur la méthode. J’avais la technologie, j’avais les besoins mais comment extraire les données 🤔.

C’est évident qu’il me fallait du **Database First** ! Mais la seule techno qui était vraiment à l’aise avec çà c’était .Net C# et je voulais çà avec Nest. Alors je me mis au travail. 

D’abord la connexion aux bases progressivement en fonction de ceux qui m’intéresse d’abord : 

![Early app.module.ts | DB Connect](https://cdn-images-1.medium.com/max/3200/1*dvGVZWyYrdvWpUccd9lT9w.png)

Vu que j’avais choisi TypeOrm comme ORM il ne me restait plus qu’à définir chaque connexion dans le AppModule (comme ci-dessus) et en donnant les infos pour me connecter à une base. Sachant aussi que cela peut se faire de manière dynamique.

Puis je n’avais plus qu’à préciser à dans les modules ala DB à utiliser :

![C’est tout !🥳🥳](https://cdn-images-1.medium.com/max/3200/1*2xeEztwCwGruZz_0Y9OMwQ.png)

Je me sentais déjà invincible ! 🚀🔥

![Oui comme çà 😂](https://cdn-images-1.medium.com/max/2000/1*iJJqkNC66NMUSV-m2-G-zg.gif)

Il restait cependant un autre problème. 

*Comment maintenant questionner ou manipuler facilement toutes ces données sans pour autant avoir à écrire toutes les **Handlers **dans mes **Controllers **et toutes les méthodes dans mes **services **?*

GraphQL peut-être ? 🤔

*Dans ce cas aussi comment prévoir toutes les questions ou filtres possibles sans écrire toutes les resolvers ?*

😂 Oui je suis vraiment très très LAZY 😂 Je cherche TOUJOURS des raccourcis.

Je me souviens qu’à cette période un de mes potes m’avait dit : “*Bro tu sais toi tu veux toujours faire l’impossible, mais cette fois-ci ce que tu demandes même Dieu n’a pas la réponse*” 😂😂😂😂.

En gros je voulais avoir une REST API mais qui se comporterais comme du GraphQL c’est à dire que dans les requêtes GET je pourrais filtrer à la volée les données que j’allais récupérer en base. Donc la requête GET construira indirectement la requête SQL.

![](https://cdn-images-1.medium.com/max/2000/0*WqkOO2fMMmNnkWJa.gif)

Le pourquoi ?! Parce que dit comme çà cela paraît complexe mais l’impact est énorme dans le système si directement en front je suis capable de poser des questions comme: 
‘*Quels sont les Utilisateurs actifs dont le log commence par F, qui ont un âge compris entre 30 et 40 ans et sont de nationalité sénégalaise ?*’ 
et que je n’ai pas à anticiper çà dans le backend avec des méthodes prévu dans les Controllers et les Services, j’aurais un système incroyablement flexible et léger.

Qu’en est-il aussi de tous ces CRUDs à faire pour des centaines de tables et une panoplies de bases ?

Il me fallait trouver un moyen d’automatiser cela et de régler ce problème de redondance dès le départ. 

C’est là qu’au milieu de tout ce chaos, après des jours et des jours de recherche, je ne sais plus comment, je tombe sur un microframework pour NestJS dit : “[***@nestjsx/crud](https://github.com/nestjsx/crud)***”.

![Oh My God 😂😭](https://cdn-images-1.medium.com/max/2000/0*zmv3t5mjvB2bWmlm.gif)

Je ne rêvais pas ! Ce truc existait vraiment et pourtant peu de gens étaient au courants 😭😭

### NESTJSX/CRUD

![](https://cdn-images-1.medium.com/max/2000/1*sZ9uJNdriCdtMvyzCl4Fug.png)

Ce truc me permettait d’avoir, comme dans le code à droite ci-dessus, des CRUDs complets, la possibilité de Filtrer, paginer, relationner et trier les informations dont j’avais besoin pendant la récupération même en base avec des requêtes hypers optimisées et safe ([en savoir plus](https://github.com/nestjsx/crud/wiki/Requests#query-params)) !

Par exemple voici la requêtes pour la question que j’avais posé sur les utilisateurs plus haut :
>  ‘Quels sont les Utilisateurs actifs dont le log commence par F, qui ont un âge compris entre 30 et 40 ans et sont de nationalité sénégalaise ?’

![](https://cdn-images-1.medium.com/max/3028/1*6xjzzVHP8JWmKAd7D9-s7Q.png)

En réalité le SQL est construis en fonction de la requête (logique tu me dira mais boff fais un tour sur leur doc tu comprendra ce que je veux dire). 

Dans le code l’implémentation est tout aussi simple. Par exemple pour avoir les endpoints ci-dessous ainsi que leurs documentations Swagger :

![Welcome Page of The API](https://cdn-images-1.medium.com/max/3192/1*uRAAQoAfF_YbE6bLYQcHGg.png)

On aura dans le controller :

![Logs Controller](https://cdn-images-1.medium.com/max/2000/1*mIGSr8J16U2QqHZxj9jqTw.png)

Et dans le service :

![](https://cdn-images-1.medium.com/max/2000/1*ityXwAqQc-2i3_5n4Caaug.png)

C’est Tout ! 😂

Dans le cas où, comme dans 60% du temps, besoin de plus de traitement spécifique, on aura qu’à faire un Override des méthodes existantes ou en créer de nouvelles comme dans nos autres applis.

Exemple :

![](https://cdn-images-1.medium.com/max/2458/1*vxHs16vXMeiMrCI7YDuTWg.png)

Donc j’étais capable de faire beaucoup plus de chose en peu de temps. 

Je suis tellement fan de cette bibliothèque que j’ai fini par contribuer à son code sur GitHub pour ajouter une petite fonctionnalité.

Mais il me restait toujours la question des entités 😭.

### ENTITIES GENERATION 

Comme je l’ai dit plutôt même si je pouvais spécifier dans la configuration de chaque BDD que l’app ne peut pas écraser la base, je pouvais pas accepter de passer mon temps à faire des entités pour ***TypeORM ***et mettre des mois à faire des relations par ci et par là. 

Donc maintenant vous connaissez la chanson comme le générique de Carglass : Je prends par un raccourci et je génère !

Le prochain Héro c’est un package npm : [***typeorm-model-generator](https://www.npmjs.com/package/typeorm-model-generator)***.

Comme son nom l’indique il permet de générer directement les entités TypeOrm en se basant sur la base qui lui a été donnée. 

Avec une ligne comme celle-ci : 

![](https://cdn-images-1.medium.com/max/2928/1*Z4OfmWzcaJQR9JstgIAw9g.png)



![](https://cdn-images-1.medium.com/max/2000/0*C2L36DGg5Wtff6cP.gif)

Je pouvais générer les entités pour toutes les tables de la base spécifiée avec les relations et tout !



Cette base solide et bien optimisée pour aller vite à permis de bien assoir le projet et de commencer à seulement deux mois du démarrage à enchainer les livraisons.

### NESTJS ARCHITECTURE

La hiérarchie côté back est très similaire au front avec une méthodologie orientée helpers qui permet de partager les traitement entre plusieurs modules et de faciliter la réutilisation et l’évolution.

Au départ j’avais pensé chaque module comme un microservice et déployé à part mais je me suis rendu compte que j’étais dans de l’Over-Engineering vis-à-vis du contexte et que les gains de performance étaient très discutables.

![](https://cdn-images-1.medium.com/max/2000/1*gcAcQ-lCrpOsmDz06t3ECQ.png)



Ensuite j’ai gardé cette même idéologie que j’ai implémentée dans le même backend vu que Nest justement avait un design très orienté modularité qui te permet d’avoir plusieurs blocs indépendants dans ton appli.

***Par exemple: ***si j’ai besoin d’utiliser le tableau de suivi des ventes et performances des agents dans les modules de la Suivie qualité, J’importe le “helper” des ventes qui génère ce tableau complexe dans le module qualité puis-je l’utilise dans mes services en faisant une injection de dépendance dans le constructeur.

![Fichier du Module Qualité ](https://cdn-images-1.medium.com/max/2046/1*HtbFoTpSNUvV-3xOJISOFA.png)

![Quality.Service.ts](https://cdn-images-1.medium.com/max/2000/1*VFfGj3O0F1Htcq6Ky7DCwQ.png)

![BACKEND MODULES DEPENDENCIES FLOW](https://cdn-images-1.medium.com/max/3198/1*9u3HN4otGgnO2VTj-_NM0A.jpeg)

### ETL PROCESS

![](https://cdn-images-1.medium.com/max/2000/0*UVcxDzjtCC2X5B08.gif)

Vous vous doutez que quand on parle de BI, on parlera forcément de l’ETL.

Selon la définition d’internet, c’est un processus automatisé qui prend les données brutes, extrait l’information nécessaire à l’analyse, la transforme en un format qui peut répondre aux besoins opérationnels et la charge dans un Data Warehouse. L’ETL résume généralement les données afin de réduire leur taille et d’améliorer leur performance pour des types d’analyse spécifique.

Dans notre cas la phase de ‘***Load***’ sera plus associés à du ‘***Visualize***’ car même si parfois les données traitées sont mis dans une base séparée. 

La structure Backend bien géré nous permet de nous concentrer sur les algorithmes et processus à mettre en place afin de pouvoir exploiter ces grandes masses de données.

Il faut savoir que d’habitude pour une application “normale” comme on a l’habitude d’en faire pour de petits clients beaucoup de choses sont ignorés côté code. Tels que le temps d’appel à la BDD, le timing des boucles, leurs types, ainsi que la performance en temps et en ressources d’une fonction, d’un helper ou d’un Microservice.

Sous le poids de toutes ces données la moindre petite optimisation est exponentielle sur l’ensemble d’un module.

Il nous est arrivé de passer plusieurs heures à faires des Benchmark entre une boucle **FOR **normale (*for i …*) et une boucle **FOR OF**. Plusieurs heures à tester plusieurs méthodes pour itérer sur des tableaux. Plusieurs jours à implémenter différents algorithmes de recherche, trie ou de graph et à mesurer leur performance.

Plusieurs semaines à mettre en place nos propres implémentations ou surcouche d’ORM car parfois certains besoins sont tellement spécifiques qu’aucune ORM ne pourrait prévoir cela donc on est obligé de créer nos propres solutions et de les optimiser.

![Exemple d’un Service Utilitaire permettant de Gérer des Transactions, Requêtes Préparées, Vues, etc sur des Bases SQL SERVER](https://cdn-images-1.medium.com/max/3200/1*RHn8bDIH2gtxzEaVKy_Rsg.png)

Nos services ETL sont souvent organisés comme suit :

![SERVICE GERANT L’ETL D’UN MODULE](https://cdn-images-1.medium.com/max/3200/1*ZcQp0Oeo8uhcCfAlDkIMAA.png)

Les données obtenues sont souvent transmises au frontend sous forme de statistiques afin que les components de ***DataViz ***afin de générer les Graphiques et Charts. 

### PREDICTION & PREVISION AI (TENSORFLOW JS)

Machine Learning et DataScience avec … JavaScript 😨?! Oui, c’est possible🥳. Python n’est pas le seul langage que vous pouvez utiliser pour le faire.

[**Tensorflow ](https://www.tensorflow.org/js?hl=fr)**a une version JS qui permet de s’approprier le ML ou DS avec JS. Je ne suis qu’à mais tout début avec Tensorflow donc cette partie “***Prediction***’” est actuellement gérée depuis l’ API de Power bi. Mais nous nous déportons de plus en plus vers [**Hal9](https://hal9.com/) **basée sur TF qui nous permettront d’avoir facilement plusieurs accès à la prédiction juste avec leurs APIs:

![HAL9 Prediction Services](https://cdn-images-1.medium.com/max/2000/1*TVruAWRu8Po2rPMGAw3lRQ.png)

…

Une fois que tout cela a été mis en place les autres challenges étaient de toujours réussir à répondre aux différentes demandes en termes de Dashboard, de métriques, de fonctionnalités tout en gardant l’appli toujours plus rapide et disponible.

Nous allons aborder maintenant la dernière partie. Celle qui à chaque nouvelle feature représente un nouveau défi.

## OPTIMISATION LIFECYCLE

### UN DEVELOPPEUR ? KESAKO?🤔

On va parler sérieusement.

C’est bien beau tout çà. C’est super de voir à quel point les technologies ont évolué pour en arriver là. Cette rapidité, ces frameworks à tout faire etc.

Mais tout commence par la base : les **BASICS**. 
J’ai constaté que de nos jours cette même beauté des technos qui font la course au plus ouvert ou à celle qui la plus courte learning curve, à fait que plein de débutant ou de nouveau venu se sont rué vers cette facilité oubliant de passage ce que c’est réellement **développer**.

Coder, c’est facile. Tout le monde est capable de mémoriser du code ou de faire dire à une machine “1+1 = 2”. Mais **DEVELOPPER **est une autre chose, une science, une philosophie, un état d’esprit.

Développer ce n’est pas suivre un tuto de 10 minutes sur comment faire une todo liste avec react et le reproduire. 
Non ! Ce n’est pas non plus lire et retenir par cœur tous les livres sur les Design Patterns, le clean code, les structures de données…

Être développeur ce n’est pas connaitre des algorithmes mais c’est **Algorithmer**. Ce n’est pas maîtriser toutes les technos mais c’est savoir répondre efficacement et rapidement à un besoin, une problématique en prenant en compte le contexte et les facteurs secondaires avec les ressources adéquates.

Enfin c’est savoir créer si çà n’existe pas car un framework c’est avant tout un langage de programmation qui lui-même est un ensemble de paradigme de programmation. Dans certain il est préférable de comprendre comment est créé la structure plutôt que d’y être un simple locataire.

Avant de parler optimisation, cache, load-balancing, Vertical/Horizontal Scaling il faut parler algo et langage.

### SELF OPTIMISATION 

En tant que dev on est amené à toucher énormément de technologie cela dit rien ne nous empêche de nous spécialiser dans un langage de notre choix qui représentera notre base algorithmique. Tout comme [Jeff Delaney](undefined) plus connu sur la chaine #fireship, j’ai appris par moi même pleins de technos.

Mais je me suis spécialisé sur JS car j’en avais envie et que c’était un très large univers. 

Juste avant de commencer ce projet, j’avais eu la très bonne idée de recommencer JS depuis la base pour remonter même cela faisait plusieurs années que je l’utilisais avec ces frameworks. Et j’ai été surpris !

Surpris de voir que JE NE SAVAIS RIEN !

![](https://cdn-images-1.medium.com/max/2000/0*t9sM0V5kZtDxvCbX.gif)

C’était comme si il y avait **JS** qui était la vrai technos et moi depuis tout ce temps je faisais quelques choses de très similaire mais qui ne l’était pas le **HS**.

Redécouvrir le langage de base sur lequel mon projet était fait m’a permis non seulement d’écrire du code de plus en plus logique mais de plus en plus performant.

Réapprendre l’asynchrone, le RxJs, les DataStructures m’ont permis de non pas multiplier mais de rendre exponentielle la vitesse d’exécution de certains traitements. Et même mon ordinateur était plus heureux: On était devenu Potes à nouveau 🥳

![Me and My Computer’s Incarnation Dancing👨🏾‍🦯](https://cdn-images-1.medium.com/max/2000/0*Xgi9rKdxWihG6hxZ.gif)

Les Design Patterns, les architectures et toutes les méthodologies que l’on passe nos journées à lire, ont fini par rentrer naturellement, en fonction des problèmes que je rencontrais mais ce qui ne viendra jamais naturellement C’est une bonne Algorithmique/Logique. Çà on le cultive !

## CODE OPTIMISATION

Il y a une tonne de manière d’optimiser un code. Mais dans tous les cas cela se fait **progressivement**.

On ne peut pas avoir une demande urgente avec une deadline serrée et se dire qu’on va faire le Héros en écrivant du Code Parfaitement “**CLEAN**”. Si tu t’obstines à le faire il est très fort probable que la chaise de ton bureau les prochains mois soit parfaitement clean et ton compte bancaire aussi.

![You’ll be nicely fired ! 👨🏾‍🦯👨🏾‍🦯](https://cdn-images-1.medium.com/max/2000/0*17mcY-xP7_p5O1VP.gif)

Attention ! 🙄 Je vous vois venir cela ne veut pas dire que tu ne dois pas écrire du code lisible et logique mais juste que le fait qu’il soit clean, organisé et optimisé ce fais progressivement après que la logique de la feature demandée est déjà étée implémentée.



### UTILISER LES METHODES DU LANGAGE

Chaque langage vient avec ses innombrables fonctions embarquées. Celles-ci ont été souvent faites en prenant en comptant tous les aspects de performances. Elles sont vos meilleures amies pour vous éviter de télécharger énormément de dépendances inutiles ou de créer un autre bordel qui tuera le prochain développeur à se pencher dessus.

En ce qui concerne Javascript, les ‘*Built-in Functions*’ (tels que les méthodes sur les arrays, etc) sont vos meilleurs amis. Il est très peu probable que vous ayez besoin de quelque chose qui n’a pas déjà été fait.

### BE ASYNC !

Le codage asynchrone est largement utilisé dans Node.js pour assurer un flux opérationnel non bloquant. Les E/S asynchrones permettent à d’autres traitements de continuer avant même la fin de la première transmission. Le codage synchrone peut potentiellement ralentir votre application. Il utilise des opérations de blocage qui pourraient bloquer votre fil principal, ce qui réduira considérablement les performances de votre App.

L’impact est énorme ! On parle parfois d’une notation Big O en “[***O(log n)](https://jarednielsen.com/big-o-factorial-time-complexity/)***”.

Exemple : Ci-dessous nous avions une fonction qui permettait de séquencer des opérations. Le problème est que chaque ligne ici attend celle précédente avant de se lancer.

![First Version Of Sequentializer](https://cdn-images-1.medium.com/max/2000/1*x5iGhOY79Bwjvt7eMeJsvg.png)

Après une p’tite optimisation nous avons :

![Second Version](https://cdn-images-1.medium.com/max/2000/1*46et6dr3TuEbSIWAWbrnDQ.png)

*Je sais 😑 Le résultat n’est pas retourné pour certaines raisons, IT’S NOT THE POINT*.

Ci-dessus on exécute les lignes de la première séquence simultanément ce qui nous permet de diviser par 4 le temps d’attente. Notez l’élégance du “***Promise.all()”*** 😍JS est vraiment...🥰

Imagines-toi maintenant faire cela partout où c’est possible. La rapidité du système se fait ressentir sur tous les modules. Par exemple j’ai certaines règles qui me force toujours à la volée de penser et d’écrire du code plus ou moins optimisé. Comme :

* “*J’éviterais toujours de parcourir totalement un tableau”*

* “*Je vérifierais toujours si une chose n’existe pas avant de le faire.*”

* “*Je n’ai pas besoin de commentaire si le code parle de lui-même*”

Etc… C’est peut-être bête mais c’est avec çà que je m’en sors toujours. (Presque 😂).

En comparaison il nous arrivait d’attendre 8 à 10 minutes pour visualiser un graphique sur la suivie de production. Aujourd’hui cela ne nous prend que **~200ms** si on désactive le cache REDIS car avec le cache la même requête prend **~4ms**.

![](https://cdn-images-1.medium.com/max/2000/0*pMjsQsEbiR76tKdb.gif)

### AVOID MEMORY LEAKS

**Unsubscribe your Subscribers !!!!**

J’ai passé deux semaines à courir derrière une lenteur générale au niveau de mon frontend alors je vous recommande cette pépite qui, si vous utilisez Angular réglera tous vos soucis:
[**Avoid Memory Leaks in Angular**
*The lifetime of some global components, such as AppComponent, is the same as the lifetime of the app itself. If we know…*dev.to](https://dev.to/theoklitosbam7/avoid-memory-leaks-in-angular-5gla)

Je ne vais même pas vous expliquer ce par quoi je suis passé. Voici en tout cas ce à quoi çà ressemble en images :

![PERF MONITOR Dealing With Memory Leaks](https://cdn-images-1.medium.com/max/5932/1*9SdOaxBTGecHWr9gF1gyxg.jpeg)

Et voilà ceux à quoi doit ressembler le moniteur de Perf en temps normale : 

![PERF MONITOR AFTER PREVENTING ML !](https://cdn-images-1.medium.com/max/3200/1*uRb9Tt2-Zzzq7Pga4ZPw3Q.png)

Dans notre cas “**l’Unsub ”**est fait automatiquement par un helper. Si vous voulez éviter ce genre de chose mieux vaut utiliser l’async pipe au maximum sur vos Comp.HTML.

Une fois que vous maitrisez assez votre workflow de développement et que vous avez optimisé au maximum votre code, Il est alors temps de mettre en cache certains traitements ou données.



### SUPPRIMEZ LES TEMPS D’ATTENTE AVEC UN CACHE !

La mise en cache côté serveur est l’une des stratégies les plus courantes pour améliorer les performances d’une application Web. Son objectif principal est d’augmenter la vitesse de récupération des données, soit en passant moins de temps à calculer ces données ou à effectuer des E/S (telles que la récupération de ces données sur le réseau ou à partir d’une base de données).

Un cache est une couche de stockage à grande vitesse utilisée comme stockage temporaire pour les données fréquemment consultées. Vous n’avez pas besoin de récupérer les données de la source principale (généralement beaucoup plus lente) des données à chaque demande.

La mise en cache est plus efficace pour les données qui ne changent pas très souvent. Si votre application reçoit de nombreuses demandes pour les mêmes données inchangées, le stockage dans un cache améliorera considérablement la réactivité de ces demandes. Vous pouvez également stocker les résultats de tâches gourmandes en calculs dans le cache, tant qu’il peut être réutilisé pour d’autres requêtes. Cela évite que les ressources du serveur ne s’enlisent inutilement en répétant le travail de calcul de ces données.

Un autre candidat courant pour la mise en cache est les requêtes API qui vont à un système externe. Supposons que les réponses puissent être réutilisées de manière fiable pour des requêtes ultérieures. Dans ce cas, il est logique de stocker les demandes d’API dans la couche de cache pour éviter la demande de réseau supplémentaire et tout autre coût associé à l’API en question.



![](https://cdn-images-1.medium.com/max/2000/0*sQQnjCS7aYsCtD0S)

À ce stade je n’étais plus tout seul j’avais un autre grand esprit avec moi et nous avons choisi d’aller sur dû [REDIS](https://redis.io/).

Son [intégration avec **NestJS](https://docs.nestjs.com/techniques/caching)** était hyper facile et nous disposions de toutes les ressources pour le mettre en place. Dès le premier jour nous étions ébahis du gain de performance que nous venions d’avoir. Nous nous prenions même pour des rivaux à Google car on surfait sur la vibe de la rapidité.

On parlais maintenant de moins de **7ms **! Nous avons passé des jours à célébrer çà.😂😂😂😂

En front la mise en cache côté navigateur faisait déjà le boulot puis la limitation, l’épuration de notre “**bundle Size”** et la gestion du ***Memory Leak ***nous ont permis de ne plus avoir de latence UI.

## LE SCALING

Nous avons comme je l’ai dit plutôt, déployé d’abord avant de continuer nos builds et livraisons. Ce workflow très orienté DevOps nous a permis très tôt de penser à des solutions pour le scaling futur de notre application. 

Bien que nous ayons toutes les ressources que l’on désirait j’ai toujours refusé d’utiliser plus que ce dont j’avais besoin. Ce qui veut dire que durant toute son existence. L’appli (Front & Back) était déployée dans l’un de nos plus faibles serveurs.

Une machine avec 4 Giga RAM, un disque HDD et un processeur i7. Tout ce qu’il y a de plus banal.

![](https://cdn-images-1.medium.com/max/2000/0*ndrqyq-94QBAKimZ.gif)

C’était la meilleure manière de nous forcer à avoir une bonne architecture et du bon code optimisé. 

D’autant plus que dans ce serveur on trouve aussi d’autre application tels qu’un Project Management Interne que j’ai mis en place et qui gère toutes l’équipe IT (*je vous en reparlerais dans un autre article*), les fiches de présences, projets/tâches, ainsi que le Helpdesk et les demandes de congés; un serveurs MySQL utilisé par certaines applis mais aussi pour nos tests. Eh OUI ! 😂

Pourtant plus il y avait de module plus la plateforme devenait performante car on appliquait toujours [***la règle du BoyScout](https://informaticienzero.github.io/la-r%C3%A8gle-du-scout-97-choses-qu-un-programmeur-doit-savoir/)***.

Côté CI/CD que ce soit pour le front ou le back nous avons pas mal de scripts exécutés au moment du BUILD qui permettent entre autres de : Versionner l’application, Copier ou déplacer le contenu du “**dist**” vers le dossier de déploiement, Mettre à jour le GIT & le GITHUB, et d’autres choses effectuées en PostBuild.

### HORIZONTAL SCALING

Depuis le début de cet article vous n’avez vu nulle part où je configure un LoadBalancer ou Docker.🧐 Ma plateforme en est-elle affectée ? NON !

Tout est une question de contexte. On ne peut pas tout faire en même temps ni tout maîtriser en même temps. J’ai une tonne de technos que je ne maitrise pas et pourtant cela ne m’empêche pas de faire des choses qui marchent bien.

Nous avons utilisé NGINX comme serveur web et reverse proxy car c’était le plus adéquat et performant pour des applications tournant sur NodeJS. Implémenter un load-balancer ne nous prendrait pas plus de temps une fois la plateforme Dockerisé. 

Cependant dès le départ j’ai voulu isolé et monitorer mes applis tournant sur nodeJS sans pour autant avoir à configurer Docker pour chacune d’elles.

Là encore une fois j’ai découvert [**PM2 ](https://pm2.keymetrics.io/)**!

PM2 est un “***process manager***” qui permet de faire pas mal de chose avec une appli node. Je vous laisse le plaisir d’aller voir par vous-même.

Mais en gros, il est utile d’utiliser un gestionnaire de processus pour :

* Redémarrez l’application automatiquement si elle plante.

* Obtenez des informations sur les performances d’exécution et la consommation de ressources.

* Modifiez les paramètres de manière dynamique pour améliorer les performances.

* Contrôler le clustering.

Un gestionnaire de processus est un peu comme un serveur d’applications : c’est un « conteneur » pour les applications qui facilite le déploiement, offre une haute disponibilité et vous permet de gérer l’application au moment de l’exécution.

Une fois toute la configuration faites sur PM2 nous étions capables d’avoir en temps sur console ou en ligne des infos précises sur la plateforme et son utilisation et d’en déduire des actions.

Exemple :

![Realtime Log On PM2 WEB](https://cdn-images-1.medium.com/max/3196/1*-SZI430Q6GBhqcSMM6yRTA.png)

![Monitoring Multiple Apps On Different Servers](https://cdn-images-1.medium.com/max/3200/1*lSRI4XFpJJ7zs0pLbZkYmQ.png)

Mais le plus incroyable c’est le [**clustering](https://blog.appsignal.com/2021/02/03/improving-node-application-performance-with-clustering.html)**.

### C’EST QUOI LE HORIZONTAL SCALING D’ABORD ?

C’est la capacité d’augmenter la capacité du serveur en connectant plusieurs entités matérielles ou logicielles afin qu’elles fonctionnent comme une seule unité logique. L’H-Scaling peut être obtenue à l’aide du ***clustering***, du ***système de fichiers distribué*** et du ***Load Balancing***.

Une instance de Node.js s’exécute dans un seul thread, ce qui signifie que sur un système multicœur (ce que sont la plupart des ordinateurs de nos jours), tous les cœurs ne seront pas utilisés par l’application. Pour profiter des autres cœurs disponibles, vous pouvez lancer un cluster de processus Node.js et répartir la charge entre eux.

Avoir plusieurs threads pour gérer les requêtes améliore le débit (requêtes/seconde) de votre serveur car plusieurs clients peuvent être servis simultanément. Nous répartissons la Charge de demande sur plusieurs instances de notre application.

Celle-ci peut être plus ou moins facile à implémenter dans une appli qui vient de démarrer mais dans notre cas c’est au dernier moment qu’on a voulu le faire. Ne me demandez pas pourquoi 😫 C’est la vie! c’est comme çà ! Facebook aussi au début c’était de la merde.👨🏾‍🦯

On avait trop la flemme de retoucher nos modules et/ou toute notre app. C’est là que PM2 nous a encore sorti une carte car du CLUSTERING il est capable de le faire sur app déjà faites. Et comment ?

Bah Juste Comme çà ! 🥳 Il te duplique ton process et gère le balancing lui-même comme un grand ! 🔥✨

![THE PM2 GOD](https://cdn-images-1.medium.com/max/2916/1*Pi--ZgOf3HLUFSa-8DrrHA.png)



![](https://cdn-images-1.medium.com/max/2000/0*NaNLSX28OU_CeGtH.gif)

Ce n’est pas tout à chaque nouveau déploiement PM2 reload et mets à jour les instances One by One tout en **s’assurant de n’avoir aucune downtime** !!

![LIST OF ALL RUNNING INSTANCE on Terminal](https://cdn-images-1.medium.com/max/3200/1*TWFoFU_YKq22Y7q_d8_g1A.png)

![MONITORING INSTANCES AND THEIR LOGS ON TERMINAL](https://cdn-images-1.medium.com/max/3200/1*PLkwwjB8hkittGz9JOIliA.png)

![](https://cdn-images-1.medium.com/max/2000/0*-161VjWKwpte27xZ.gif)

Si vous voulez en savoir plus sur comment configurer un Clustering avec PM2 je vous conseille cet article :
[**Improving Node.js Application Performance With Clustering | AppSignal Blog**
*When building a production application, you are usually on the lookout for ways to optimize its performance while…*blog.appsignal.com](https://blog.appsignal.com/2021/02/03/improving-node-application-performance-with-clustering.html)

### Async vs MultiThread

Il s’agit d’une idée fausse générale que la programmation asynchrone et le multithreading sont identiques. Mais ils ne le sont pas. La programmation asynchrone concerne la séquence asynchrone des tâches, tandis que le Multithreading est plusieurs threads ou processus fonctionnant en parallèle.

Le Multhreading est un moyen d’asynchrones dans la programmation, mais nous pouvons également avoir des tâches asynchrones sur un single thread.

Le multithread agit au niveau du processeur alors que l’asynchrone est au niveau des opérations du programme.



### **ENFIN LE SUIVI & LE MONITORING**

Avant d’essayer d’améliorer les performances d’un système, il est nécessaire de mesurer le niveau de performance actuel. De cette façon, vous connaîtrez les inefficacités et la bonne stratégie à adopter pour obtenir les résultats souhaités. L’évaluation du niveau actuel de performances d’une application peut nécessiter l’exécution de différents types de tests, tels que les suivants :

* **Test de charge** : fait référence à la pratique consistant à simuler l’utilisation attendue d’un système et à mesurer sa réponse à mesure que la charge de travail augmente.

* **Tests de résistance** : conçus pour mesurer les performances d’un système au-delà des limites des conditions de travail normales. Son objectif est de déterminer combien le système peut gérer avant qu’il ne tombe en panne et comment il tente de se remettre d’une panne.

* **Spike testing **: permet de tester le comportement d’une application lorsqu’elle reçoit une augmentation ou une diminution drastique de la charge.

* **Test d’évolutivité **: utilisé pour trouver le point auquel l’application cesse de se mettre à l’échelle et identifier les raisons qui la sous-tendent.

* **Test de volume** : détermine si un système peut gérer de grandes quantités de données.

* **Test d’endurance** : permet d’évaluer le comportement d’une application logicielle sous une charge soutenue pendant une longue période, pour détecter des problèmes tels que des fuites de mémoire.

L’exécution de certains ou de tous les tests ci-dessus vous fournira plusieurs mesures importantes, telles que :

* ***temps de réponse***

* ***latence moyenne***

* ***taux d’erreur***

* ***requêtes par seconde***

* ***débit***

* ***Utilisation du processeur et de la mémoire
utilisateurs concurrents
et plus.***

Après avoir mis en place une optimisation spécifique, n’oubliez pas de relancer les tests pour vérifier que vos modifications ont eu l’effet souhaité sur les performances du système.

Il est également important d’utiliser un outil de surveillance des performances des applications (APM) pour garder un œil sur les performances à long terme d’un système. Différentes solutions de surveillance peuvent s’en occuper pour vous. 

Aussi le suivi des utilisateurs et de leurs actions dans le cas d’un produit d’entreprise permet de prévenir les fraudes et actions frauduleux et de dégager la responsabilité ou non de ceux qui sont ciblés.

![Juste comme çà 😂😅](https://cdn-images-1.medium.com/max/2000/0*WPreLe7zQBP-6LHd.gif)

Aujourd’hui jours après jours nous continuons à relever des défis et à répondre toujours à des demandes tout aussi folles ! Mais nous n’avons aucune crainte quant à l’évolution et à la rigidité de notre application. Il nous reste beaucoup de choses à parfaire et à implémenter mais nous le faisons avec fierté et sagesse.

Ce n’est pas à cause de mon talent ou de mon génie qu’aujourd’hui cette plateforme est là où il est, NON. C’est parce que j’ai eu la chance d’avoir pu me poser des limites. D’avoir su qu’il fallait poser de petites pierres bout à bout pour avoir cette structure.

J’ai eu aussi la chance d’avoir un DSI avec un mindset incroyable qui m’a permis de tester ce que j’avais en tête. Qui a su tolérer mes erreurs et qui m’a permis d’évoluer.

Mais je dois aussi beaucoup de choses à ce que nous développeur on oublie très souvent, les SOFTSKILLS. Être développeur c’est avoir aussi une intelligence des situations et un certain tact qui permet de saisir les opportunités là où y en a et de faire un impact dans la tête et le cœur des gens. 

**Car au final on fait un logiciel pour des humains et non de simples utilisateurs.**



## QUELQUES SCREENSHOT DE LA PLATEFORME

En raison d’un NDA et de tralala pareil je ne vous montrerais pas une version complète de l’application et des autres fonctionnalités. Néanmoins je reste ouvert pour toutes questions supplémentaires.

![Login Page](https://cdn-images-1.medium.com/max/3188/1*oiguzoVBpQyqTbLYtRjtuQ.png)

![Error Login — Ignore The SnowFlakes](https://cdn-images-1.medium.com/max/3200/1*QGsyzjeuZt6pa7BpnKbQEg.png)

![Welcome !](https://cdn-images-1.medium.com/max/3192/1*MtwzTOnIYA8EJGvmPRj04Q.png)

![Dark Mode and Eyes Protection](https://cdn-images-1.medium.com/max/3200/1*uybY2AY1veBxIpQ4Vgky5w.png)

Les utilisateurs reçoivent de jolies mails animés quand une actions importante est effectué sur leur comptes (réinitialisation, blocage, inscription):

![Mails](https://cdn-images-1.medium.com/max/3200/1*m4uv6IqTCsnzFk99LfP99g.png)

![Calcul en temps réel de données saisie sur un tableau remplaçant des feuilles excel](https://cdn-images-1.medium.com/max/3200/1*PFYGgB-sH4Yk5QIkjV9Fhw.png)

Plusieurs modules nécessitent le remplissage de données ou la création du tableau complexe donc nous avons implémenté un component de Grids qui permet d’avoir soit un élément avec toutes les fonctionnalités Excel soit carrément une alternative à Excel :

![Yup We Have Our Own Excel 🥳😂](https://cdn-images-1.medium.com/max/3196/1*91-fuE87BXGkSI4YgnuVfw.png)

…

FIND ME ON MY WEBSITE:
[**🚀 ORBIT WORLD ⍟ Keep Going Further 🚀**
*What does it look like working with me or futurize? Discuss the project The customer at the center of the project ! I…*orbitturner.com](https://orbitturner.com)

![](https://cdn-images-1.medium.com/max/2880/1*2hrmhN7k7U_fKLrYkOOkZg.gif)








