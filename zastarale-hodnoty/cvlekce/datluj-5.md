---
title: Datluj.cz, fáze 5
demand: 3
---

Přidáme do naší vyúkové hry počítání chyb. Vždy, když komponenta `Wordbox` zaznamená chybu, dá o tom vědět svému rodiči a ten aktualizuje svůj stav. 

V této chvíli věříme, že jste dostatečně zkušení na to, aby vám popis výše stačil k dokončení cvičení. Pokud se přesto cítíte nejistě, můžete následovat podrobný popis:

1. Do komponenty `Stage` přidejte stav `[mistakes, setMistakes]` s prvotní hodnotou `0`. Zobrazte stav na příslušném místě v komponentě.
1. Přidejte do komponenty `Wordbox` callback `onMistake`, který bude komponentu `Stage` informovat o překlepu.
1. V komonentě `Stage` vytvořte handler `handleMistake`, který svýší stav `mistake` o jedna.
1. V komponentě `Wordbox` zavolejte funkci `onMistake` pokaždé, když nastane chyba. To je potřeba udělat v handleru události `keyup`. Pravděpodobně tušíte, že nám takto hrozí zastarání *prop* `onMistake`.
1. V komponentě `Wordbox` přidejte *prop* `onMistake` do závislostí v `useEffectu`, aby nám nezastarala. 
1. Vyzkoušejte, že aplikace správně funguje.
