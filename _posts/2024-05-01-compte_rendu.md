---
title: Compte-rendu
#author: evadoys
date: 2024-05-01 +0800
#categories: [Blogging, Tutorial]
#tags: [writing]
math: true
toc: true
---

# Présentation 


Dans le cadre de cette étude, nous ambitionnons d’explorer les modalités comportementales d’un individu sous l’influence de son temps d’écran. Ces modalités sont représentées par trois variables fondamentales : l’ennui, la solitude et la productivité. L’ennui se manifeste comme la composante principale de l’ensemble des facteurs influençant les variations du temps d’écran. Les deux autres variables, quant à elles, jouent un rôle essentiel dans la modulation de l’ennui à travers une série d’interactions et de situations critiques. Une interaction peut se comprendre comme la production d’un résultat induit par des co-effets propres à un ensemble de variables étudiées. Ceci peut aussi tout aussi bien s’interpréter comme le résultat d’une conjonction simultanée de plusieurs variables descriptives du problème étudié. Précisons que chaque variable évolue dans un domaine défini, chaque domaine étant représenté par un ensemble de valeurs discrètes, décrivant, en un sens, une échelle de valeurs possibles pour la variable en question. Mentionnons enfin qu’il existe des valeurs critiques propres à chaque variable. Ce sont généralement des valeurs extrêmes du domaine relatif à la variable représentant des seuils, à partir desquels certains effets critiques pourront apparaitre. Citons, comme exemple, qu’un temps d’écran supérieur ou égal à 15 heures par jour risque de produire des effets indésirables sur la santé, notamment en dégradant les vertus réparatrices du sommeil.



# Auteurs 

Les différents auteurs de ce projets sont : 

- Laplagne Anis
- Bouchenna Damia
- Sekher Nadine
- El Filali Fatine
- Celyan Menzou

# Description synthétique du projet

<span style="color:green">**Problématique**</span> : Comment le temps d’écran influence-t-il au quotidien notre productivité,
solitude et ennui ?

<span style="color:green">**Hypothèse principale**</span> : Le temps d'écran quotidien a une influence significative sur les niveaux de productivité, de solitude et d'ennui des individus. Une réduction ciblée et régulée du temps passé devant les écrans améliorera ces aspects.

<span style="color:green">**Hypothèses secondaires**</span>:

- Les individus peuvent adapter leur comportement en fonction des règles imposées pour réguler le temps d'écran.
- Les interventions basées sur des règles dynamiques sont plus efficaces pour réduire le temps d'écran que des interventions statiques ou non personnalisées.
- La réaction à la régulation du temps d'écran varie significativement entre les individus, influencée par des facteurs personnels comme les habitudes préexistantes et la disposition à changer.

<span style="color:green">**Objectifs** </span>: 
- Développer un modèle dynamique qui simule l'impact de différentes règles de régulation du temps d'écran sur la productivité, la solitude et l'ennui.
- Identifier des règles efficaces pour maintenir ou réduire le temps d'écran à un seuil qui favorise une amélioration de la productivité et une réduction de la solitude et de l'ennui.
- Tester la robustesse du modèle en effectuant des simulations sur différents groupes d'individus pour évaluer la variabilité des réponses.

<span style="color:green">**Critères d’évaluation** </span>:
- Réduction du temps d'écran : Mesurer la baisse effective du temps d'écran dans les simulations où les règles efficaces sont appliquées.
- Amélioration de la productivité : Évaluer l'augmentation de la productivité en corrélation avec la réduction du temps d'écran.
- Diminution de la solitude et de l'ennui : Analyser les changements dans les niveaux de solitude et d'ennui en réponse à la régulation du temps d'écran.
- Adoption des règles : Observer la fréquence à laquelle les individus suivent les règles imposées et les ajustements spontanés de leur comportement en réponse à ces règles.

# Présentation structurée des résultats

Nous avons décidé pour ce projet d'utiliser un automate finis non déterministe (AFN). Celui-ci permet de représenter plusieurs possibilités de transitions pour un même état et un même symbole d'entrée. Par ailleurs, contrairement aux automates déterministes, les AFN offrent une plus grande flexibilité dans la modélisation. Ils peuvent facilement être adaptés pour inclure de nouvelles règles ou comportements sans restructurer tout l'automate, ce qui est avantageux dans les études comportementales où les réactions peuvent être imprévisibles ou non linéaires. Enfin, les AFN sont bien adaptés pour gérer les états ambigus où plusieurs résultats peuvent être possibles à partir d'une même condition initiale. Cela reflète la réalité des processus décisionnels humains où plusieurs choix peuvent être envisagés dans une situation donnée. 

### Définition mathématique d'un AFN : 

Soit $A = (Q, \Sigma, \delta, I, F)$ un quintuplet où : 

