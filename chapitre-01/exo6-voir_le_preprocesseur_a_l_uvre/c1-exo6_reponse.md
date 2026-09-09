# C1-Exo5 — Que fait vraiment le préprocesseur ?

> `clang++` indisponible ici, remplacé par `g++` (même préprocesseur GNU/Clang-compatible
> en pratique ; le nombre exact de lignes varie légèrement selon le compilateur et sa
> version, mais l'ordre de grandeur et l'explication sont identiques).

## Fichier source (6 lignes écrites)

```cpp
#include <iostream>
int main(int argc, char* argv[]) {
    std::cout << "NGIATE KAMNANG INGRID\n";
    std::cout << "YAOUNDE";
    return 0;
}
```

## Commande

```bash
clang++ -E bonjour.cpp > sortie.txt
wc -l sortie.txt
```

## Résultat obtenu

```
35880 sortie.txt
```

**6 lignes écrites → 35880 lignes produites.**

## Explication de l'écart

`-E` arrête la chaîne après l'étape 1, celle du **préprocesseur**. Cette étape ne comprend
pas le C++ : elle se contente de faire des remplacements textuels purement mécaniques,
avant que la moindre analyse de syntaxe n'ait lieu.

La ligne `#include <iostream>` est justement une instruction pour le préprocesseur : elle
lui ordonne de **copier-coller intégralement** le contenu du fichier `iostream`, qui à son
tour inclut lui-même d'autres en-têtes internes de la bibliothèque standard
(`bits/c++config.h`, `bits/requires_hosted.h`, etc.), et ainsi de suite en cascade.

Résultat : `sortie.txt` ne contient presque aucune ligne « inventée » par nous — quasiment
tout vient du contenu déclaratif de la bibliothèque standard C++, qui est très volumineux
(templates, déclarations de classes, macros de configuration...), même si l'on n'utilise
en pratique qu'une infime fraction de tout cela (`std::cout` et `std::endl`).

Nos 6 lignes ne représentent donc qu'une portion infime — moins de 0,02 % — du texte que le
compilateur doit réellement analyser à l'étape suivante. Un simple `#include`, en apparence
anodin, déclenche l'ingestion de dizaines de milliers de lignes de déclarations.

## Auteur

NGIATE KAMNANG INGRID