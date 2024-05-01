---
title: Compte-rendu
#author: evadoys
date: 2024-01-05 14:10:00 +0800
#categories: [Blogging, Tutorial]
#tags: [writing]
render_with_liquid: false
math: true
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

**Problématique** : Comment le temps d’écran influence-t-il au quotidien notre productivité,
solitude et ennui ?

**Hypothèse principale** : Le temps d'écran quotidien a une influence significative sur les niveaux de productivité, de solitude et d'ennui des individus. Une réduction ciblée et régulée du temps passé devant les écrans améliorera ces aspects.

**Hypothèses secondaires**:

- Les individus peuvent adapter leur comportement en fonction des règles imposées pour réguler le temps d'écran.
- Les interventions basées sur des règles dynamiques sont plus efficaces pour réduire le temps d'écran que des interventions statiques ou non personnalisées.
- La réaction à la régulation du temps d'écran varie significativement entre les individus, influencée par des facteurs personnels comme les habitudes préexistantes et la disposition à changer.

**Objectifs** : 
- Développer un modèle dynamique qui simule l'impact de différentes règles de régulation du temps d'écran sur la productivité, la solitude et l'ennui.
- Identifier des règles efficaces pour maintenir ou réduire le temps d'écran à un seuil qui favorise une amélioration de la productivité et une réduction de la solitude et de l'ennui.
- Tester la robustesse du modèle en effectuant des simulations sur différents groupes d'individus pour évaluer la variabilité des réponses.

**Critère(s) d’évaluation**:
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
- Jour 1 : L'individu commence à un état élevé
- Jour 2 : L'automate applique $(+0,1, -0.05, -0.2, +0.15)$ qui pourrait le mener à l'état Moyen selon la fonction $\delta$
- Jour 3 : 

