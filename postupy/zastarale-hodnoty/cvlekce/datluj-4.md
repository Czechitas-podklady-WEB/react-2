---
title: Datluj.cz, fáze 4
demand: 3
---

Přidáme možnost zobrazovat více slov najednou. 

Pokud na obrazovce vidím více slov, vždy píšeme první na seznamu. Takovému slovu řikáme, že je aktivní.

1. Do komponenty `Wordbox` přidejte prop `active`, která říká, zda je komponenta zrovna aktivní. Uvnitř `useEffectu` přidávejte/odebírejte posluchač události `keyup` pouze v případě, že prop `active` má hodnotu `true`. Tím zaručíme, že klávesy bude poslouchat pouze aktivní komponenta.
1. Přidejte prop `active` do seznamu závislostí pro `useEffect`, aby se při její změně efekt spustil.
1. V komponentě `Stage` budeme nyní ve stavu udržovat pole tří slov. Zařiďte, aby pouze první slovo v seznamu mělu prop `active` nastaveno na `true`. Vždy chceme psát pouze první slovo.
1. Ve funkci `handleSuccess` nyní musíme odstranit slovo ze začátku seznamu a vygenerovat nové slovo na konec, abychom si udržovali pořád stejný počet zobrazených slov.
1. Vyzkoušejte, že vaše aplikace správně funguje.