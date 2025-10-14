## Typování API

Většina moderních aplikací v Reactu načítá data z nějakého API. Připomeňme si rychle, jakým způsobem jsme s daty obvykle opracovali v předchozích kurzech:

Zatím ještě úplně bez TypeScriptu:

```js
import {useState, useEffect} from 'react';

function MyComponent() {
  const [person, setPerson] = useState(null);

  useEffect(() => {
    const getData = async () => {
      const res = await fetch(`https://some-api.com`);
      const json = await res.json();
      setPerson(json);
    }
    getData();
  }, []);

  return (
    {
      data === null
      ? <p>Načítám data...</p>
      : <div>
          <h2>{person.name} {person.surname}</h2>
          <p>{person.age}</p>
          <p>{person.hasDriversLicence ? 'Má' : 'Nemá'} řidičský průkaz.</p>
        </div>
    }
  )
}
```

Příklad nahoře je zatím pouze v JavaScriptu. Bez nastavených typů. V takové situaci se jako typescriptové vývojářky cítíme velmi nepohodlně. Chceme typovou bezpečnost.

Když v editoru podržíme myší nad proměnnými `res` a `json`, zjistíme následující:
- TypeScript u proměnné `res` správně odvodil a nastavil typ na `Response` (odpověď serveru na dotaz položený pomocí `fetch`)
- u proměnné `json` ale vidíme typ `any` !!!

TypeScript samozřejmě nemůže vědět, jaká data (a v jakém tvaru) nám server pošle. To musíme TyepScriptu říci my.

Předpokládejme, že na náš dotaz dostaneme ze serveru JSON data v tomto tvaru:

```json
{
  "name": "Alena",
  "surname": "Nováková",
  "age": 27,
  "hasDriversLicence": true
}
```

Připravíme si pro tato data interface:

```ts
interface Person {
  name: string;
  surname: string;
  age: number;
  hasDriversLicence: boolean;
}
```

A pak tento interface použijeme na adekvátních místech:
- jako typ pro stav, kam budeme data ze serveru ukládat
- jako typ pro proměnnou, do které budeme dékódovat JSON data ze serverové odpovědi

```ts
import {useState, useEffect} from 'react';

interface Person {
  name: string;
  surname: string;
  age: number;
  hasDriversLicence: boolean;
}

function MyComponent() {
  const [person, setPerson] = useState<Person | null>(null);

  useEffect(() => {
    const getData = async () => {
      const res = await fetch(`https://some-api.com`);
      const json: Person = await res.json();
      setPerson(json);
    }
    getData();
  }, []);

  return (
    {
      data === null
      ? <p>Načítám data...</p>
      : <div>
          <h2>{person.name} {person.surname}</h2>
          <p>{person.age}</p>
          <p>{person.hasDriversLicence ? 'Má' : 'Nemá'} řidičský průkaz.</p>
        </div>
    }
  )
}
```
