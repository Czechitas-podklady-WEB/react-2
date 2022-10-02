---
title: Datluj.cz, fáze 2
demand: 3
---

V tomto cvičení zařídíme, že uživatel bude moci napsat slovo zobrazené na obrazovce. 

1. Komponenta `Wordbox` musí nějakým způsobem informovat svého rodiče o tom, že uživatel správně napsal zadané slovo. Za tímto účelem přidejte do props v komponentě `Wordbox` callback `onSuccess`.
1. V posluchači uádlosti `keyup` zařiďtě, že pokud uživatel napsal správně poslední písmenku, místo nastavení stavu volejte rovnou funkci `onSuccess`.
1. V komponentě `Stage` vyrobte funkci `handleSuccess`, která nastaví stav `words` na prázdné pole. Předejte tuto funkci komponentě `Wordbox`. Takto zajistíme unmount komponenty po správném napsání slova. 
