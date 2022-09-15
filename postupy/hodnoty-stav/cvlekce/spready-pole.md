---
title: Jednoduché spready polí
demand: 2
---

Všechny následující úkoly dělejte v konzoli. Na začátku si připravte cvičné pole

```js
> const names = ['jana', 'pavel', 'eva', 'jitka', 'radek', 'zuzka', 'ondra']
```

Všechny následující operace proveďte jako immutable

1. Přidejte na konec pole hodnotu `'hanka'`.
1. Přidejte na začátek pole hodnotu `'romana'`.
1. Vytvořte čistou kopii pole.
1. Odstraňte poslední prvek pole.
1. Odstraňte z pole hodnotu na třetím indexu.

---solution
```js
const names = ["jana", "pavel", "eva", "jitka", "radek", "zuzka", "ondra"];

const a = [...names, "hanka"]
const b = ["romana", ...names]
const c = [...names]
const d = [...names].pop()
const e = [...names]
e.splice(3, 1)

console.log(a, b, c, d, e);
```
