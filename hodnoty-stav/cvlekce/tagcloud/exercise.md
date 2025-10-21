---
title: Tagy
demand: 3
---

Vyrobte v Reactu komponentu `TagCloud`, která bude umět zobrazovat tagy jako na obrázku.

::fig{src=assets/tagcloud.png size=70}

1. Založte novou React aplikaci pomocí Vite a TypeScriptu a vymažete výchozí vzorový kód.
1. Vytvořte novou komponentu `TagCloud`.
1. Vzhled tagů je bonus, ze začátku se zaměřte pouze na funkcionalitu, tj. klidně ať se tagy vypisují jen jako nenastylované textové řetězce.
1. Uvnitř komponenty vytvořte stav `tags`. Tagy budou ve stavu uložené jako pole textových řetězců.
1. Přidejte do komponenty formulář s textovým políčkem, pomocí kterého bude možné zadat nový tag. Při odeslání formuláře přidejte nový tag na konec pole ve stavu `tags`. Dejte pozor, aby pole zůstalo immutable. Nový tag do pole přidávejte pomocí spread operátoru.
1. Přidejte do komponenty tlačítko, které odstraní první tag ze seznamu. Opět zachovejte imutabilitu stavu.

## Bonus

1. Přidejte CSS styl, který napodobí vzhled tagů z obrázku.
1. Upravte formulář, stav, a celou unkcionalitu komponenty tak, aby:
   - tag už není jen textový řetězec, ale objekt který obsahuje **text** a **barvu**
   - upravte formulář, aby se při zadávání nového tagu kromě textu i vybírala barva ze selectu
   - tagy se zobrazují včetně barevného proužku na straně
1. Vytvořte komponentu pro jeden `Tag` a upravte komponentu `TagCloud` tak, aby ji používala.
