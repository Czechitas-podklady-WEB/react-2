## Komponenty

Komponenty v Reactu jsou funkce. Už víme, že v TypeScriptu by všechno mělo mít svůj typ, tedy i komponenta.

U komponenty nás nejvíce zajímá, jaké má *props*. Jaké "parametry" může přijmout a jakého jsou typu.

Víme, že props přichází do komponenty jako vlastnosti objektu. Proto si nejprve vytvoříme *interface* pro tento objekt, kde nastavíme, jako vlastností musí/může mít.

```tsx
export interface PersonProps {
  name: string;
  age: number;
  hasDog: boolean;
}
```

A pak vytvoříme komponentu, kde tento typ/interface nastavíme jako typ pro props:

```tsx
export const Person = ({name, age, hasDog} : PersonProps) => {
  return (
    <div>
      <h2>{name} ({age} let)</h2>
      <p>{hasDog ? 'Má' : 'Nemá'} psa.</p>
    </div>
  )
}
```

Všimněte si, že jsme ze souboru exportovali i interface `PersonProps`, abychom ho případně mohli naimporotvat do místa, kde bychom chtěli pracovat s daty, která mají stejný tva jako props této komponenty.



## Nedoporučený způsob

V Reactu existuje pro komponenty připravený typ `React.FC` (jako FunctionComponent), který můžeme použít. Použití tohoto typu může mít svoje důvody, ale dnes se od něho spíše odrazuje, protože s sebou nese i nějaké nevýhody.

Uvádíme ukázku jen kvůli tomu, že byste se s tím v praxi mohli setkat.

```tsx
// abychom měli typ k dispozici, musíme importovat React
import React from 'react';

export const MyComponent: React.FC = () => {
  return (
    <h1>Ahoj, jsem tvoje komponenta</h1>
  )
}
```

Pokud by komponenta měla props, vypadal by záis takto:

```tsx
import React from 'react';

export interface MyComponentProps {
  name: string;
  age: number;
}

export const MyComponent: React.FC<MyComponentProps> = ({name, age}) => {
  return (
    <h1>Ahoj, jsem tvoje komponenta</h1>
  )
}
```