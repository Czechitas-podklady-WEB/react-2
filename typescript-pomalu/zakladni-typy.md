## Datové typy v TypeScriptu

Jako rychlé opáčko z minulé lekce si pojďme ještě jednou ukázat, jaké mám základní typy v TypeScriptu:

## Základní datové typy

```ts
let count: number = 42;
let message: string = "Hello, TypeScript!";
let isLogged: boolean = true;
```

Trochu zvláštní nám může připadat, že máme speciální datový typ pro hodnoty `null` a `undefined`, které obvzkle reprezentují neexistující nebo neznámé hodnoty:

```ts
let data: null = null;
let value: undefined = undefined;
```

## Objekty

Potřebujeme-li do proměnné uložit objekt, mohli bychom typ nastavit na `object`, ale to obvykle v praxi moc nepoužíváme. My totiž chceme, aby na nás byl TypeScript **přísný**. Typy chceme nastavovat co nestriktnější (narrow type). Když nadefinujeme typ jako `objekt`, můžeme do proměnné uložit jakýkoliv objekt. Ať už do proměnné uložíme objekt s popisem zaměstnance, objekt s údaji z faktury, nebo výherní tiket z loterie, TypeScript bude spokojený. Objekt jako objekt.

```ts
// toto jde, ale většinou to neděláme
let user: object = { ... };
```

U objektů obvykle chceme nastavit přesný **tvar** (shape), který objekt musí dodržet. To znamená, že nastavíme, jaké přesně vlastnosti v objektu musí být a jakého jsou typu. V TypeScriptu existují dva způsoby, jako to udělat. Buď pomocí `type` nebo pomocí `interface`. Oba se zapisují velmi podobně, jen s malými rozdíly, a pro naše základní použití mezi nimi neexistuje rozdíl. Odlišnosti v použití si ukážeme v pozdější lekci o pokročilém TypeScriptu.

V obou připadech nejprve nadefinujeme typ/interface a poté vytvoříme proměnnou s tímto typem.

```ts
// pomocí type
type User = {
  name: string;
  age: number;
  isAdmin: boolean;
}

const newUser: User = { ... }
```

```ts
// pomocí interface
interface User {
  name: string;
  age: number;
  isAdmin: boolean;
}

const newUser: User = { ... }
```

Našla jsi rozdíl v zápisu `type` a `interface`? My obvykle budeme v kurzu preferovat interface, ale většinou je úplně jedno, který ze zápisů použiješ. V praxi se můžeš setkat s tím, že zaměstnavatel nebo tým bude mít nastavené vlastní reference a ty se budeš muset přizpůsobit.


## Pole

Pro pole také existují dva způsoby, jak nastavit typ. No není ten TypeScript zábava? Je úplně jedno, který zápis použiješ. Osobně si myslím, že první zápis s hranatými závorkami za názvem typu je trochu kratší a přehlednější a budeme ho v kurzu preferovat.

```ts
let numbers: number[] = [1, 2, 3, 4];
let name: Array<string> = ['Alena', 'Jana', 'Linda'];
```

Samozřejmě můžeš chtít mít v programu i pole objektů. V tom případě použijeme typ/interface objektu úplně stejným způsobem, jako základní typy. Když budeme potřeboval pole uživatelů (viz. typ User uvedený výše), napíšeme prostě:

```ts
let users: User[] = [{ ... }, { ... }];
// nebo
let users: Array<User> = [{ ... }, { ... }];
```

## Speciální typy `any` a `void`

**any** je typ, který umožňuje proměnným nabývat hodnot jakéhokoliv typu. V podstatě se pak proměnná bude chovat jako v klasickém JavaScriptu a můžeme do ní uložit libovolnou hodnotu. Používejte jen velmi výjimečně, protože tím ztrácíte typovou kontrolu.

```js
// toto všechno je OK, což je vlastně hrozně špatně
let dynamicValue: any = "This can be anything.";
dynamicValue = 42;
dynamicValue = true;
dynamicValue = { name: 'Emil', age: 27 };
dynamicValue = [1, 2, 3];
```

Typ **void** reprezentuje absenci hodnoty. Používá se obvykle pro funkce, které nic nevracejí. O funkcích si povíme za chvilku v další sekci.

```js
const logMessage = (): void => {
  console.log("This is a log message.");
};
```

## Skupina hodnot

Někdy potřebujeme určit, že proměnná může obsahovat pouze konrétní hodnotu. Můžeme hodnotu použít jako typ:

```ts
let name: 'Alena' = 'Alena';

// chyba, jméno může být pouze Alena
name = 'Lucie'
```

To obvykle není příliš užitečné, ale můžeme si vytvořit typ, který obsahuje **skupinu hodnot** (tzv. union values):

```ts
type Direction = 'sever' | 'jih' | 'východ' | 'západ';

let direction: Direction = 'jih';

// chyba, m;6e obsahovat pouye sever, jih, východ nebo západ
direction = 'rovně';
```

