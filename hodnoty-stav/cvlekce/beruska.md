---
title: Beruska
demand: 3
---

Upravíme stav v Reactové hře, kde ovládáte berušku a chodíte s ní po rozkvetlé louce.

1. Udělejte fork [repozitáře](https://github.com/Czechitas-podklady-WEB/ladybug-zadani) s naprogramovanou hrou.
1. Pomocí `npm install` a `npm run dev` hru spusťte a vyzkoušejte, že funguje.
1. Pozice a orientace berušky je v komponentě `App` reprezentována třemi stavy. Z toho dva z nich se vždy mění společně. Navíc musíme berušce vždy předávat tři prop. To je nešikovné.
1. Upravte komonentu `App` tak, aby používala jeden objektový stav `ladybugState`. Zachovejte immutabilitu stavu a měňte jej pomocí spreadů.
1. Upravte komponentu `Ladybug` tak, aby místo tří prop používala pouze jednu, ve které očekává celý objekt.
1. Vyzkoušejte, že vaše hra funguje.