- $Q$ est un ensemble fini d'états
- $\Sigma$ l'alphabet (ou ensemble fini de symboles)
- $\epsilon$ un symbole qui n'est pas dans $Q \cup \Sigma$ ($\epsilon$ transition ou transition arbitraire)
- $I \subseteq Q$ l'ensemble des états initiaux
- $F \subseteq Q$ l'ensemble des états terminaux de l'automate
- $\delta : Q \times (\Sigma \cup \{ \epsilon \}) \longrightarrow \mathcal{P}(Q)$ avec $\mathcal{P}(Q)$ l'ensemble des parties de $Q$

### Variables d'états

Suite à des sondages que nous avons effectués, nous avons émis comme hypothèses les règles suivantes : 

$$
    \begin{cases}
    p^+ \Rightarrow e^- \\
    p^- \Rightarrow e^+ \\
    p^0 \Rightarrow e^0\\
    e^+ \Rightarrow s^+\\
    e^- \Rightarrow s^-\\
    e^0 \Rightarrow s^0\\
    e^+ \Rightarrow t^+ \\
    e^- \Rightarrow t^-\\
    e^0 \Rightarrow t^0\\
    p^+ \Rightarrow t^- \\
    p^- \Rightarrow t^+\\
    p^0 \Rightarrow t^0\\
    \end{cases}
$$


Expliquons en détails ces règles. Par exemple prenons la première ligne $p^+ \Rightarrow e^-$, cela signifie : "Si la productivité augmente, alors l'ennui diminue". Un autre exemple, la ligne $p^0 \Rightarrow t^0$ signifie : "Si la productivité ne change pas, alors le temps d'écran ne change pas". Ainsi, chaque symboles dans $\Sigma$ est un quadruplet qui indique la direction et l'intensité des changements appliqués à chaque variable d'état.


### Exemple d'utilisation de l'AFN de façon très simpilifié

Le but de cette section est de proposer de façon très simplifié comment l'AFN fonctionne sans rentrer dans trop de détails technique pour permettre aux lecteurs de mieux comprendre.

Supposons que chaque état dans $Q$ représente un profil comportemental basé sur les niveaux des quatre variables d'état. Les états pourraient être catégorisés comme suit:

- Faible : Faible temps d'écran et faible ennui
- Moyen : Temps d'écran moyen et ennui moyen
- Elevé : Temps d'écran élevé et ennui élevé

De plus, l'état initial pourrait être basé sur les observations initiales des variables d'état. Par exemple, si l'individu commence avec un temps d'écran élevé, mais une productivité et un ennui moyens. Par exemple, partons d'un état initial élevé. Ainsi, les états terminaux ($F$) pourraient être ceux où un équilibre souhaitable est atteint, par exemple, faible temps d'écran et haute productivité. Par conséquent, la fonction de transition pourrait être utilisée de la sorte : 


$$
\begin{cases}
    \delta(Elevé, (+0,1, -0.05, -0.2, +0.15)) &\longrightarrow  \{moyen \} \\
    \delta(Moyen, (0,0,-0.3, +0.3)) &\longrightarrow \{Faible \} \\
\end{cases}
$$

**Exemple de mode de fonctionnement** : 
- Jour 1 : L'individu commence à un état <span style="color:orange">élevé</span>
- Jour 2 : L'automate applique $(+0,1, -0.05, -0.2, +0.15)$ qui pourrait le mener à l'état <span style="color:orange">Moyen</span> selon la fonction $\delta$
- Jour 3 : L'automate applique $(0,0,−0.3,+0.3)$, menant potentiellement l'individu à l'état <span style="color:orange">Faible</span>, un état terminal où les objectifs sont atteints.



![Image 1](/images/i1.png)

On peut observer sur le schéma comment l'AFN fonctionne avec $\Delta_1 = (+0,1, -0.05, -0.2, +0.15)$ et $\Delta_2 = (0,0,−0.3,+0.3)$

## Implémentation en Python

### Chargement des packages et initialisations et personnalisation

```python
import itertools
import math
import random

import matplotlib as mpl
import matplotlib.pyplot as plt
import numpy as np
from tqdm.notebook import tqdm
```


A des fins de personnalisation, on se propose de définir une petite fonction qui nous permet de construire des couleurs "originales"...

```python
def rescale_color(*colors):
    col = np.asarray(tuple(colors)) / 255
    return col


MYLIGHTGREEN = rescale_color(24, 167, 69)
MYLAVENDE = rescale_color(113, 91, 192)
MYPINK = rescale_color(244, 112, 144)

MY_ORANGE = rescale_color(245, 73, 29)
MY_BLUE = rescale_color(38, 48, 151)
MY_BLUE2 = rescale_color(77, 122, 181)
MY_BACK = rescale_color(245, 245, 245)
MY_MAROON = rescale_color(157, 12, 12)
MY_GREEN = rescale_color(12, 108, 4)
MY_YELLOW = rescale_color(245, 240, 206)
```

Enfin, Les lignes qui suivent permettent de spécifier les valeurs d'un certain nombre de paramètres graphiques pour personaliser les tracés.

