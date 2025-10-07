## Stav a události v Reactu

V komponentách často vytváříme interní stav pomocí `useState`. Potřebujeme nastavit, jakého typu bude hodnota, která bude ve stavu uložená.

Pokud jde o základní datové typy, typ se sám odvodí z výchozí hodnoty a my nemusíme nic dělat:

```tsx
import {useState} from 'react';

export const MyComponent = () => {
  // count má typ number, protože hodnota 0 je number
  const [count, setCount] = useState(0);

  // name má typ string, protože 'Alena' ej string
  const [name, setName] = useState('Alena');
}
```

Pokud ale potřebujeme do stavu ukládat například objekt, chceme pro tento objekt vytvořit interface a potom tento interface podstrčit do `useState` jako typ hodnoty, která tam bude uložená:

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

Často potřebujeme u událostí použít tzv. **eventObject**. Ten má pro každý typ události jinou podobu. Obsahuje jiné vlastnosti, pokud šlo o událost kliknutí na tlačítko, a jiné vlastnosti, pokud šlo o událost změna hodnoty formulářového pole.

Pokud naše událost potřebuje použít event object, musíme správně nastavit jeho typ, aby TypeScript věděl, jaké vlastnosti v objektu má očekávat.

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

### Události pro jiné elementy

| Prvek | Typ |
| ----- | --- |
| `<input>` |`React.ChangeEvent<HTMLInputElement>` |
| `<form>` |`React.FormEvent<HTMLFormElement>` |
| `<button>` |`React.MouseEvent<HTMLButtonElement>` |
| `<div>` |`React.MouseEvent<HTMLDivElement>` |
| `<select>` |`React.ChangeEvent<HTMLSelectElement>` |
| `<a>` |`React.MouseEvent<HTMLAnchorElement>` |
