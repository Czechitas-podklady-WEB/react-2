## ESLint

Pokud na projektu pracuje více vývojářů, často chceme vynutit dodržování nějaké kultury ohledně formátování kódu, aby se nám nestalo, že kód v každý souboru bude vypadat jinak podle toho, kdo jej zrovna psal.

Významnou pomůckou je v tomto nástroj zvaný *linter*, který kontroluje napsaný kód a hlásí všechny prohřešky proti nim. Nejpoužívanější nástroj pro lintování JavaScriptu se jmenuje *ESLint*. Abychom jej mohli začít používat, je potřeba s nejdříve do VS Code nainstalovat rozšíření stejného jména.

Musíme také do našeho projektu nainstalovat balíček *eslint*.

```
npm install -D eslint
```

Podobně jako Webpack i ESLint má svůj konfigurační soubor. Ten se jmenuje `.eslintrc.js`. 


VS Code Settings:

```
"eslint.validate": [
  "javascript"
],
"editor.codeActionsOnSave": {
  "source.fixAll.eslint": true,
}
```

Odkazy:

- [Seznam ESLint pravidel](https://eslint.org/docs/latest/rules/)
- [eslint:recommended](https://github.com/eslint/eslint/blob/main/conf/eslint-recommended.js)

