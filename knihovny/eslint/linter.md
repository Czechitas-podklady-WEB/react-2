## Kontrola kvality kódu

Pokud na projektu pracuje více vývojářů, často chceme vynutit dodržování nějaké kultury ohledně formátování kódu, aby se nám nestalo, že kód v každý souboru bude vypadat jinak podle toho, kdo jej zrovna psal.

Významnou pomůckou je v tomto nástroj zvaný *linter*, který kontroluje napsaný kód a hlásí všechny prohřešky proti nim. Nejpoužívanější nástroj pro lintování JavaScriptu se jmenuje *ESLint*. Abychom si jej mohli vyzkoušet a správně nastavit, bude třeba provést následující kroky.

1. Vytvořte si na disku složku `es-sandbox`, ve které inicializujeme běžný NPM projekt pomocí
   ```
   npm init -y
   ```
1. V projektu vytvořte soubor `index.js`, do kterého vložte krátký kousek kódu, na kterém budeme lintování testovat.
   ```js
   document.body.innerHTML = "<h1>Hello World</h1>";
   ```
1. Nainstalujte do projektu balíček *eslint* jako vývojovou závislost
   ```
   npm install -D eslint
   ```
1. Aby nám VS Code během vývoje zobrazoval lintovací chyby, je potřeba nainstalovat rozšíření s názvem *ESLint*.
1. VS Code je také potřeba správně nastavit. Následující nastavní přidáme do *JSON Settings*.
   ```
     "eslint.validate": [
       "javascript"
     ],
     "editor.codeActionsOnSave": {
       "source.fixAll.eslint": true,
     }
   ```

### Konfigurace

Podobně jako Webpack i ESLint má svůj konfigurační soubor. Ten se jmenuje `.eslintrc.js` a vytvoříme jej v hlavní složce projektu. V základní verzi může konfigurace vypadat například takto.

```js
module.exports = {
  env: {
    es2015: true,
  },
  parserOptions: {
    sourceType: 'module',
  },
}
```

- Pomocí vlastnosti `env` nastavujeme v jakém prostředí JavaScript používáme.
- Nastavením `es2015: true` říkáme, že používáme JavaScript ve verzi ES2015. 
- Hodnota `sourceType: 'module'` říká, že chceme používat `import/export` místo vkládání JavaScriptu pomocí `<script>` tagů.

ESLint má dobrou [dokumentaci](https://eslint.org/docs/latest/user-guide/configuring/), které se dočtete podrobnosti ke každému jednotlivému nastavení.
