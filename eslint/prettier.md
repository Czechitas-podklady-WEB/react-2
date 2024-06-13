## Prettier pro hezčí kód

Pracuje-li na projektu více vývojářů, chceme kromě kvality kódu obvykle vynutit i formátování kódu, aby se nám nestalo, že kód v každém souboru bude vypadat jinak podle toho, kdo jej zrovna psal.

Podobně jako nám *linter* vynucoval kvalitu kódu a opravoval chyby, můžeme použít *code formatter* pro opravu formátování. Situace se trochu komplikuje tím, že i *linter* může nějaké formátování kódu opravovat.

### Linter vs. code formatter

Linter:
- hlásí chyby v kódu,
- automaticky opravuje chyby v kódu,
- umožnuje nám nastavit si vlastní pravidla,
- může formátovat kód.

Formátovač kódu:
- pouze formátuje kód.

### Prettier

Nejznámějším a nejpoužívanějším nástrojem pro formátování kódu je Prettier. Podobně jako u ESLintu i Prettier budeme do projektu instalovat jako NPM balíček a zároveň si přidáme do VS Code i rozšíření → [odkaz](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode).

Ve VS Code si do Settings JSON přidáme:
```JSON
{
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}
```

### Přidání Prettieru do projektu

1. Nainstalujeme Prettier jako vývojářskou závislost:
   ```bash
   npm install -D -E prettier
   ```
1. V kořenové složce projektu vytvoříme soubor `.prettierrc`, abychom dali editoru a dalším nástrojům vědět, že náš projekt používá Prettier. Do souboru zatím napíšeme jenom:
   ```js
   {}
   ```
1. Můžeme vytvořit soubor `.prettierignore`, do kterého bychom uvedli jména souborů a složek, které má Prettier ignorovat. Pokud náš projekt obsahuje soubor `.gitignore`, můžeme tento krok přeskočit. Prettier bude ignorovat stejné soubory jako Git.

Protože chceme v projektu používat ESLint a Prettier zároveň a oba nástroje mohou formátovat kód, musíme je nastavit tak, aby spolupracovali a vzájemně si nepřepisovali provedené změny.

1. Nainstalujeme doplňující style guide pro ESLint.
   ```bash
   npm install --save-dev eslint-config-prettier
   ```
2. Do konfiguračního souboru ESLintu doplníme prettier do sekce `extends` a dáme ho na poslední místo. Prettier tak bude mít šanci nakonec naformátovat kód dříve opravený ESlintem.
   ```js
   extends: [
     'konfigurace-ktere-zde-jsou-z-drivejska',
     'eslint-config-prettier',
   ]
   ```

### Konfigurace Prettieru

V konfiguračním souboru `.pretierrc` si můžeme nastavit, jak má Prettier náš kód formátovat.

```JSON
{
  "trailingComma": "es5",
  "useTabs": false,
  "tabWidth": 2,
  "semi": false,
  "singleQuote": true,
  "printWidth": 80
}
```

Taková konfigurace například zajistí:
- čárky za každým prvek v poli nebo za každou vlastností objektu
- odsazení kódu pomocí mezer, ne tabulátoru
- jedna úroveň odsazení je o 2 mezery
- na konci příkazů nevyžadujeme středníky
- k ohraničení textových řetězců používáme jednoduché uvozovky (apostrofy)
- řádky kódu chceme mít maximálně 80 znaků dlouhé

Kompletní přehled parametrů najdete v [dokumentaci](https://prettier.io/docs/en/api).


