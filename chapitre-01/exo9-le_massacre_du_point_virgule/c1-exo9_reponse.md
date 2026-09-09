# C1-Exo9 - Le nassacre du point virgule

## Test1 

```cpp
#include <iostream>
int main(int argc, char* argv[]) {
    // Affichage de mon nom sur une ligne
    std::cout << "NGIATE KAMNANG INGRID" << std::endl
    // Affichage de ma ville sur une ligne
    std::cout << "YAOUNDE"
    return 0
}
```
**Commande de compilation**

```
g++ c1-exo9_main.cpp -o programme
```

**Resultalt 1:**
```
Un message d'erreure
```
```
c1-exo9_main.cpp:4:54: error: expected ';' before 'std'
    4 |     std::cout << "NGIATE KAMNANG INGRID" << std::endl
      |                                                                                                            ^
      |                                                                                                            ;
    5 |     // Affichage de ma ville sur une ligne
    6 |     std::cout << "YAOUNDE"
```
## Test2 

```cpp
#include <iostream>
int main(int argc, char* argv[]) {
    // Affichage de mon nom sur une ligne
    std::cout << "NGIATE KAMNANG INGRID" << std::endl;
    // Affichage de ma ville sur une ligne
    std::cout << "YAOUNDE"
    return 0
}
```
**Commande de compilation**

```
g++ c1-exo9_main.cpp -o programme
```

**Resultalt 2:**
```
Un message d'erreure
```
```
c1-exo9_main.cpp:6:27: error: expected ';' before 'return'
    6 |     std::cout << "YAOUNDE"
      |                           ^
      |                           ;
    7 |     return 0
      |     ~~~~~~                 
```
```
Un message d'erreure a disparus celui de

c1-exo9_main.cpp:4:54: error: expected ';' before 'std'
    4 |     std::cout << "NGIATE KAMNANG INGRID" << std::endl
      |                                                      ^
      |                                                      ;
    5 |     // Affichage de ma ville sur une ligne
    6 |     std::cout << "YAOUNDE"
      |     ~~~                                               
```

## Auteur

NGIATE KAMNANG INGRID