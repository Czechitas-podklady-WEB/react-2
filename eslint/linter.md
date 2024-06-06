## Kontrola kvality kódu - ESLint

Pokud na projektu pracuje více vývojářů, často chceme vynutit dodržování nějaké kultury ohledně kvality a formátování kódu.

Významnou pomůckou pro kontrolu kvality kódu je v tomto nástroj zvaný *linter*, který kontroluje napsaný kód a hlásí všechny prohřešky proti nim. Nejpoužívanější nástroj pro lintování JavaScriptu se jmenuje *ESLint*.

Pojďme si ho vyzkoušet nejprve na úplně jednoduchém projektu bez Reactu a bez TypeScriptu. Pouze čistý JavaScript.

1. Vytvořte si na disku složku `es-sandbox`, ve které inicializujeme běžný NPM projekt pomocí
   ```
   npm init -y
   ```
1. V projektu vytvořte soubor `index.js`, do kterého vložte krátký kousek kódu, na kterém budeme lintování testovat.
   ```js
   document.body.innerHTML = "<h1>Hello World</h1>";
   ```
1. Nainstalujte do projektu balíček *eslint* jako vývojovou závislost
   ```bash
   npm install -D eslint
   ```
1. Aby nám VS Code během vývoje zobrazoval lintovací chyby, je potřeba nainstalovat rozšíření s názvem *ESLint*. → [odkaz](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
1. VS Code je také potřeba správně nastavit. Následující nastavní přidáme do *JSON Settings*.
   ```
     "editor.codeActionsOnSave": {
       "source.fixAll.eslint": true,
     }
   ```

### Konfigurace

Podobně jako Vite nebo další front-endové nástroje i ESLint má svůj konfigurační soubor. Ten se jmenuje `.eslintrc.js` (nebo s příponou `.cjs` nebo `.mjs`) a vytvoříme jej v hlavní složce projektu. V základní verzi může konfigurace vypadat například takto.

```js
module.exports = {
  env: {
    es2020: true,
  },
  parserOptions: {
    sourceType: 'module',
  },
}
```

- Pomocí vlastnosti `env` nastavujeme v jakém prostředí JavaScript používáme.
- Nastavením `es2020: true` říkáme, že používáme JavaScript ve verzi ES2020.
- Hodnota `sourceType: 'module'` říká, že chceme používat `import/export` místo vkládání JavaScriptu pomocí `<script>` tagů.

ESLint má dobrou [dokumentaci](https://eslint.org/docs/latest/user-guide/configuring/), které se dočtete podrobnosti ke každému jednotlivému nastavení.