```python
mpl.rcParams.update(
    {
        "pgf.texsystem": "pdflatex",
        "font.family": "serif",
        "text.usetex": True,
        "pgf.rcfonts": False,
        "axes.spines.right": False,
        "axes.spines.top": False,
    }
)
```

## Définition des structures de données et des fonctions de haut niveau

La variable `global_rules` représente une liste de tuples décrivants les interactions décritent plus haut. Il s'agit de __toutes les règles__ qui ont été identifiées en première instance. Il n'est pas exclus qu'il en manque, ou que certaines doivent être affinées. Ce sera un des points à vérifier. A titre de rappel, le tuple `('p+', 'e-')` représente l'implication $\textrm{p+} \Longrightarrow \textrm{e-}$, i.e., lorsque le niveau de production hors activité connexe aux réseaux sociaux augmente, alors l'ennui diminue.

```python
global_rules = [
    ("p+", "e-"),
    ("p-", "e+"),
    ("p0", "e0"),
    ("e+", "s+"),
    ("e-", "s-"),
    ("e0", "s0"),
    ("e+", "t+"),
    ("e-", "t-"),
    ("e0", "t0"),
    ("p+", "t-"),
    ("p-", "t+"),
    ("p0", "t0"),
]
```

La fonction `generate_state` se charge de construire un état possible, représenté par un quadruplet $[e^\varepsilon,s^\varepsilon,t^\varepsilon,p^\varepsilon]$ où $\varepsilon \in \\{0, +,- \\} $. Cet état est construit de façon aléatoire via la fonction `random.choices`, Dans le cas présent, le tirage se fait selon une loi uniforme. 

En effet, soit $\Sigma = \\{+, 0, - \\}$ et soit $(e,s,t,p) \in \Sigma^4$. On définit la fonction $G : \\{\emptyset \\} \longrightarrow \Sigma^4, x \mapsto (e^{\epsilon}, s^{\epsilon}, t^{\epsilon}, p^{\epsilon})$ où $\epsilon \in \Sigma$. Pour une valeur $x \in \\{e,s,t,p \\}$, la probabilité que $x$ prenne une valeur spécifique $\epsilon \in \Sigma$ est donnée par : 

$$
\mathbb{P}\{x = \epsilon \} = \dfrac{1}{\lvert \Sigma \rvert}
$$

Comme la fonction $G$, qui génère un quadruplet d'états, utilise cette distribution uniforme pour chaque variable indépendamment, on trouve : 

$$
\forall y \in \{\emptyset \}, \mathbb{P} \{G(y)\} = \left(\dfrac{1}{3} \right)^4 = \dfrac{1}{81}
$$


```python
# Génération d'un état possible
def generate_state():
    return list(
        map(
            lambda x: str(x[0] + x[1]),
            list(zip(["e", "s", "t", "p"], random.choices(["-", "0", "+"], k=4))),
        )
    )
```

La fonction `generate_rules_from_state` se charge de construire toutes les implications possibles depuis un état généré. En somme, elle construit toutes les règles d'interactions possibles - au sens des règles définies au préalable - que l'on peut obtenir depuis un état. Par exemple, supposons que l'état en cours soit `si = ['e+', 's+', 't0', 'p0']`. L'appel `generate_rules_from_state(si)` fournit les résulats suivants:

```shell
[('e+', 's+'),
 ('e+', 't0'),
 ('e+', 'p0'),
 ('s+', 'e+'),
 ('s+', 't0'),
 ('s+', 'p0'),
 ('t0', 'e+'),
 ('t0', 's+'),
 ('t0', 'p0'),
 ('p0', 'e+'),
 ('p0', 's+'),
 ('p0', 't0')]
```

En d'autres termes, il s'agit de générer toutes les permutations à deux éléments parmi quatre possibles. La formule générale d'obtention des permutations à $p$ éléments parmi $n$ possibles est $\displaystyle{p!\binom{n}{p}}$. Dans notre cas, nous aurons un total de $\displaystyle{2!\binom{4}{2}}=12$ possibilités.

Afin de simplifier les codes, nous utiliserons la fonction `permutations` du package `itertools` pour construire notre liste d'implications.


```python
# Fonction generate_rules_from_state
def generate_rules_from_state(state):
    return list(itertools.permutations(state, 2))
```

Par ailleurs, passons à l'une des implémentations les plus compliquées, c'est-à-dire celle de la fonction `generate_action`. Dans ce cadre, nous allons tenter d'être le plus exhaustif possible afin d'en fournir une explication complète. Notons que cette fonction fait appel à deux fonctions locales dont les productions seront détaillées un peu plus loin.

Les paramètres de la fonction sont `rule` et `bump_value`. 

- `rule` décrit une règle (une implication) sous la forme d'un tuple tel que décrit plus haut;
- `bump_value` est la valeur positive qui devra être appliquée à une coordonnée d'un état en cours. Rappelons qu'un état est un quadruplet $(e,s,t,p)$ valant, par exemple $(1,2,1,4)$ à un instant d'observation $t_i$, $i=0,\cdots,N$, où $N$ est l'horizon de la période d'étude (par exemple, $N$=30 jours).

