# FCSC 2025 Atomic secable

Mr Performances cherche un algorithme efficace pour évaluer la multiplication sur une courbe elliptique tout en se protégeant des attaques physiques.

Il a opté pour une implémentation de la loi d’addition sur la courbe en respectant le principe d’atomicité. Ce principe repose sur une séquence unique d’opérations pour calculer le doublement d’un point, ou l’addition de deux points différents ; ce qui assure une très bonne protection contre les attaques par analyse de temps d’exécution ou même de la forme de la trace de fuite (par canaux auxiliaires). Cette protection est en effet nécessaire, puisque la distinction de l’opération effectuée (doublement ou addition) permet de retrouver de l’information sur les bits du scalaire, qui est censé rester secret.

En ajoutant des opérations factices, il est assez facile d’obtenir deux séquences identiques pour l’évaluation d’un doublement ou d’une addition de points, mais cela serait au détriment des performances.

Mr Performances, fidèle à ses principes, utilise une séquence sans perte de performances ! Sa séquence est adaptée aux courbes de la forme `y^2 = x^3 + b` et ne contient que 9 multiplications modulaires. Il vous met au défi de casser son implémentation pour la courbe standard secp192k1 (qui a la bonne forme) à l’aide d’une attaque par fautes. Cependant, il a mis en place des contremesures pour limiter une telle attaque :

- les bits du scalaire sont lus deux fois (et comparés) avant de lancer une séquence ;
- les coordonées finales `(x, y)` doivent former un point de la courbe.

Pour cela, il fournit son code assembleur commenté permettant d’évaluer une multiplication avec le générateur sur la courbe. Dans le cadre de l’épreuve, le code est exécuté dans une machine virtuelle et il est possible d’indiquer les instructions à perturber. Il n’y a pas de limite sur le nombre d’instructions à perturber, mais le modèle de faute consiste uniquement en l’attribution d’une valeur aléatoire au registre de destination de l’opération. Par exemple, pour fauter les trois premières instructions il faut entrer, après les chevrons, `0 1 2` (séparés par des espaces).

La documentation de la machine virtuelle est disponible [sur cette page](https://hackropole.fr/fr/doc/vm2025/).

Auteur : Neige

Origine : [Atomic secable](https://hackropole.fr/fr/challenges/hardware/fcsc2025-hardware-atomic-secable/)


## Challenge
[files/assembly.py](files/assembly.py)
[files/atomic-secable.py](files/atomic-secable.py)
[files/crypto_accelerator.py](files/crypto_accelerator.py)
[files/ecdsa_keygen.asm](files/ecdsa_keygen.asm)
[files/machine_faulted.py](files/machine_faulted.py)
[files/machine.py](files/machine.py)

-----------

## Installation manuel
Vous n'utilisez pas l'application **les CTFs de Cyrhades** ? C'est dommage !
Mais voici comment installer ce CTF manuellement :

> git clone https://github.com/Hack-Oeil/fcsc2025-hardware-atomic-secable.git

> cd fcsc2025-hardware-atomic-secable

> docker compose up

-----------

## Sur le site officiel hackropole.fr
> https://hackropole.fr/fr/challenges/hardware/fcsc2025-hardware-atomic-secable/
