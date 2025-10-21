---
title: Beruska
demand: 3
---

Upravíme stav v Reactové hře, kde ovládáte berušku a chodíte s ní po rozkvetlé louce.

1. Udělejte fork [repozitáře](https://github.com/Czechitas-podklady-WEB/ladybug-zadani) s naprogramovanou hrou.
1. Pomocí `npm install` a `npm run dev` hru spusťte a vyzkoušejte, že funguje.
1. Pozice a orientace berušky je v komponentě `App` reprezentována třemi stavy. Z toho dva z nich se vždy mění společně. Navíc musíme berušce vždy předávat tři prop. To je nešikovné.
1. Upravte komonentu `App` tak, aby místo tří samostatných stavů `posX`, `posY` a `direction` používala jeden objektový stav s názvem `ladybugState`, který bude obsahovat všechny tři vlastnosti.

   Pro stav si budete muset vytvořit *interface* a ten pak nastavit jako typ pro `useState`.

   Zachovejte immutabilitu stavu a uvnitř funkce `handleKeyUp` ho měňte pomocí spreadů.
1. Upravte komponentu `Ladybug` tak, aby místo tří prop používala pouze jednu, ve které očekává celý objekt. Bude třeba upravit interface `LadybugProps`. Snažte se vyhnout duplikování kódu (to se týká i definice typů a interfaců), nezapomeňte, že typy lze z jedné komponenty exportovat a do druhé importovat.
1. Vyzkoušejte, že po vašem zásahu hra funguje :)

