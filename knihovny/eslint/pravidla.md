## ESLint pravidla

I když jsme ESLint základně nastavili, zatím nic nedělá. Je to proto, že jsme nespecifikovali žádná pravidla pro kvalitu našeho kódu. 

ESLint obsahuje stovky pravidel pro různé situace. Tato pravidla se zapisují do konfigurace pod klíč `rules`. Takto například řekneme, že pokud ESLint uvidí neexistující proměnnou, má ji označit jako chybu.

```js
rules: {
  'no-undef': 'error',
},
```

Pokud jsme vše správně nastavili, po uložení konfigurace nám ESLint okamžitě podtrhne proměnnou `document` v souboru `index.js` jako chybu. A má pravdu, tuto proměnnou jsme skutečně nikde nedefinovali. 

