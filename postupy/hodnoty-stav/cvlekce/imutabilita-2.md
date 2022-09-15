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
1. Vytvořte funkci `rotate`, která obdrží pole a kladné celé číslo. Funkce odrotuje pole doprava o zadaný počet kroků. 
   Příklad:
   ```js
   > rotate([10, 11, 12, 13, 14, 15], 4)
   [12, 13, 14, 15, 10, 11]
   ```
1. Vytvořte funkci `shuffle`, která náhodně zamíchá prvky v poli.

---solution

```js
const drag = (array, from, to) => {
  const result = [...array];
  result.splice(from, 1);
  result.splice(to, 0, array[from]);
  return result;
};

const rotate = (array, steps) => {
  const result = [...array];
  const tail = result.splice(-steps);
  result.unshift(...tail);
  return result;
};

//trochu kryptická varianta, ale také funguje
const rotate2 = (array, steps) => {
  const tmp = [...array];
  return [...tmp.splice(-steps), ...tmp];
};

const shuffle = (array) => {
  const result = [...array];
  result.sort(() => Math.random() - 0.5);
  return result;
};

//ověření řešení

const mojePole = [10, 11, 12, 13, 14, 15];

console.log("drag", drag(mojePole, 4, 1), "očekáváno", [10, 14, 11, 12, 13, 15]);
console.log("Je mojePole nezměněné?", mojePole);

console.log("rotate", rotate(mojePole, 4), "očekáváno", [12, 13, 14, 15, 10, 11]);
console.log("Je mojePole nezměněné?", mojePole);

console.log("rotate2", rotate2(mojePole, 4), "očekáváno", [12, 13, 14, 15, 10, 11]);
console.log("Je mojePole nezměněné?", mojePole);

console.log("shuffle", shuffle(mojePole));
console.log("shuffle", shuffle(mojePole));
console.log("Je mojePole nezměněné?", mojePole);
```
