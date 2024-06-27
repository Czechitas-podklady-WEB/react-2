## Pokrytí kódu testy

Vitest nám umí i ukázat, kolik procent našeho kódu je tzv. pokrytých testy.

Abychom se mohli nechat statistiku pokrytí vygenerovat, bude Vitest potřebovat ještě knihovnu `coverage-v8`:
```bash
npm install --save-dev @vitest/coverage-v8
```

Do skriptů v našem `package.json` si přidáme další skript:
```json
{
  "scripts": {
    "test": "vitest",
    "coverage": "vitest run --coverage"
  }
}
```

A pak můžeme na příkazové řádce spustit:
```bash
npm run coverage
```

Dostaneme tabulku, která nám ukáže, rpo jaké soubory v naší aplikaci máme nebo nemáme napsané testy a kolik procent v daném souboru testy pokrývají.

::fig{src=assets/coverage.png size=70}

Není vždy nezbytně nutné, aby bylo testy pokryto 100 % aplikace. Důležité je pokrytí kritických funkcí a komponent. Zároveň je třeba si uvědomit, že když je soubor 100% pokryt testy neznamená to, že je otestován dobře a že testy případně odhalí všechny chyby. Znamená to jen, že jsme danou funkci/komponentu *nějak* otestovali.