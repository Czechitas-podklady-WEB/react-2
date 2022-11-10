---
title: Roletka
demand: 4
---

Základní formulářové prvky v HTML jdou často špatně stylovat a pokud to design aplikace vyžaduje, musíme si často naprogramovat svoje vlastní. My si v tomto příkladu vytvoříme vlastní rozbalovací roletku nahrazující formulářový prvek `<select>`.

1. Naklonujte si repozitář s [připravenou aplikací](https://github.com/Czechitas-podklady-WEB/roletka-zadani). Nezapomeňte na `npm install`.
1. Aplikaci spusťte a prozkoumejte zdrojový kód. Uvidíte, že v aplikaci je vytvořená komponenta `Dropdown`, do která jako *props* můžeme poslat:
   - `placeholder` - výchozí text, který se v záhlaví roletky zobrazí, když není vybraná žádná položka.
   - `options` - pole textových řetězců, které představují jednotlivé volby v roletce.
   - `selected` - textový řetězec, odpovídající aktuálně vybrané položce. Ppokud je vybraná nějaká položka, tak se zobrazí v záhlaví roletky místo výchozího textu.
   - `onChange` - callback funkce, která se zavolá, když uživatel v roletce něco vybere. Do funkce se jako parametr pošle vybraná hodnota.
1. Všimněte si, že komponenta není hotová. Naše roletka zůstává stále otevřená. Seznam možností (prvek s třídou `dropdown__list`) musíme buď skrýt nebo zobrazit, podle toho, zda má být roletka zavřená nebo otevřená.
1. Potřebujeme zařídit následující:
   - roletka bude ve výchozím stavu zavřená (`dropdown__list` je skrytý)
   - kliknutím na záhlaví roletky `dropdown__header` ji otevřeme nebo zase zavřeme
   - kliknutím na vybranou položku se nejen odešle vybraná hodnota do rodičovské komponenty (to už funguje), ale roletka se zároveň i zavře
   - kliknutí kamkoliv mimo roletku by ji také mělo zavřít
1. První tři odrážky ze seznamu výše by pro vás už neměly být těžké. Vytvořte si v komponentě stav, zda je roletka otevřená nebo ne. Podle hodnoty stavu zobrazujte nebo nezobrazujte prvek s třídou `dropdown__list`. Reagujte na kliknutí na `dropdown__header` a přepínejte hodnotu stavu. Nezapomeňte přidat nastavení stavu na správnou hondotu i do funkce, která se spouští při kliknutí na položku v seznamu.
1. Poslední bod bude obtížnější a budeme muset trochu přemýšlet. Jak uděláme, aby se roletka zavřela, když klikneme kamkoliv mimo ni?