Ceci étant posé, la fonction commence par analyser chaque composante du tuple représentant la règle passée en paramètre. Pour chaque composante, on extrait la __lettre__ et le __signe__. Comme on considère qu'un état est toujours construit selon l'ordre $(e,s,t,p)$, nous allons donc appeler la fonction locale `get_index_from` qui, en fonction de la lettre passée en paramètre, renverra son indice dans le quadruplet d'état. Par exemple, l'appel `get_index_from('e')`renverra 0 puisque la modalité $e$ se trouve en première position dans le quadruplet. De même, `get_index_from('p')` renverra 3, etc...

Ensuite, nous appelons la fonction `get_action_from` qui, en fonction du signe passé en paramètre, renvoie l'action à appliquer à une modalité. Pour le moment, cette action est une __quantité signée__  à appliquer de façon __additive__ à une modalité. Elle est définie de la façon suivante:

- Si le signe vaut '0' : alors aucune action n'est à appliquer, et `action = 0`;
- Si le signe vaut '+' : alors l'action à appliquer vaut `action = +bump_value`;
- Si le signe vaut '-' : alors l'action à appliquer vaut `action = -bump_value`.

Nous allons donc construire un quadruplet $Q_c=(i_1,a_1,i_2,a_2)$, où $i_1,i_2$ représentent les indices de l'état en cours qui devrons être modifiés par les actions $a_1,a_2$. Ainsi, en initialisant un quadruplet de dimension 4 à zéro, que l'on notera $Q_0=[0,0,0,0]$ (il s'agit d'une liste de sorte que les coordonnées puissent être modifiées), il suffira alors de construire le vecteur de chocs à appliquer à l'état en cours de la façon suivante:

$$
\begin{align*}
Q_0[Q_c[0]]&\textrm{ += } Q_c[1]\\
Q_0[Q_c[2]]&\textrm{ += } Q_c[3]
\end{align*}
$$

Illustrons tout ceci sur un exemple. Supposons l'appel suivant : `generate_action(("e+", "p-"), 1)`. Voici les différentes productions du corps de la fonction :

- Première partie :
 ```python
    letter_p, sign_p = rule[0][0], rule[0][1] # letter_p = "e" et sign_p = "+"
    letter_c, sign_c = rule[1][0], rule[1][1] # letter_c = "p" et sign_c = "-"
```
- Seconde partie :
```python
    to_do = (
        get_index_from(letter_p),
        get_action_from(sign_p),
        get_index_from(letter_c),
        get_action_from(sign_c),
    ) # Ici, to_do = (0,1,3,-1)
```
- Troisième partie :
 ```python
    state_shift = [0] * 4               # state_shift = [0,0,0,0]
    
    state_shift[to_do[0]] += to_do[1]   # state_shift = [1, 0, 0,  0]
    state_shift[to_do[2]] += to_do[3]   # state_shift = [1, 0, 0, -1]

  ```

Finalement, la fonction renvoie le vecteur de choc $c_t=[1, 0, 0, -1]$ qui sera appliqué à l'état en cours. Supposons que l'état en cours $s_t$ vaille $s_t=[2,2,3,1]$, alors le nouvel état au temps $t+1$ sera $s_{t+1}=s_t+c_t=[3,2,3,0]$

 ```python
def generate_action(rule, bump_value):
    def get_index_from(state_letter):
        idx = 0
        match state_letter:
            case "e":
                idx = 0
            case "s":
                idx = 1
            case "t":
                idx = 2
            case "p":
                idx = 3
        return idx

    def get_action_from(sign_letter):
        action = 0
        match sign_letter:
            case "0":
                action = 0
            case "+":
                action = bump_value
            case "-":
                action = -bump_value
        return action

    letter_p, sign_p = rule[0][0], rule[0][1]
    letter_c, sign_c = rule[1][0], rule[1][1]

    to_do = (
        get_index_from(letter_p),
        get_action_from(sign_p),
        get_index_from(letter_c),
        get_action_from(sign_c),
    )

    state_shift = [0] * 4

    state_shift[to_do[0]] += to_do[1]
    state_shift[to_do[2]] += to_do[3]

    return state_shift
  ```

Dans la mesure où l'on considère que les modalités d'un état varient dans des intervalles de valeurs de type $[[ m^-;m^+]\]$, où $m^-$ et $m^+$ représentent les valeurs minimale et maximale respectivement que peut prendre la modalité $m$, on se propose de borner les valeurs d'une modalité dans cet intervalle. Mathématiquement, cela revient à définir la fonction $\phi_{m^-,m^+}:x\in\mathbb{R}\mapsto \max(m^-,\min(m^+, x))$, puis à l'appliquer sur la valeur d'une modalité d'un état. Dans notre code, cette fonction est définie ci-dessous. Par conséquent, on écrit la fonction suivante : 

```python
def bound_values(a, b, x):
    return np.maximum(a, np.minimum(b, x))
```

