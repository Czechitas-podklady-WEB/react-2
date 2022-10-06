---
title: Datluj.cz, fáze 2
demand: 3
---

V tomto cvičení zařídíme, aby po napsání slova ihned naskočilo slovo další.

1. Komponenta `Wordbox` musí nějakým způsobem informovat svého rodiče o tom, že uživatel správně napsal zadané slovo. Za tímto účelem přidejte do *props* v komponentě `Wordbox` callback `onFinish`.
1. V posluchači události `keyup` zařiďte, že pokud uživatel napsal správně poslední písmenko, místo nastavení stavu zavoláte rovnou funkci `onFinish`.
1. V komponentě `Stage` vyrobte funkci `handleFinish`, která nastaví stav `words` na prázdné pole. Předejte tuto funkci komponentě `Wordbox`. Takto zajistíme *unmount* komponenty po správném napsání slova.
1. Místo nastavování stavu na prázdné pole můžeme rovnou vygenerovat nové slovo – pomocí připravené funkce `generateWord`. Vygenerujte slovo délky 6. Dejte však pozor, že do stavu je vždy potřeba nastavit pole, tedy v tomto případě pole o jednom prvku.
1. Vyzkoušejte, že po napsání slova ihned přiskočí další. 
