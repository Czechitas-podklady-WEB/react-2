V této lekci se vydáme hlouběji do tajů JavaScriptových proměnných a hodnot. Přestože takový výklad může vypadat jako začátečnické téma, brzy zjistíme, že situace je zapeklitější než by se na první pohled zdálo. 

## Motivace

Vytvořme nejdříve několik nevinně vypadajících proměnných:

```js
const age1 = 25;
const age2 = 25;

const name1 = 'robert';
const name2 = 'robert';

const workout1 = [5, 3, 7];
const workout2 = [5, 3, 7];
```

Zdá se, že proměnné po dvojících obsahují tytéž hodonty. Pojďme to otestovat v konzoli.

```js
> age1 === age2
true
> name1 === name2
true
> workout1 === workout2
???
```

Výsledek posledního porovnávání schválně vynecháváme abyste si příkaz sami vyzkoušeli. Výsledek vás nejspíše překvapeni. 

Aby zmatení nebylo málo, provedeme ještě následující experiment:

```js
> const x = [1, 2, 3]
> const y = x;
> x.push(4)
> x === y
???
```

V prvním případě jsme jako porovnání dvou zdánlivě stejných hodnot obdrželi `false`. V druhém případě jsme naoopak při porovnání dvou očekávaně odlišných hodnot obdrželi `true`. Zkusme ještě něco naprosto přímočarého:

```js
> [1, 2, 3] === [1, 2, 3]
false
```

Ne, ještě JavaScript navždy nezavrhujte, není rozbitý. Ve skutečnosti na podobnou situaci narazíte ve většině programovacích jazyků. Logiku a smysl v tom všem objevíme, když porozumíme pojmům jako :em[reference] a :em[imutabilita].