Enfin, nous définissons une fonction `update_state` qui gère simplement l'addition de deux vecteurs. Cela permet de modifier un état en lui additionnant un vecteur de choc, comme expliqué plus haut. Notons que nous appliquons sur chaque coordonnée du nouvel état la fonction `bound_value` afin de s'assurer que les valeurs des modalités appartiennent à des intervalles de valeurs admissibles. Dans notre cas, nous faisons le choix de définir un état en modalités exprimées en "probabilités". C'est la raison pour laquelle nous bornons nos valeurs entre 0 et 1.

```python
def update_state(state, action):
    tmp = list(sum(xy) for xy in zip(state, action))
    return list(map(lambda x: bound_values(0, 1, x), tmp))
```

## Boucle principale de simulation

A présent, l'idée est de générer un certain nombre de simulations pour observer comment évolue un état initialialement fixé à certaines valeurs de modalité. Il y aura beaucoup à dire du code ci-dessous dans la version finale du document, et nous nous proposons, dans un premier temps, d'exposer les graphiques des évolutions des modalités dans le temps (horizon 60 jours, soit deux mois) et pour chaque simulation (nombre de simulation fixé à 10000).

A cet effet, nous fixons les hypothèses suivantes :

- L'état initial est toujours le même pour toutes les simulations. On le choisi de sorte que :
    -  l'ennui, la solitude, le temps d'écran soient minimaux;
    -  La productivité soit maximale.

Compte tenu des règles définies, nous conjecturons que les trois premières modalités risquent d'augmenter, alors que la quatrième risque de baiser. Ceci est une intuition qui correspond au fait que la productivité peut potentiellement se faire "pervetir" par les autres facteurs.

Nous n'avons pas encore tester d'autres hypothèses comme le fait de faire varier l'amplitude des chocs, de rendre ces derniers asymétriques (avec des valeur non égales en valeur absolue), de tester l'impact de chocs multiplicatifs et non additifs, ainsi que bien d'autres idées que nous exposerons ultérieurement.

```python
all_simulations = []
NB_DAYS = 30 * 2
NB_SIMULATION = 10_000

for _s in tqdm(range(NB_SIMULATION)):
    current_state_values = np.array([0.001, 0.001, 0.001, 0.80])
    current_state_values = current_state_values / sum(current_state_values)
    states = []
    for _p in range(NB_DAYS):
        state_i = generate_state()
        generated_rules = generate_rules_from_state(state_i)

        for rule in generated_rules:
            if rule in global_rules:
                ga = generate_action(rule, 1 / (NB_DAYS - 1))
                current_state_values = update_state(current_state_values, ga)
        states.append(current_state_values)
    all_simulations.append(states)

simulations = np.array(all_simulations)

# On trace les graphes :

fix, ax = plt.subplots(2, 2, figsize=(12, 7))
idx = 0
ax[0, 0].plot(simulations[:, :, idx].T, color=MY_BLUE2, alpha=0.3)
ax[0, 0].plot(simulations[:, :, idx].mean(axis=0), lw=3, color=MY_MAROON)
ax[0, 0].set_title("Var E")

idx = 1
ax[0, 1].plot(simulations[:, :, idx].T, color=MY_BLUE2, alpha=0.3)
ax[0, 1].plot(simulations[:, :, idx].mean(axis=0), lw=3, color=MY_MAROON)
ax[0, 1].set_title("Var S")

idx = 2
ax[1, 0].plot(simulations[:, :, idx].T, color=MY_BLUE2, alpha=0.3)
ax[1, 0].plot(simulations[:, :, idx].mean(axis=0), lw=3, color=MY_MAROON)
ax[1, 0].set_title("Var T")

idx = 3
ax[1, 1].plot(simulations[:, :, idx].T, color=MY_BLUE2, alpha=0.3)
ax[1, 1].plot(simulations[:, :, idx].mean(axis=0), lw=3, color=MY_MAROON)
ax[1, 1].set_title("Var P")

plt.show()
```

Les graphes générés sont les suivants : 

![Image 1](/images/c1.png)

Sans proposer d'analyses fines, on observe que nos intuitions se confirment par les graphiques ci-dessus. Les courbes épaisses de couleur foncée correspondent aux trajectoires moyennes des modalités conditionnellement aux 10000 simulations. On observe assez clairement les tendances anticipées.

## Partie 2 -- Génération asymétrique

