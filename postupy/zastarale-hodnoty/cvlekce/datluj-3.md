---
title: Datluj.cz, fáze 3
demand: 3
---

Zařídíme zpětnou vazbu pro uživatele zda napsal správné písmeno. Budeme chtít, aby slovo při chybě změnilo barvu.

1. V komponentě `Wordbox` vytvořte nový pravdivostní stav `[mistake, setMistake]`, který bude říkat, zda uživatel udělal překlep. Na začátku bude stav nastaven na `false`.
1. Pokud má stav `mistake` hodnotu `true`, vykreslete slovo s třídou `wordbox wordbox--mistake`. 
1. V reakci na událost `keyup` správně nastave stav `mistake` na `true` nebo `false` dle toho, zda uživatel napsal správné písmeno.
1. Vyzkoušejte, že aplikace funguje správně. 
1. Zamyslete se nad tím, zda nám hrozí problém se zastaráním stavu `mistake` a zdůvodněte, proč ano nebo proč ne. 