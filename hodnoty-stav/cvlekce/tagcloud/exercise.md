---
title: Tagy
demand: 3
---

Vyrobte v Reactu komponentu `TagCloud`, která bude umět zobrazovat tagy jako na obrázku. 

::fig{src=assets/tagcloud.png size=70}

1. Založte novou React aplikace a vytvořte komponentu `TagCloud`.
1. Tagy uložte do stavu `tags` jako pole řetězců.
1. Přidejte do komponenty formulář s textovým políčkem, pomocí kterého bude možné zadat nový tag. Při odeslání formuláře přidejte nový tag na konec pole ve stavu `tags`. Dejte pozor, aby pole zůstalo immutable. Při přidání tagu vždy vyrobte pole nové pomocí spreadu. 
1. Přidejte do komponenty tlačítko, které odstraní první tag ze seznamu. Opět zachovejte imutabilitu stavu.