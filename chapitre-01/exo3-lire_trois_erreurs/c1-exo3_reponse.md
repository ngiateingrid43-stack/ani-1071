# C1-Exo3 — Trois fautes introduites une par une (avec printf / cstdio)

> Remarque technique : `clang++` n'étant pas disponible dans mon environnement d'exécution,
> j'ai compilé avec `g++ -std=c++17 -Wall`. Les catégories d'erreurs et les étapes de la
> chaîne de compilation concernées sont identiques avec clang++ ; seul le libellé exact du
> message peut varier légèrement d'un compilateur à l'autre.

## Programme de base (correct)

```cpp
 1  #include <cstdio>
 2
 3  int main(int argc, char* argv[]) {
 4      printf("NGIATE KAMNANG INGRID\n");
 5      printf("YAOUNDE\n");
 6      return 0;
 7  }
```

Compilation de référence (sans faute) : réussit sans erreur ni avertissement.

---

## Faute 1 — Retirer un point-virgule (fin de la ligne 4)

```cpp
4      printf("NGIATE KAMNANG INGRID\n")
5      printf("YAOUNDE\n");
```

**Compilation :**
```
faute1.cpp: In function 'int main(int, char**)':
faute1.cpp:4:38: error: expected ';' before 'printf'
    4 |     printf("NGIATE KAMNANG INGRID\n")
      |                                      ^
      |                                      ;
```

| Élément | Détail |
|---|---|
| Message exact | `error: expected ';' before 'printf'` |
| Ligne signalée | **4** (colonne 38, juste après la parenthèse fermante) |
| Ligne réellement fautive | **4** (c'est bien là que le `;` manque) |
| Étape de la chaîne qui a parlé | **Analyse syntaxique** (parsing) du compilateur — avant même de vérifier le sens du code, il vérifie que la grammaire du langage est respectée |

Ici, exceptionnellement, la ligne signalée correspond exactement à la ligne fautive : le compilateur s'arrête dès qu'il rencontre le jeton `printf` (ligne 5) qu'il n'attendait pas juste après l'expression de la ligne 4, et positionne donc le curseur d'erreur juste avant, en fin de ligne 4.

---

## Faute 2 — Écrire `Printf` au lieu de `printf`

```cpp
4      Printf("NGIATE KAMNANG INGRID\n");
```

**Compilation :**
```
faute2.cpp: In function 'int main(int, char**)':
faute2.cpp:4:5: error: 'Printf' was not declared in this scope; did you mean 'printf'?
    4 |     Printf("NGIATE KAMNANG INGRID\n");
      |     ^~~~~~
      |     printf
```

| Élément | Détail |
|---|---|
| Message exact | `error: 'Printf' was not declared in this scope; did you mean 'printf'?` |
| Ligne signalée | **4** |
| Ligne réellement fautive | **4** (identique — l'erreur de frappe est directement là) |
| Étape de la chaîne qui a parlé | **Analyse sémantique** du compilateur (résolution de noms / recherche d'identificateur). La syntaxe est correcte — `Printf(...)` ressemble à un appel de fonction parfaitement valide — mais aucune fonction de ce nom n'existe dans les symboles connus |

C++ étant sensible à la casse, `Printf` et `printf` sont deux identificateurs totalement distincts. Le compilateur ne « corrige » rien : il propose juste une suggestion (`did you mean`), mais l'erreur est bien réelle.

---

## Faute 3 — Retirer la ligne `#include <cstdio>`

```cpp
1
2  int main(int argc, char* argv[]) {
3      printf("NGIATE KAMNANG INGRID\n");
```

**Compilation :**
```
faute3.cpp: In function 'int main(int, char**)':
faute3.cpp:3:5: error: 'printf' was not declared in this scope
    3 |     printf("NGIATE KAMNANG INGRID\n");
      |     ^~~~~~
faute3.cpp:1:1: note: 'printf' is defined in header '<cstdio>'; did you forget to '#include <cstdio>'?
  +++ |+#include <cstdio>
    1 |
```

| Élément | Détail |
|---|---|
| Message exact | `error: 'printf' was not declared in this scope` (+ note : `'printf' is defined in header '<cstdio>'; did you forget to '#include <cstdio>'?`) |
| Ligne signalée | **3** (le premier usage de `printf`) |
| Ligne réellement fautive | **1** (c'est là que la ligne `#include <cstdio>` a été supprimée et devrait être réinsérée) |
| Étape de la chaîne qui a parlé | **Analyse sémantique** du compilateur, mais la cause réelle est en amont, au niveau du **préprocesseur** |

C'est le cas le plus instructif des trois : la ligne signalée (3) n'est **pas** la ligne réellement fautive (1). Le préprocesseur ne « parle » pas ici, car il n'y a pas de directive invalide à traiter — il ne fait simplement rien à l'endroit où l'`#include` a disparu. Le compilateur ne découvre le problème que plus tard, lorsqu'il rencontre `printf` à la ligne 3 et cherche en vain sa déclaration. Le message d'erreur porte donc sur la conséquence (usage non déclaré), tandis que la cause (absence d'inclusion) est reléguée dans la note — que g++ fournit ici par courtoisie, mais que tous les compilateurs ne donnent pas systématiquement.

---

## Auteur

NGIATE KAMNANG INGRID