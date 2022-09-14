---
title: Imutabilita 2
demand: 4
---

Ve všech následujících úkolech vytvořte vlastní funkcí dle zadání. Všechny funkce nechť zachovají do funkce předávanou hodnotu. Bude tedy možné je použít jako operace nad immutable hodnotami.

1. Vytvořte funkci `drag`, která obdrží pole a dva indexy. Funkce přetáhne prvek na prvním indexu na místo označené druhým indexem.
   Příklad:
   ```js
   > drag([10, 11, 12, 13, 14, 15], 4, 1)
   [10, 14, 11, 12, 13, 15]
   ```
1. Vytvořte funkci `shuffle`, která náhodně zamíchá prvky v poli.
