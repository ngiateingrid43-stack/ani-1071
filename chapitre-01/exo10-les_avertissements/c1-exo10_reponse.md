# C1-Exo10 — Avertissement vs erreur (`-Wall -Wextra`)

## Test

```cpp
int main(){
    int x = 42;  // jamais utilisée
    return 0;
}
```

```
clang++ -std=c++17 -Wall -Wextra inutilisee.cpp -o programme
```

**Résultat :**
```
warning: unused variable 'x' [-Wunused-variable]
```
→ Exécutable produit, programme fonctionne, code de sortie 0.

Contre-exemple (point-virgule manquant) :
```
error: expected ',' or ';' before 'return'
```
→ Aucun exécutable produit.

## Différence

| | Avertissement | Erreur |
|---|---|---|
| Bloque la compilation | Non | Oui |
| Cause | Code valide mais suspect | Code qui viole la grammaire du C++ |

**L'erreur arrête la compilation** parce que le compilateur ne sait pas quoi générer :
le code n'a aucun sens défini par la norme.

**L'avertissement existe sans bloquer** parce que le code, lui, est valide — le
compilateur sait quoi générer — mais la construction ressemble souvent à un oubli.
Il alerte pour laisser le développeur juger, sans lui imposer une correction.

## Auteur

NGIATE KAMNANG INGRID