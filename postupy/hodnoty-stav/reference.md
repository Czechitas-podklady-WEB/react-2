## Reference

Jak už jsme prve zmínili, následující porovnání působí naprosto nevinně. 

```js
> const age = 25
> age === 25
true
```

Tajemství, proč takové porovnání vůbec funguje, je skryté v tom, že číslo 25 čistě logicky existuje v celém vesmíru pouze jedno. Nemám více různých čísel 25. Mezi čísly 24 a 26 je prostě jedno celé číslo a i když jej použíjeme v deseti různých proměnných, tyto proměnné vždycky budou osahovat totéž číslo 25.

Takové úvaha může působit banálně. JavaScript se nás však snaží přesvědčit, že řetězce fungují stejným způsobem jako čísla.

```js
> const name = 'petr'
> name === 'petr'
true
```

Z hlediska JavaScriptu řetězec `'petr'` taky existuje pouze jeden. Pokud do deseti proměnných uložíme řetězec `'petr'`, JavaScript to chápe tak, že jde pořád a tentýž řetězec.

Pole a objekty však fungují jinak. Pokaždé, když použijeme hodnotu `[1, 2, 3]`, JavaScript vytvoří úplně nové pole, i když třeba se stejným obsahem. To je důvod, proč následující porovnání vrátí `false`.

```js
> [1, 2, 3] === [1, 2, 3]
false
```

Důvod pro rozdílné chování řetězců a polí spočívá v tom, že obash řetězců nelze měnit, kdežto u polí to možné je. Není problém napsat

```js
> const x = [1, 2, 3];
> x.push(4)
```

Po této operaci bude proměnná `x` obsahovat hodnotu `[1, 2, 3, 4]`. Řetězec však žádnou takovou operaci nemá. Pokud chceme k řetězci něco přidat, napíšeme prostě

```js
> const name = 'petr';
> 'petr' + 'a'
'petra'
```

Tím jsme však vyrobili zcela **nový** řetězec `'petra'`. V proměnné `name` je pořád obsažena stará hodnota `petr`. 