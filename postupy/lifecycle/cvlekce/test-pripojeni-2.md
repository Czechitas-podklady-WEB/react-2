---
title: Test připojení 2
demand: 3
---

V řešení předchozího cvičení nastává nepříjemná situaci, která není hned na první pohled patrná. V následujícíh krocích ji vyřešíme. Pokračujte v řešení z předchozího cvíčení.

1. Do koponenty `Offline` přdejte `useEffect`, který se bude spouštět při každém renderu komponenty. 
1. Zkuste nyní několikrát přejít mezi stránkami _Domů_ a _Test připojení_. Poté na stránce _Test připojení_ vyzkoušejte odpojení od internetu. V konzoli uvidíte, že komponenta se vyrenderovala zbytečně několikrát po sobě. Zamyslete se, proč taková situace nastává.
1. Toto je prosto na zamyšlení...
1. Situace nastává proto, že při každém mountu kouponenty se vytvoří úplně nové funkce `handleOffline` a `handleOnline`, které se připojí jako posluchače událostí. Na událost tak reagují všechny funkce ze všech mountů, které kdy nastaly. 
1. Abychom se vyhnuli vícenásobnému renderu, musíme posluchače události při unmountu komponenty zase odstranit voláním `window.removeEventListener`. Proveďte tedy při unmountu nezbytný úklid a vyzkoušejte, že komponenta se pak i po několika mountech překresluje pouze jednou. 