Dans le cadre de l'amélioration de notre modèle dynamique, nous avons introduit un choix délibéré d'asymétrie dans l'application des vecteurs de choc. Cette décision s'appuie sur des considérations pragmatiques reflétant la complexité des comportements humains face aux changements technologiques et leurs répercussions sur la productivité. Notamment, il est reconnu que les variations de productivité ne suivent pas un modèle linéaire en réponse aux fluctuations du temps d'écran. Il est souvent plus ardu d'accroître la productivité par la diminution du temps d'écran que de constater une dégradation de celle-ci due à son augmentation. Cette observation est d'autant plus pertinente lorsque les alternatives au temps d'écran sont moins immédiatement gratifiantes ou moins stimulantes intellectuellement.
De surcroît, les habitudes associées à l'utilisation des écrans s'avèrent résistantes aux modifications. Diminuer le temps d'interaction avec les écrans exige typiquement un effort conséquent et une volonté affirmée, impliquant le développement de nouvelles routines et la recherche d'activités substitutives satisfaisantes. Ces aspects soulignent la nécessité d'approches asymétriques dans la modulation des chocs, pour produire un modèle qui soit non seulement descriptif mais aussi prédictif des tendances comportementales en réponse aux interventions visant à réguler le temps d'écran.

Nous allons procéder à une réévaluation des fonctions préalablement introduites en adoptant une approche asymétrique dans la modélisation des réactions comportementales. L'objectif est d'effectuer une simulation sur une période de soixante jours, au terme de laquelle seront sélectionnées les règles qui conduisent à un temps d'écran n'excédant pas 45% de l'activité globale. Dans les deux mois subséquents, l'individu simulé sera soumis à un processus d'auto-régulation visant à maintenir ou à atteindre un seuil d'utilisation d'écran inférieur ou égal à 45%. Il est essentiel de reconnaître la complexité inhérente au comportement humain, lequel ne saurait être assimilé à des schémas mécaniques ou automatisés. Par conséquent, notre modèle intègrera une composante d'aléatoire dans la génération des règles, combinée à une sélection stratégique de règles ayant démontré leur efficacité pour réduire le temps d'écran dans les limites souhaitées.

```python
def generate_asymmetric_action(rule, bump_value_increase, bump_value_decrease):
    def get_index_from(state_letter):
        return {"e": 0, "s": 1, "t": 2, "p": 3}.get(state_letter, -1)

    def get_action_from(sign_letter, bump_up, bump_down):
        action = 0
        if sign_letter == "+":
            action = bump_up
        elif sign_letter == "-":
            action = -bump_down
        return action

    # Initialisation du vecteur d'action avec des zéros
    action_vector = [0, 0, 0, 0]

    # Calcul des actions pour chaque composant de la règle
    for letter, sign in rule:
        idx = get_index_from(letter)
        action_vector[idx] += get_action_from(sign, bump_value_increase, bump_value_decrease)

    return action_vector
```

### Première simulation


Nous effectuons notre première simulation asymétrique sur 60 jours. Expliquons tout de même certains points : 

L'état initial de l'individu est représenté par un vecteur `initial_state` contenant les valeurs initiales des variables d'état. Pour garantir la cohérence des manipulations et des comparaisons ultérieures, une normalisation est appliquée pour que la somme des composantes du vecteur soit unitaire, plaçant ainsi chaque variable sur une échelle relative qui traduit sa proportion dans le cadre global de l'état de l'individu. Cette normalisation facilite une interprétation en termes de pourcentages, permettant ainsi une compréhension plus claire et directe des données simulées.


L'objectif de cette phase de simulation est de recenser et de consigner les règles d'action, dénotées par `effective_rules`, qui conduisent à un temps d'écran inférieur ou égal à 45% de la distribution temporelle totale de l'individu. L'identification de ces règles efficaces est cruciale pour formuler des stratégies d'intervention adaptatives dans les phases subséquentes de la simulation. Ces règles seront évaluées non seulement pour leur efficacité immédiate mais aussi pour leur pertinence dans le cadre d'une auto-régulation à long terme.

De plus, `bump_increase` est le montant ajouté à une variable lorsqu'un changement positif est effectué. Il est défini comme étant relativement petit pour représenter une augmentation graduelle ou un effort plus important pour améliorer, par exemple, la productivité ou réduire l'ennui. Tandis que `bump_decrease` est le montant soustrait d'une variable lorsqu'un changement négatif est requis. Il est défini comme étant plus grand pour représenter une tendance à la baisse plus facile ou plus rapide, par exemple, une diminution de la productivité ou une augmentation de l'ennui avec une augmentation du temps d'écran.

```python
# Paramètres de la simulation
NB_DAYS = 60
initial_state = np.array([0.01, 0.01, 0.7, 0.7])
initial_state /= sum(initial_state)  # Normalisation pour que la somme soit 1

bump_increase = 1 / (NB_DAYS - 1)  # Plus petit pour les augmentations
bump_decrease = 2 / (NB_DAYS - 1)  # Plus grand pour les diminutions

results = []
rules_applied = []
effective_rules = []

for day in tqdm(range(NB_DAYS)):
    state = generate_state()
    rules = generate_rules_from_state(state)
    action_vector = np.zeros(4)

    for rule in rules:
        if rule in global_rules:
            action_value = bump_increase if "+" in rule else bump_decrease
            action = generate_asymmetric_action(rule, action_value, action_value)
            action_vector += action

    new_state = update_state(initial_state, action_vector)
    results.append(new_state)
    initial_state = new_state
    rules_applied.extend([(rule, new_state[2]) for rule in rules])  # Stocker la règle et le temps d'écran après application

# Identifier les règles qui ont maintenu le temps d'écran inférieur ou égal à 0.45
for rule, screen_time in rules_applied:
    if screen_time <= 0.45:
        effective_rules.append(rule)

effective_rules = list(set(effective_rules))  # Supprimer les doublons
print("Règles efficaces qui maintiennent le temps d'écran sous 45%:", effective_rules)
```

