---
title: Datluj.cz, fáze 1
demand: 3
---

V tomto cvičení zařídíme, že uživatel bude moci napsat slovo zobrazené na obrazovce. 

1. Udělejte si fork [repozitáře](https://github.com/Czechitas-podklady-WEB/datluj.cz) se zadáním celého projektu. Nainstalujte závislosti a prohlédněte si strukturu projektu. Po spuštění stránky uvidíte na obrazovce jedno slovo vykreslené pomocí komponenty `Wordbox`. 
1. Prostudujte si zdrojový kód a seznamte se s tím, jak aplikace funguje.
1. Prohlédněte si kompnentu `Stage`. Prozatím si navšímejte funkce `generateWord`, tu máme připravenou na později. Ve stavu komponenty máme uloženo pole slov místo přímo jednoho řetězce. To je také příprava na později. Dokud neřekneme jinak, budeme pracovat s jednoprvkovým polem.
1. Upravte komponentu `Wordbox` tak, že pověsíte posluchače události `keyUp` na `document`. Pokud uživatel napsal správně první písmenko slova, toto písmenko ze slova umažte. Takto pokračujte dokud uživatel nenapíše celé slovo. V posluchači budete používat stav `lettersLeft` a bude potřeba se vyhnout jeho zastarávání (stale state). Použijte probíranou techniku, kdy posluchače události měníte svépomocí. Do závislostí `useEffectu` bude potřeba přidat stav `lettersLeft`. 
1. Jakmile uživatel napíše správně celé slovo na stránce zůstane viset prázdná komponenta `Wordbox`. Nechejte ji zatím viset. 
