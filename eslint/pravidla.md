## ESLint pravidla

I když jsme ESLint základně nastavili, zatím nic nedělá. Zatím jsme totiž nespecifikovali žádná pravidla pro kvalitu našeho kódu.

ESLint obsahuje stovky pravidel pro různé situace. Tato pravidla se zapisují do konfigurace pod klíč `rules`. Takto například řekneme, že pokud ESLint uvidí neexistující proměnnou, má ji označit jako chybu.

```js
rules: {
  'no-undef': 'error',
},
```

Pokud jsme vše správně nastavili, po uložení konfigurace nám ESLint okamžitě podtrhne proměnnou `document` v souboru `index.js` jako chybu. A má pravdu, tuto proměnnou jsme skutečně nikde nedefinovali. Proměnná `dokument` je však automaticky definovaná pokud kód spouštíme v prohlížeči. Dáme tedy ESLintu vědět, že náš JavaScript se spouští v prostředí prohlížeče.

```js
env: {
  browser: true,
}
```

V tuto chvíli už nám ESLint použití `document` dovolí.

### Automatické opravy

Pokud je jednoznačné, jak se má nějaká chyba v kódu opravit, ESLint to udělá za vás při uložení souboru. Nastavme třeba, že chceme vždy používat jednoduché uvozovky místo dvojitých. To nám zařídí pravidlo [quotes](https://eslint.org/docs/latest/rules/quotes).

```js
rules: {
  'no-undef': 'error',
  'quotes': ['error', 'single'],
},
```

Když nyní uložíme náš `index.js`, dvojité uvozovky se automaticky změní na jednoduché.

### Doporučená pravidla

Pravidel pro ESLint je opravdu hodně. Jejich celý seznam najdete v [dokumentaci](https://eslint.org/docs/latest/rules). Konfigurace každého pravidla je zde detailně popsaná. Pomocí těchto pravidel si můžete zkusit sestavit vlastní kulturu kódu. Například takto:

```js
rules: {
  'constructor-super': 'error',
  'for-direction': 'error',
  'getter-return': 'error',
  'no-async-promise-executor': 'error',
  'no-case-declarations': 'error',
  'no-class-assign': 'error',
  'no-compare-neg-zero': 'error',
  'no-cond-assign': 'error',
  'no-const-assign': 'error',
  'no-constant-condition': 'error',
  'no-control-regex': 'error',
  'no-debugger': 'error',
  'no-delete-var': 'error',
  'no-dupe-args': 'error',
  'no-dupe-class-members': 'error',
  'no-dupe-else-if': 'error',
  'no-dupe-keys': 'error',
  'no-duplicate-case': 'error',
  'no-empty': 'error',
  'no-empty-character-class': 'error',
  'no-empty-pattern': 'error',
  'no-ex-assign': 'error',
  'no-extra-boolean-cast': 'error',
  'no-extra-semi': 'error',
  'no-fallthrough': 'error',
  'no-func-assign': 'error',
  'no-global-assign': 'error',
  'no-import-assign': 'error',
  'no-inner-declarations': 'error',
  'no-invalid-regexp': 'error',
  'no-irregular-whitespace': 'error',
  'no-loss-of-precision': 'error',
  'no-misleading-character-class': 'error',
  'no-mixed-spaces-and-tabs': 'error',
  'no-new-symbol': 'error',
  'no-nonoctal-decimal-escape': 'error',
  'no-obj-calls': 'error',
  'no-octal': 'error',
  'no-prototype-builtins': 'error',
  'no-redeclare': 'error',
  'no-regex-spaces': 'error',
  'no-self-assign': 'error',
  'no-setter-return': 'error',
  'no-shadow-restricted-names': 'error',
  'no-sparse-arrays': 'error',
  'no-this-before-super': 'error',
  'no-undef': 'error',
  'no-unexpected-multiline': 'error',
  'no-unreachable': 'error',
  'no-unsafe-finally': 'error',
  'no-unsafe-negation': 'error',
  'no-unsafe-optional-chaining': 'error',
  'no-unused-labels': 'error',
  'no-unused-vars': 'error',
  'no-useless-backreference': 'error',
  'no-useless-catch': 'error',
  'no-useless-escape': 'error',
  'no-with': 'error',
  'require-yield': 'error',
  'use-isnan': 'error',
  'valid-typeof': 'error'
}
```

Vyladit takto precizní nastavení je však práce, ze které hrozí velká újma na psychické pohodě a pro slabší jedince i vážné zdravotní problémy. Existují proto určité doporučené sady pravidel, kterým se říká :term{cs="stylistické příručky" en="style guides"}.

Základní doporučená nastavení obsahuje konfigurace `eslint:recommended`, která je přímo součástí `ESLintu`, můžete ji použít takto:

```js
extends: 'eslint:recommended'
```

Tato pravidla jsou však jen velmi základní a většinou potřebujeme mnohem detailnější nastavaní. V praxi se nejvíce používají následující 3 stylistické příručky. Každá prosazuje určité styly formátování.

- [Standard](https://standardjs.com) - je mimo jiné proti používání středníků,
- [AirBnB](https://github.com/airbnb/javascript) - nejpřísnější ze všech tří:
  - vyžaduje středníky,
  - vyžaduje mezery kolem složených závorek u objektů,
  - vyžaduje `default export`, pokud exportujeme pouze jednu hodnotu,
- [Google](https://google.github.io/styleguide/jsguide.html) - méně přísná než AirBnB, také vyžaduje středníky.

Všechny tyto příručky se shodnou na následujicím:

1. odsazení pomocí dvou mezer,
1. jednoduché uvozovky místo dvojitých,
1. otvírací složená závorka bloku není na novém řádku,
1. nepoužívat `var`, vždy `const` nebo `let`,
1. žádné bílé znaky na konci řádků.

Detailnější srovnání všech příruček najdete například v [tomto článku](https://betterprogramming.pub/comparing-the-top-three-style-guides-and-setting-them-up-with-eslint-98ea0d2fc5b7).

### AirBnB style guide

Pokud bychom například chtěli použít příručku AirBnB, musíme nainstalovat balíček [eslint-config-airbnb](https://www.npmjs.com/package/eslint-config-airbnb)

```js
npm install -D eslint-config-airbnb
```

Stačí pak do `.eslintrc.js` vložit

```js
extends: 'airbnb'
```
