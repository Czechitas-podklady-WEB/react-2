---
title: Jednoduché spready objektů
demand: 2
---

Všechny následující úkoly dělejte v konzoli. Na začátku si připravte cvičný objekt:

```js
> const ticket = { from: 'Praha', to: 'Lisabon', currency: 'EUR', price: 115 }
```

Všechny následující operace proveďte jako immutable

1. Přidejte do objektu vlastnot `duration` s hodnotu `2h`.
1. Změňte vlastnost `price` na hodnotu 130.

--- solution
const ticket = { from: "Praha", to: "Lisabon", currency: "EUR", price: 115 };
const a = { ...ticket, duration: "2h" }
const b = { ...ticket, price: 130 }

console.log(a, b)
