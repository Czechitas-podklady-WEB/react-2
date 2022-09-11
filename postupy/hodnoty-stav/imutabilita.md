## Imutabilita

Důvod pro podivné chování odhalené v předchozí sekci spočívá v tom, že v JavaScriptu obash řetězců nelze měnit, kdežto u polí to možné je. Není problém napsat

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

Tím jsme však vyrobili zcela **nový** řetězec `'petra'`. V proměnné `name` je pořád obsažena stará hodnota `petr`. Pokud nějaká hodnota nejde změnit, říkáme odborně, že je :em[immutable]. Řetězce jsou vždy immutable a to jak v JavaScriptu tak ve většině ostatních jazyků.

Protože řetězce nejde měnit, představujeme si, že řetězec `'petr'` je pouze jeden. Můžeme jej použít na deseti místech, a pořád to bude tentýž `'petr'`. Všimněte si, že stejným způsobem fungují především čísla. Například číslo 25 logicky existuje v celém vesmíru pouze jedno. Nemáme více různých čísel 25. Kdyby existovalo více různých čísel 25, následující porovnání by nefungovalo, protože bychom nevědli, se kterým číslem 25 vlastně porovnáváme. 

```js
> const age = 25
> age === 25
true
```

Díky tomu, že řetězce jsou stejně jako čísla immutable, funguje pak stejným způsboem i následující porovnání. 

```js
> const name = 'petr'
> name === 'petr'
true
```

Na druhou stranu, pole a objekty jsou v JavaScriptu :em[mutable]. Polí `[1, 2, 3]` může skutečně existovat více. Proto následující porovnání nefunguje.

```js
> const x = [1, 2, 3];
> x === [1, 2, 3]
false
```

Pokaždé, když použijeme hodnotu `[1, 2, 3]`, JavaScript vytvoří úplně nové pole, i když se stejným obsahem. Ve chvíli kdy porovnáváme proměnnou `x`, vytvořili jsme zcela novou hodnotu `[1, 2, 3]`, která už nemá s hodnotou v proměnné nic společného. Ještě lépe to ukáže následující výraz.

```js
> [1, 2, 3] === [1, 2, 3]
false
```