Notons que les règles efficaces obtenues peuveut différées car la génération de ces règles restent aléatoire. On graphe ce que donne cette première simulation pour l'ensemble des variables d'états : 

![Image 1](/images/c2.png)

### Deuxième simulation 

Dans le cadre de notre étude longitudinale sur l'efficacité des interventions comportementales, une deuxième phase de simulation de 60 jours a été initiée. Cette phase est basée sur la présupposition que maintenir un temps d'écran inférieur ou égal à 45% constitue un seuil de régulation stable et souhaitable pour l'individu. L'objectif de cette simulation est de permettre à l'individu de réguler activement son temps d'écran en s'appuyant sur un ensemble de règles éprouvées, déterminées lors de la phase précédente de la simulation comme étant efficaces pour atteindre et maintenir ce seuil.

Pour ajouter une dimension de réalisme et d'adaptabilité au modèle, la simulation intègre également une composante d'aléatoire dans la sélection des règles à appliquer (règles selon nos hypothèses cf. `global_rules`). Cela permet de simuler un comportement plus dynamique et moins prédictible, reflétant ainsi plus fidèlement la variabilité et la complexité des comportements humains dans des conditions réelles. Cette approche vise à évaluer non seulement la capacité de l'individu à se conformer aux régulations proposées mais aussi son aptitude à intégrer de nouvelles stratégies comportementales qui peuvent émerger de manière spontanée ou en réponse à des changements contextuels.

```python
NB_DAYS_NEW_SIMULATION = 60
initial_state_new = np.array([0.01, 0.01, 0.7, 0.7])
initial_state_new /= sum(initial_state_new)  # Normalisation

bump_increase_new = 1 / (NB_DAYS_NEW_SIMULATION - 1)
bump_decrease_new = 2 / (NB_DAYS_NEW_SIMULATION - 1)

# Simulation en utilisant les règles efficaces et exploration de nouvelles règles
results_new = []
for day in tqdm(range(NB_DAYS_NEW_SIMULATION)):
    state_new = generate_state()
    rules_new = generate_rules_from_state(state_new)
    action_vector_new = np.zeros(4)

    for rule_new in rules_new:
        if rule_new in global_rules:
            # Appliquer les règles efficaces pour réguler et explorer de nouvelles règles
            if rule_new in effective_rules or np.random.rand() < 0.5:  # 50% de chance d'essayer de nouvelles règles
                action_value_new = bump_increase_new if "+" in rule_new else bump_decrease_new
                action_new = generate_asymmetric_action(rule_new, action_value_new, action_value_new)
                print(action_new)
                action_vector_new += action_new

    new_state_new = update_state(initial_state_new, action_vector_new)
    results_new.append(new_state_new)
    initial_state_new = new_state_new

# Graphique des résultats pour visualiser l'efficacité
results_new = np.array(results_new)
```

On affiche nos résultats : 

```python
plt.figure(figsize=(12, 8))
plt.plot(results_new[:, 2], label='Temps d\'écran (t)')
plt.xlabel('Jours')
plt.ylabel('Proportion du temps d\'écran')
plt.title('Évolution du Temps d\'Écran dans la Nouvelle Simulation')
plt.axhline(y=0.45, color='r', linestyle='--', label='Seuil de 45\%')
plt.legend()
plt.show()
```

On obtient alors l'image suivante : 

![Image 1](/images/c3.png)

On remarque que notre individu arrive à se réguler dans le temps en ayant appris de ses erreurs du passé. 

Par ailleurs, pour obtenir l'ensemble des variables d'états sur cette simulation on écrit : 

```python
days = np.arange(1, NB_DAYS_NEW_SIMULATION + 1)
results_new = np.array(results_new)

# Créer le graphique pour chaque variable de l'état
plt.figure(figsize=(12, 8))
plt.plot(days, results_new[:, 0], label='Ennui (e)', marker='o')
plt.plot(days, results_new[:, 1], label='Solitude (s)', marker='o')
plt.plot(days, results_new[:, 2], label='Temps d\'écran (t)', marker='o')
plt.plot(days, results_new[:, 3], label='Productivité (p)', marker='o')

# Configuration du graphique
plt.title('Évolution des Variables sur 60 Jours')
plt.xlabel('Jour')
plt.ylabel('Valeur des variables')
plt.legend()
plt.grid(True)
plt.show()
```

![Image 1](/images/c4.png)

Notons que la courbe en vert est la même que celle obtenue plus haut.

### Troisième partie -- Généralisation

