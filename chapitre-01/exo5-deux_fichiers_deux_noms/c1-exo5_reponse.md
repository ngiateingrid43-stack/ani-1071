# C1-Exo4 — Un même fichier source, deux noms d'exécutable

## Objectif

Compiler **exactement le même fichier source** (`c1-exo4_main.cpp`) deux fois de suite,
en ne changeant que le nom de l'exécutable produit, pour observer le lien réel entre
nom du fichier source et nom du programme final.

## Code source (inchangé)

```cpp
#include <iostream>

int main(int argc, char* argv[]) {
    // Affichage de mon nom sur une ligne
    std::cout << "NGIATE KAMNANG INGRID\n";
    // Affichage de ma ville sur une ligne
    std::cout << "YAOUNDE";
    return 3;
}
```

## Compilation (deux fois, même source)

```bash
clang++ -std=c++17 -Wall c1-exo4_main.cpp -o essai_un
clang++ -std=c++17 -Wall c1-exo4_main.cpp -o essai_deux
```

Aucune autre différence entre les deux commandes que l'option `-o`.

Les deux fichiers binaires ont exactement la même taille (16360 octets) : ce sont deux
copies indépendantes, mais strictement identiques en contenu mais juste de nom differents.


## Auteur

NGIATE KAMNANG INGRID