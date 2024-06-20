## Generické typy

Generiku už jsme si jednou ukazovali, pojďme se na ni přesto podívat na jednodušším příkladu a vysvětlit, kdy ji můžeme potřebovat. Možná už jste slyšeli o principu **DRY** (tj. *"Neopakujme se."*, *"Don't repeat yourself."*), který nám s tím pomůže. Jedním ze způsobů jak se vyhnout zbytečnému opakování je totiž právě generika.

Představte si, že programujete web pro svůj oblíbený časopis a často potřebujete potřebujete zvýraznit první element pole - jednou je to první článek na blogu, podruhé první písmeno článku a tak dále. Funkce na získání prvního elementu pole bude vypadat pokaždé stejně, liší se jenom pole, která jí předáváte. Jednou to můžou být čísla, jindy stringy. Mohli bychom napsat:

```ts
const getFirstLetter = (allLetters: string[]) => allLetters[0];

const getFirstBlogPost = (posts: BlogPost[]) => posts[0];

const getFirstNumber = (numbers: number[]) => numbers[0];
```

Hmmm...

Nezdá se vám to jako hodně opakování? V případě takhle krátké a jasné funkce to nemusí vadit, ale úplně stejný princip bude platit i s komponenty, které v Reactu budete chtít vyrábět maximálně znovupoužitelné. Stejně tak nebudete chtít psát logiku `useForm` hooku, který jsme si ukazovali minule, pokaždé znovu jen proto, že váš formulář zpracovává jiná data.

S použitím generiky můžeme naše tři funkce na získání prvního prvku pole spojit do jedné:

```ts
const getFirstItem<T> = (item: T[]): T => T[0];
```

`getFirstItem([1, 2, 3])` nám vrátí číslo `1`. `getFirstItem([a, b, c])` nám vrátí `a`. A my už se nemusíme opakovat. :)

::fig{src=assets/generics.png size=70}