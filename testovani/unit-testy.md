## Unit testy

Jak už jsme zmínili předtím, unit testy slouží pro otestování samostné jednotky našeho kódu, typicky nějaké funkce nebo metody.

Pro unit testy existuje mnoho známých testovacích frameworků, jejichž jména jste možná už někdy zaslechli:
- Jest
- Mocha
- Jasmine

Protože v našich reactích projektech používá Vite, vyzkoušíme si nástroj **Vitest** od stejných autorů, který je moderní, rychlý, jednoduchý na konfiguraci, nativně podporuje TypeScript. Díky zaručené kompatibilitě s Vite ekosystémem je to pro naše aplikace ideální volba. Navíc je zcela kompatibilní s extrémně populárním Jestem, případně i s jiným testovacím frameworkem Chai.

## Vitest

[Vitest](https://vitest.dev/) si musíme do našeho projektu nejprve nainstalovat jako vývojářskou závislost:

```bash
npm install --save-dev vitest
```

Abychom mohli testy jednoduše spouštět, přidejme si do `package.json` další skript:

```json
{
  "scripts": {
    "test": "vitest"
  }
}
```

Testy pak můžeme jednoduše spoustit pomocí `npm run test`.

Můžete si také nainstalovat [doplněk Vitest do VS Code](https://marketplace.visualstudio.com/items?itemName=vitest.explorer), který vám umožní spouštět testy a prohlížet si jejich výsledky přímo v prostředí editoru.

### Kam psát testy

Soubory s testy by se vždy měly jmenovat `*.test.ts` nebo `*.spec.ts`.

Testy můžeme umístit do složky  `tests` (v kořenové složce projektu). Později do této složky umístíme i soubor `setup.ts`, kde nastavíme další testovací nástroje.

```
.
├─ src
│  └─ App.tsx
├─ tests
│  ├─ setup.ts
│  └─ some-other.test.ts
├─ package.json
└─ vite.config.ts
```

Pokud píšeme test pro konkrétní komponentu, je dobrým zvykem pojmenovat soubor s testem stejně jako se jmenuje komponenta a umístit ji do stejné složky. Například:

```
.
├─ App.tsx
├─ App.test.ts
├─ Component.tsx
└─ Component.test.ts
```

Není to ale podmínka. Nástroj, který budeme pro testování používat, si naše testy najde a spustí skoro kdekoliv, pokud se jmenují správně `*.test.tsx`. Různé týmy mají různé zvyklosti, jak si testy v projektu organizovat.


### Struktura testovacího souboru

Každý soubor s testy se skládá z následujících částí:
- **Test suite** - testovací sada, můžeme pomocí ní seskupit více testů do skupiny a tu nějak pojmenovat. *Test suite* tedy může obsahovat více jednotlivých *test cases*. Pro vytvoření sady používáme `describe`.
- **Test case** - testovací případ popisuje, co chceme ověřit. Pro definici testu používáme `test` nebo `it`.
- **Assertion** - tvrzení, vyhodnotí výsledek (např. volání funkce) a porovná ho s očekávaným výsledkem. Používáme `expect`.


## První test

Pojďme si ukázat, jak takový jednoduchý test může vypadat.

Vytvořme si v kořenové složce projektu složku `tests` a v ní soubor `first.test.ts`:

```ts
import { describe, test, it, expect } from 'vitest'

// test suite
describe('Truthy statements', () => {

  // test
  test('1 + 1 equals 2', () => {
    // assertion
    expect(1+1).toEqual(2)
  })

  // test
  it('should equal to true', () => {
    // assertion
    expect(!false).toEqual(true)
  })

})
```

Tento konkrétní test je nám samozřejmě k ničemu, ale jednoduše na něm vidíme způsob budování unit testů.

`describe` můžeme klidně vynechat, pokud nepotřebujeme v rámci jednoho testovacího souboru seskupovat testy do více skupin.

`test` a `it` dělají tu stejnou věc - popisují náš test. Záleží pouze na nás, jakou variantu si vybereme, aby se nám testovací případy lépe četly. *"It should equal to true"* zní hezky anglicky.

### Testování funkcí

Pod pojmem *unit test* si většinou představíme základní testování funkcí. V reálné aplikaci budeme mít například soubor s několika funkcemi. Jednotlivé funkce v souboru exportujeme, abychom je mohli na jiném místě v aplikaci naimportovat a použít. To stejné uděláme i v našem testovacím souboru - funkce si naimportujeme a otestujeme, zda s různými hodnotami vrací správné výsledky.

Představme si jednoduchý soubor *math.ts*:
```js
export function add(a: number, b:number):number {
  return a + b;
}

export function sum(...numbers:number[]):number {
  return numbers.reduce(add, 0)
}
```

K němu si můžeme napsat sadu testů v souboru *math.test.ts*:
```ts
import {describe, test, expect } from 'vitest'
import { add, sum } from './math'

describe('Add function', () => {
  test('1 + 2 equals to 3', () => {
    expect(add(1, 2)).toEqual(3)
  })

  test('1 + -1 equals to 0', () => {
    expect(add(1, -1)).toEqual(0)
  })
})

describe('Sum function', () => {
  test('sum(1, 2, 3) equals to 6', () => {
    expect(sum(1, 2, 3)).toEqual(6)
  })

  test('sum(1, -1) equals to 0', () => {
    expect(sum(1, -1)).toEqual(0)
  })

  test('sum() equals to 0', () => {
    expect(sum()).toEqual(0)
  })
})
```

V naší jednoduché ukázce jsme si prozatím použili pouze metodu `toEqual`, které testuje, zda je hodnota rovná očekávané hodnotě. Možností, jak výsledky porovnávat, máme samozřejmě ale mnohem více. Můžeme testovat i typy:

- [dokumentace pro expect](https://vitest.dev/api/expect.html)
- [dokumentace pro expectTypeOf](https://vitest.dev/api/expect-typeof.html)
