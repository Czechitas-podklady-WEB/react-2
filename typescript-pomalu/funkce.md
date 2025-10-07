## Funkce

U funkcí v typescriptu nastavujeme dvě věci:
- typ parametrů funkce
- typ návratové hodnoty

```ts
function add(a: number, b: number) : string {
  return `Součet čísel ${a} a ${b} je ${a + b}.`;
}
```

Nezáleží na tom, jestli je to funkce vytvořená pomocí slova `function` nebo jako *arrow function*.

```ts
const add = (a: number, b: number) : string {
  return `Součet čísel ${a} a ${b} je ${a + b}.`;
}
```

Pokud funkce nevrací žádnou hodnotu, můžeme to explkicitně vyjádřit tím, že jako návratový typ uvedeme `void`.

```ts
function sayHello() : void {
  console.log('Hello');
}
```

## Funkce jako hodnota

Protože funkce je v JavaScriptu hodnota podobně jako např. číslo, můžeme funkce předávat do jiných funkcí jako parametry, případně můžeme mít funkce jako hodnoty vlastností u objektů (pak jim obvykle říkáme metody). Pak samozřejmě musíme mít možnost nastavit typ takové vlastnosti nebo parametru.

Představme si, že máme funkci, která spustí jinou funkci s nastaveným zpožděním.

```ts
function sayHello() : void {
  console.log(`Hello`);
}

function setDelay(delay: number, callback: ????) : void {
  console.log(`Run callback after ${delay} seconds`);
  setTimeout(callback, delay * 1000);
}

// chceme funkci sayHello spustit za 5 vterin
setDelay(5, sayHello);
```

Co napíšeme místo otazníků `????`? Jak nadefinujeme, že do funkce `setDelay` můžeme poslat jen funkce určitého typu?

```ts
// chceme, aby callback byla vždy funkce bez parametrů, která nevrací žádnou hodnotu
function setDelay(
  delay: number,
  callback: () => void
) : void {
  // ...
}
```

Můžeme so samozřejmě typ nadefinovat i dopředu a potom ho použít:

```ts
type HelloFunction = () => void;

function setDelay(
  delay: number,
  callback: HelloFunction
) : void {
  // ...
}
```

Pokud by se jednalo o funkci s parametry a/nebo s návratovou hodnotou, je to jednoduché:

```ts
type AddFunction = (a: number, b: number) => string;
```

Tomuto typu bude odpovídat každá funkce, která má dva číselné parametry a vrací textový řetězec.
