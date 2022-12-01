## Rozbíjení keší

V této části otevřeme velmi technické téma, které je však naprosto zásadní pro funkčnost již nasazeného webu. 

Webové prohlížeč se snaží co nejvíce optimalizovat načítání stránky, aby uživatel musel čekat pouze co nejkratší možnou dobu. Jedním ze způsobů zrychlení načítaní je takzvané :term{cs=kešování en=caching}, kdy si prohlížeč ukládá už jednou stažené soubory jako obrázky, JavaScripty, CSS někam na disk. Když se pak stránka načte znova, prohlížeč si se serverem vykomunikuje, jestli se daný soubor od posledního načtení změnil a pokud ne, prohlížeč použije soubor, kerý má uložený a nemusí jej znova stahovat.

Kešování však působí potíže ve chvíli, kdy na server nahrajeme novou verzi našeho webu. V tu chvíli je potřeba mít web server opravdu správně nastavený, aby s prohlížečem správně vykomunikoval kešování a i prohlížeč musí být velmi poctivý ve správě keše. Výsledek je, že tento process často nezafunguje úplně správně a některé assety se načtou z keše i když na serveru je již nová verze. V tu chvíli uživatel obdrží nějakou verzi stránky, která je namixovaná ze souborů z nové a staré verze. Tomuto se chceme za každou cenu vyhnout.

Nejspolehlivější technika, jak obejít keš v prohlížeči funguje tak, že soubor má stejný název, pokud jeho obsah zůstává stejný. Pokud se obsah souboru změnil, změní se i jeho název. Tím jej prohlížeč považuje za zcela nový soubor, která nemá v keši a musí jej tedy stáhnout. Této technice říkáme :term{cs="rozbití keše" en="cache busting"}.

### Digitální otisk

Webpack pro účely rozbití keše umožňuje k názvu vygenerovaného souboru připojit takzvaný *content hash*, nebo-li digitální otisk. Hashování je algoritmus, který umí vzít nějaký digitální obsah a vyrobit z něj unikátání "otisk", což je vždy nějaká směsice písmen a číslic, například 

```
43408ae1976241f58edc19288377b581
```

Platí, že stejná data, například soubor na disku, mají vždy stejný otisk. Naopak různá data mají otisk (až na vyjímky) různý. 

Ve Webpacku připojíme digitální otisk k názvu souboru pomocí `[contenthash]`. Napříkla pro obrázky:

```js
filename: 'img/[name]-[contenthash].[ext]'
```