Dans cette section, nous étendons les méthodologies appliquées dans la deuxième partie du projet en encapsulant le processus de simulation dans une fonction nommée `run_simulation`. Cette démarche vise à réaliser 100 simulations pour chaque individu parmi un ensemble de 300, sur une période de 60 jours. Pour optimiser l'efficacité computationnelle de cette tâche volumineuse, nous utilisons la bibliothèque `multiprocessing`. Cette bibliothèque exploite les capacités multi-processeurs de l'ordinateur, permettant une exécution parallèle des calculs. L'adoption de cette approche est cruciale pour minimiser les risques de latence ou de surcharge du système, assurant ainsi une gestion fluide et efficace des simulations de grande envergure.

On importe la bibliothèque `multiprocessing` :

```python
from multiprocessing import Pool
```

On relance notre simulation sur nos groupes d'individus : 

```python
from multiprocessing import Pool

def run_simulation(sim_id):
    # Paramètres de simulation pour un individu
    NB_DAYS = 60
    initial_state = np.random.rand(4)
    initial_state /= initial_state.sum()  # Normalisation

    bump_increase = 1 / (NB_DAYS - 1)
    bump_decrease = 2 / (NB_DAYS - 1)
    
    results = []
    for day in range(NB_DAYS):
        state = generate_state()
        rules = generate_rules_from_state(state)
        action_vector = np.zeros(4)

        for rule in rules:
            if rule in global_rules:
                if rule in effective_rules or np.random.rand() < 0.5:
                    action_value = bump_increase if '+' in rule else bump_decrease
                    action = generate_asymmetric_action(rule, action_value, action_value)
                    action_vector += action

        new_state = update_state(initial_state, action_vector)
        results.append(new_state)
        initial_state = new_state  # Mise à jour de l'état initial pour le jour suivant

    return np.array(results)

# Paramètres pour les simulations
NB_SIMULATIONS = 100
NB_INDIVIDUALS = 300
NB_DAYS = 60

# Utiliser multiprocessing pour exécuter les simulations
with Pool(processes=8) as pool:
    all_results = list(tqdm(pool.imap(run_simulation, range(NB_SIMULATIONS * NB_INDIVIDUALS)), total=NB_SIMULATIONS * NB_INDIVIDUALS))
    all_results = np.array(all_results).reshape(NB_INDIVIDUALS, NB_SIMULATIONS, NB_DAYS, 4)
```

Puis on visualise nos courbes : 

```python
# Calculer la moyenne sur toutes les simulations et tous les individus pour chaque jour
mean_results = all_results.mean(axis=(0, 1))

# Créer le graphique pour chaque variable de l'état
plt.figure(figsize=(12, 8))
days = np.arange(1, NB_DAYS + 1)

plt.plot(days, mean_results[:, 0], label='Ennui (e)', marker='o')
plt.plot(days, mean_results[:, 1], label='Solitude (s)', marker='o')
plt.plot(days, mean_results[:, 2], label='Temps d’écran (t)', marker='o')
plt.plot(days, mean_results[:, 3], label='Productivité (p)', marker='o')

# Configuration du graphique
plt.title('Évolution Moyenne des Variables sur 60 Jours pour 300 Individus avec 100 Simulations Chacun')
plt.xlabel('Jour')
plt.ylabel('Valeur Moyenne des Variables')
plt.legend()
plt.grid(True)
plt.show()
```

![Image 1](/images/c5.png)

## Conclusion 

Pour conclure cet exposé, il est manifeste que nos hypothèses préliminaires sur la diminution potentielle du temps d'écran se vérifient de manière notable. Bien que la sélection des règles soit effectuée de manière aléatoire, le critère de filtrage qui exige que l'individu régule son temps d'écran pour ne pas dépasser 45% s'avère efficace. Cette régulation s'observe même si les profils spécifiques des courbes peuvent varier en raison du caractère aléatoire des règles appliquées. En réitérant notre simulation, nous anticipons que, malgré la variabilité interindividuelle, la tendance générale à la baisse du temps d'écran se maintiendra à travers différents groupes d'individus. Cette consistance souligne la robustesse de notre approche modélisatrice face aux variations intra et intergroupes.

De plus, il aurait été envisageable de concevoir une fonction destinée à examiner les règles établies initialement afin de générer des règles plus élaborées, ce qui aurait permis des simulations d'une plus grande précision. Toutefois, une telle entreprise relève du domaine de l'intelligence artificielle et, compte tenu du temps limité alloué à la réalisation de ce projet, nous avons préféré éviter le risque de présenter un projet inachevé.

# Remerciements

Nous tenons à exprimer notre profonde gratitude à notre professeur, Monsieur Amoussou Manuel, pour son encadrement rigoureux et continu tout au long de notre projet de recherche. Nous adressons également nos remerciements aux encadrants qui ont rendu possible la réalisation de recherches scientifiques de qualité. Enfin, nous sommes reconnaissants à l'ensemble des personnes qui ont participé à notre sondage, permettant ainsi l'établissement de nos règles initiales.