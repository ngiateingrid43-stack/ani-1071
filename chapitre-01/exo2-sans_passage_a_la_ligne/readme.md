# C1-Exo1 — Affichage sans retour à la ligne (`\n` retiré)

## Code source

```cpp
#include <iostream>

int main(int argc, char* argv[]) {
    // Affichage de mon nom sur une ligne
    std::cout << "NGIATE KAMNANG INGRID";
    // Affichage de ma ville sur une ligne
    std::cout << "YAOUNDE";
    return 0;
}
```

Par rapport à la version précédente, `std::endl` a été retiré de chaque instruction `std::cout`.

## Compilation

```bash
clang++ -std=c++17 -Wall c1-exo1_main.cpp -o programme
```

## Exécution

```bash
./programme
```

## Sortie obtenue

```
NGIATE KAMNANG INGRIDYAOUNDE
```

(le `$` représente ici l'invite de commande qui revient juste après l'exécution)

## Ce qui change

Dans la version originale, `std::endl` insérait un caractère de fin de ligne (`\n`) après chaque chaîne, en plus de vider le tampon de sortie (*flush*). Résultat : `NGIATE KAMNANG INGRID` et `YAOUNDE` s'affichaient chacun sur leur propre ligne mais sur la meme ligne.

En retirant `std::endl` (donc le `\n`), les deux appels à `std::cout` écrivent leurs chaînes **à la suite, sans aucun caractère de séparation**. Le flux de sortie ne contient donc que :

```
NGIATE KAMNANG INGRIDYAOUNDE
```

sans retour à la ligne final.

## Pourquoi l'invite de commande se colle au texte — et pourquoi ce n'est pas un bug

Le terminal affiche exactement, caractère pour caractère, ce que le programme écrit sur la sortie standard (`stdout`) — rien de plus. Un retour à la ligne à la fin d'un affichage n'est **pas automatique** : c'est le programme qui doit explicitement l'écrire (via `'\n'` ou `std::endl`).

Ce comportement est **normal et documenté** : le terminal n'ajoute jamais de saut de ligne implicite à la sortie d'un programme. C'est une conséquence directe et logique du retrait du `\n`, pas un dysfonctionnement du compilateur, du programme ou du terminal.

## Auteur

NGIATE KAMNANG INGRID