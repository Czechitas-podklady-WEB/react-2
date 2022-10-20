---
title: Emotikon
demand: 3
---

V tomto cvičení máme připravenou aplikaci, ve které si uživatel může vytvořit vlastní emotikon. Může si vybrat barvu, oči a ústa z předpřipravených variant, které se mu poskládají do celkového emotikonu.

1. Naklonujte si [repozitář](https://github.com/Czechitas-podklady-WEB/emoticon-zadani) se zadáním projektu. Prohlédněte si strukturu kódu a vyzkoušejte si fungování aplikace.
1. Při kliknutí na oči, ústa nebo barvu se pouze vypíše ID vybrané položky do konzole. Aplikaci musíme upravit, aby se změny projevili na emotikonu v levé části.
1. Protože aplikace je sestavená ze spousty komponent, které jsou do sebe vnořené na několika úrovních, víme už dopředu, že bychom se nevyhnuli *props drilling* - předávání props z komponenty do komponenty, a tam do další komponenty, atd. Proto raději použijeme context.
1. Ve složce `src` vytvořte soubor `setting-context.js` a v něm vytvořte nový *React context* s názvem `SettingContext`. Vytvořte i vlastní *hook* `useSettings`, který vám zjednodušší používání *contextu*.
1. V komponentě `App` vytvořte stav `settings`, který bude obsahovat objekt v následujícím tvaru:
   ```js
   {
     eyes: 1,
     mouth: 2,
     color: 3
   }
   ```
   Jednotlivé hodnoty budou představovat ID vybraného tvaru očí, úst a barvy pozadí.
   Hodnoty jsou uvedené v souboru `data.js` ve složce `src`, odkud je můžete importovat, kam bude potřeba.
1. V komponentě `App` obalte celý její JSX obsah do komponenty `SettingsContext.Provider`, která nám umožní *context* používat v celé aplikaci.
1. Do *prop* nazvané `value` nastavte *provideru* výchozí hodnotu contextu - sem uvložíme hodnotu stavu `settings`. To bude výchozí konfigurace emotikonu, když uživatel aplikaci spustí.
1. Upravte komponentu `Emoticon` tak, aby:
   - používala náš vytvořený *context*
   - podle hodnot v contextu zobrazovala správný emoticon
1. Když se podíváte na komponentu `Emoticon`, vidíte, že do ní na začátku importujeme natvrdo dva obrázky a v JSX používáme natvrdo hodnotu červené barvy. Natvrdo importované hodnoty odstraňte a použijte hodnoty ze souboru `/src/data.js`, které odpovídají IDčkům uloženým v *contextu*.
1. Aplikace by měla fungovat tak, že když v komponentě `App` změníte výchozí hodnoty *contextu*, zobrazí se odpovídající obličej.




