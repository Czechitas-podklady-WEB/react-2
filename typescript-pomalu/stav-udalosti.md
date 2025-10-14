## Stav a události v Reactu

V komponentách často vytváříme interní stav pomocí `useState`. Potřebujeme nastavit, jakého typu bude hodnota, která bude ve stavu uložená.

Pokud jde o základní datové typy, typ se sám **odvodí** z výchozí hodnoty a my nemusíme nic dělat:

```tsx
import {useState} from 'react';

export const MyComponent = () => {
  // count má typ number, protože hodnota 0 je number
  const [count, setCount] = useState(0);

  // name má typ string, protože 'Alena' ej string
  const [name, setName] = useState('Alena');
}
```

Pokud ale potřebujeme do stavu ukládat například objekt, vytvoříme interface a potom tento interface podstrčíme do `useState` jako typ hodnoty, která tam bude uložená:

```tsx
import {useState} from 'react';

export interface User {
  name: string;
  age: number;
  hasDog: boolean;
}

export const MyComponent = () => {
  const [user, setUser] = useState<User>({
    name: 'Alena',
    age: 27,
    hasDog: true,
  });
}
```

## Události

Když reagujeme na události (např. odeslání formuláře, klik na odkaz, stisk klávesy), často potřebujeme v obslužné funkci použít tzv. **eventObject**. Ten má pro každý typ události jinou podobu a a bude obsahovat trochu jiné vlastnosti, když šlo o událost kliknutí na tlačítko (`onClick`), a jiné vlastnosti, když šlo o událost změna hodnoty formulářového pole (`onChange`).

Potřebuje-li naše obslužná funkce použít event object, musíme správně nastavit jeho typ, aby TypeScript věděl, jaké vlastnosti v objektu má očekávat.

### Kliknutí na tlačítko

```tsx
function handleClick(e: React.MouseEvent<HTMLButtonElement>) {
  console.log("Kliknuto!", e.clientX, e.clientY);
}

return <button onClick={handleClick}>Klikni</button>;
```

### Změna formulářového pole

```tsx
function handleChange(e: React.ChangeEvent<HTMLInputElement>) {
  console.log(e.target.value);
}

return <input onChange={handleChange} />;
```

Pro prvek `<textarea>` by to bylo `React.ChangeEvent<HTMLTextAreaElement>` atd.

### Odeslání formuláře

```tsx
function handleSubmit(e: React.FormEvent<HTMLFormElement>) {
  e.preventDefault();
  console.log("Formulář odeslán");
}

return <form onSubmit={handleSubmit}>...</form>;
```

### Nejčastější události pro běžné elementy

| Prvek | Událost | Typ |
| ----- | ------- | --- |
| form | onSubmit | `React.FormEvent<HTMLFormElement>` |
| input | onChange | `React.ChangeEvent<HTMLInputElement>` |
| textarea | onChange | `React.ChangeEvent<HTMLTextAreaElement>` |
| select | onChange | `React.ChangeEvent<HTMLSelectElement>` |
| button | onClick | `React.MouseEvent<HTMLButtonElement>` |
| div | onClick | `React.MouseEvent<HTMLDivElement>` |
| a | onClick | `React.MouseEvent<HTMLAnchorElement>` |

## Jak zjistit, jakého typu je událost

Můžeš hledat na Googlu nebo se zeptat ChatuGPT. Nejjednodušší ale je, nechat si napovědět přímo v editoru. Stačí do události napsat anonymní funkci, která přijímá parametr `e`, a pak se na něj myší postavit. VS Code ti ukáže nápovědu TypeScriptu, kde bude uvedeno, jakého typu event být.

Například chci reagovat na kliknutí na `<div>`:

```tsx
export const ClickableDiv = () => {
  return (
    <div onClick={(e) => {}}> Klikni na mě</div>
  )
}
```

Když najedu myší na `e`, VS Code mi řekne, že `e` je typu `React.MouseEvent<HTMLDivElement>`.

Na začátku to vypadá složitě, ale časem zjistíš, že se typ skládá ze dvou částí. První 48st určuje typ událostia nejčastěji to bude `FormEvent`, `ChangeEvent`, `MouseEvent` a `KeyboardEvent`. Druhá část je pak uvedená ve špičatých závorkách a představuje prvek, na kterém k události dochází - např.  `HTMLDivElement`, `HTMLInputElement`, `HTMLButtonAlement` a podobně.

## Složené typy

Občas se nám stane, že potřebujeme volat jednu funkci, jako reakci na událost u několika různých formulářových prvků.

V TypeSriptu existuje symbol *svislítka* `|`, který můžeme použít pro spojení více typů (tzv. *union type*).

My už jsme jeho použití viděli, když jsme definovali typ, který může obsahovat pouze určité hodnoty, např.:

```ts
type Direction = 'sever' | 'jih' | 'východ' | 'západ';
```

Svislítko slouží jako **nebo** a říká, že v Direction může být `sever` nebo `jih` nebo `východ` nebo `západ`.

Stejně ho můžeme použít i v případě naší funkce, která má reagovat na událost onChange na prvku `<input>` **nebo** `<textarea>`.

```ts
const onChange = (e: React.ChangeEvent<HTMLInputElement | HTMLTextAreaElement>) => {
  // kód funkce
}
```