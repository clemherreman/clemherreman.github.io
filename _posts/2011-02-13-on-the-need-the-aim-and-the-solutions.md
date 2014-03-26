---
layout: post
title: On the need, the aim and the solution(s)
category: thoughts
published: true
---

![Complexité](/images/complexity.jpg)
<legend>Dave Smith, Centre for Mathematical Biology, Uni Oxford</legend>

Un des aspects que j'apprécie le plus dans le développement, est la liberté totale
de ce qu'il est possible de faire. Nous construisons des applications, des logiciels,
[des systèmes entiers, pouvant atteindre des complexités rendant leur appréhension
par un seul cerveau quasiment impossible](http://www.google.com "Google"). Pourquoi ?
Parce que oui, nous construisons, mais contraitement aux maçons, nous construisons
de l'air. De l'intangible. De l'information. Pas de problème de forces, torsions,
d'approvisionnement _(exception faite de café, bien entendu !)_. Là où, lorsqu'on travaille
n'importe comment, rien ne dépasse 2 mètres et s'écroule, dans le développement,
on peut tout à fait construire des applications utilisées par des milliers de personnes,
qui ne tiennent que grâce à des hacks et autres bouts de ficelles. Cette liberté,
cette possibilité de tout faire, permet à certains d'entre nous de faire des merveilles,
mais surtout à d'autres de faire [n'importe quoi](http://stackoverflow.com/questions/130965/what-is-the-worst-code-youve-ever-written/143711#143711).


_Disclaimer : Toute ressemblance avec des situations réelles ou avec des
personnes existantes ou ayant existé ne saurait être fortuite, et découle d'une volonté
de l'auteur de témoigner, afin d'éviter aux générations futures de recommencer cette
horreur. Pour préserver l'anonymat, les noms et fonctions ont d'ailleus été changés._

Prenons un exemple concret. Vous développez une application web, qui affiche des
graphiques sur l'évolution de quelques données métier. Tout se passe au mieux, puis
le directeur financier s'approche, vous félicite pour votre bon travail, et vous demande
si ce serait possible d'avoir, en dessous des graphiques, les mêmes données mais
dans un tableau. Prenez quelques secondes pour imaginer comment vous feriez, sachant
que les données sont extraites d'une base de données, que les diagrammes sont en flash, et que
ces données sont fournies au flash à travers le HTML  :

{% highlight html %}<object type="application/x-shockwave-flash" data="/flash/exemple.swf">
  <param name="flashvars" value="data=SomeSerializedDataToBeDisplayed" />
</object>
{% endhighlight %}

Vous avez trouvé ? Bien. Je pense ne pas me tromper si je dis que vous vous êtes
probablement dit quelque chose d'approchant :
 > Facile. J'ai visiblement déjà les données extraites, puisque je les
 > fournis au Flash. Je rajoute quelques lignes pour créer un `<table>`, quelques
 > minutes de réflexion sur le design, et hop, à moi le ronronnement du directeur financier !

Oui, mais seulement voilà, pourquoi faire simple quand on peut faire autrement ?
Le développeur avec lequel je travaillais, du reste parfaitement compétent et doué,
eu ce jour là un autre idée d'approche. Avec quelques lignes de javascript placées
après la balise flash, il parse le HTML, en extrait les données sérialisées, les parse,
construit à la volée le tableau HTML et affiche le tout. Oui. Rien que ça. 

Je passe outre les problèmes de maintenance, de compréhension, ainsi que les jurons
que prononceraient les pauvres développeurs qui se retrouveraient avec ce code à
maintenir. Et je ne pas pas de la testabilité, des bonnes pratiques _(et des petits chatons morts)_.
Cet exemple montre le large spectre que couvrent les solutions à un même problème. Et
pourtant, le problème est relativement simple. Imaginez que vous deviez écrire un compilateur
pour LISP, ou un système d'exploitation, ou encore [indexer l'Internet dans sa totalité](http://www.google.com).

## Dénoncer c'est bien beau, mais que faire ?

Malheureusement, dans le développement comme dans la religion, il n'y a jamais de réponse
universelle _(sauf éventuellement 42)_. Pas de solution miracle. Pas de
[balle d'argent](http://fr.wikipedia.org/wiki/Pas_de_balle_en_argent). Mais s'il
n'y a pas de méthode ultime, il y a quand même des bonne pratiques, dont une
qui peut sembler évidente, mais qui est paradoxalement dure à appliquer : la
simplicité, aussi connue sous le nom de **KISS : Keep It Simple, Stupid**. L'idée
est que, plus la solution retenue est simple, moins elle est mauvaise, et même parfois bonne.

Personne ne veut de code astucieux, ni de code exploitant une fonctionnalité du
langage connu des 4 core-developpers initiaux. Un bon code est un code **simple à
lire, et encore plus simple à comprendre**, le rendant **logique** et **maintenable** _(et
souvent élégant)_.

> « Write programs for people first, computers second », Steve McConnell - [Code Complete](http://www.cc2e.com/)

Vous avez un projet avec un simple formulaire de contact pour un site vitrine ?
Pas la peine de créer un framework de validation des saisies des utilisateurs. Quelques
lignes suffiront à valider cet unique formulaire. Besoin d'un export vers du XML ?
Pas besoin de créer un meta-language, modélisé par un ensemble de classes, et
faisant la liaison entre vos objets et n'importe quel format d'export imaginable.

**Faites simple, clair, et efficace.**


