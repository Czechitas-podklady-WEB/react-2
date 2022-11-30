---
title: Nastavení projektu
demand: 3
---

Zkusíme si od základu vyrobit jednoduchý *Webpack* projekt.

1. Někde na disku si vytvořte složku `wp-app`.
1. Ve složce inicializujte v NPM projekt. Vytvořte základní strukturu projektu se složkou `src`, souborem `index.js` a souborem `index.html`.
1. Pomocí JavaScriptu vložte do stránky odstavec s textem
   ```
   Zvlášť zákeřný učeň s ďolíčky běží podél zóny úlů
   ```
1. Nainstalujte do projektu *Webpack* a *DevServer*.
1. V `package.json` vytvořte spouštěcí skript pro příkaz `serve`.
1. Vytvořte zcela základní konfiguraci pro *Webpack*, která pouze zpracuje hlavní soubor `src/index.js` a vyrobí výsledný soubor s názvem `app.js`.
1. Přidejte do konfigurace asset modul pro soubory HTML. Vytvořte soubor `index.html`, který vkládá správný JavaScript. Importujte váš soubor `index.html`, aby jej Webpack vložil do cílové složky.
1. Nakonfigurujte `DevServer` tak, aby explicitně vytvářel složku `dist`.
1. Spusťte váš NPM skript a vyzkoušejte, že vaše aplikace funguje.
1. Přidejte do vaší konfigurace další asset modul pro zpracování souborů s příponou `.ico`. Tyto soubory nechť *Webpack* vloží do složky `dist/images`.
1. Do hlavičky souboru `index.html` nastavte cestu k faviconě
   ```html
   <link rel="icon" type="image/x-icon" href="/images/rocket.ico" />
   ```
1. Stáhněte si [faviconu raketky](assets/rocket.ico) a vložte ji do složky `src`. V souboru `index.js` importuje raketku a sestavte projekt *Webpackem*. Vyzkoušejte, že stránka správně funguje a že má hezkou ikonku.
1. Z dokumentace k `DevServeru` vyčtěte, jak se nastavuje port, na kterém má server běžet. Změňte konfiguraci tak, aby váš web běžel na portu 4000 místo výchozích 8080.
