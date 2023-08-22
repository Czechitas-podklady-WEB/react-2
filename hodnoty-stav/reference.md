## Reference

Z předchozí částí víme, že řetězce jsou immutable. Možná se ptáte, jaký to má důvod. Díky tomu, že řetězec nejde změnit, můžeme si představovat, že například řetězec `'Petr'` existuje v celém programu pouze jeden. Můžeme jej použít na deseti místech, a pořád to bude tentýž `'Petr'`. 

Výhoda je, že můžeme provádět následující porovnání. 

```js
> const name = 'Petr'
> name === 'Petr'
true
```

Kdyby se při každém použití řetězce `'Petr'` vytvořila nová hodnota tak, jak to funguje u polí nebo objektů, výše uvedené porovnání by nefungovalo a nemohli bychom řetězce mezi sebou porovnávat. To by bylo hodně nešikovné, protože bychom pak nomohli zjišťovat jestli uživatel zadal například správné heslo apod. 

```js
> const password = 'kocka-leze-dirou'
> password === 'kocka-leze-dirou'
false // kdyby řetezce fungovaly jako pole a objekty
```

V podstatě chceme, aby řetězce fungovaly podobně jako čísla. Například číslo 25 také logicky existuje v celém vesmíru pouze jedno. Nemáme více různých čísel 25. Kdyby existovalo více různých čísel 25, opět bychom se dostali do problémů při porovnávání. 

```js
> const age = 25
> age === 25 // Tohle už by byla jiná 25!
false
```

Programátoři začátečníco často slýchávají, že proměnná jsou jako šuplíky nebo krabičky, do kterých se ukládají hodnoty. Tato analogie však právě nyní selhává. Už jsme viděli, že řetězec `'Petr`` je pouze jeden. Těžko však můžeme totéž tričko složit do dvou různých šuplíků ve skříni. 

```js
const name1 = 'petr';
const name2 = 'petr';
```

Ve skutečnosti proměnná na hodnotu pouze odkazuje podobně jako třeba webový odkaz odkazuje na nějakou webovou stránku. 

Na druhou stranu, pole a objekty jsou v JavaScriptu :em[mutable]. Polí `[1, 2, 3]` může skutečně existovat více. Pokaždé, když použijeme hodnotu `[1, 2, 3]`, JavaScript vytvoří úplně nové pole, i když se stejným obsahem. 

Pokud chtěli, aby dvě proměnné skutečně odkazovaly na totéž pole, musíme to provést takto. 

```js
> const x = [1, 2, 3]
> const y = x
> x === y
true
> x.push(8)
> y
[1, 2, 3, 8]
```