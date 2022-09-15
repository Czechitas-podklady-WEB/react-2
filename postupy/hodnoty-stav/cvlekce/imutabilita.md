---
title: Imutabilita
demand: 3
---

Ve všech následujících úkolech vytvořte vlastní funkcí dle zadání. Všechny funkce nechť zachovají do funkce předávanou hodnotu. Bude tedy možné je použít jako operace nad immutable hodnotami.

1. Vytvořte funkci `reversed`, která obrátí pořadí prvků v poli.
1. Vytvořte funkci `remove`, která obdrží pole a index. Funkce smaže prvek na zadaném indexu.
1. Vytvořte funkci `swap`, která obdrží pole a dva indexy. Funkce prohodí prvky na těchto indexech.

---solution
```js
const reversed = (input) => {
  return [...input].reverse();
};

const remove = (array, index) => {
  const result = [...array];
  result.splice(index, 1);
  return result;
};

const swap = (array, a, b) => {
  const result = [...array];
  result[a] = array[b];
  result[b] = array[a];
  return result;
};

// otestování
const mojePole = [10, 11, 12, 13, 14, 15];

console.log("reversed", reversed(mojePole), "očekáváno", [15, 14, 13, 12, 11, 10]);
console.log("Je mojePole nezměněné?", mojePole);

console.log("remove", remove(mojePole, 3), "očekáváno", [10, 11, 12, 14, 15]);
console.log("Je mojePole nezměněné?", mojePole);

console.log("swap", swap(mojePole, 2, 4), "očekáváno", [10, 11, 14, 13, 12, 15]);
console.log("Je mojePole nezměněné?", mojePole);
```
