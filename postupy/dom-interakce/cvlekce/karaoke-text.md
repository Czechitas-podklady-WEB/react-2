---
title: Karaoke - text
demand: 3
---

Budeme pokračovat v předchozím cvičení. Vytvoříme komponentu pro zobrazování textu píšničky a naučíme ji scrollovat na aktuální řádek textu.

1. V repozitáři se zadáním najdete soubor `lyrics-lines.js` obsahujcí text písničky *Lemon Tree*. Vložte tento soubor do `src` vašeho projektu.
1. Vytvořte komponentu `Lyrics`, která v *prop* s názvem `lines` bude očekávat data ve formátu jaký vídíte v souboru `lyrics-lines.je`. Komponenta zobrazí jednotlivé řádky textu pod sebou jak je naznačeno v repozitáři se zadáním.
1. V souboru hlavní komponenty `App` importujte objekt ze souboru `lyrics-lines.js` a předejte jej komponentě `Lyrics`. Nyní byste na stránce měli vidět text celé písničky.
1. Komponenta `Lyrics` bude mít ještě jednu *prop* s názvem `currentLineIndex`. Ta bude udávat, který řádek textu má být zvýrezněn pomocí CSS třídy `current-line`.
1. V komponentě `App` vytvořte stav uchovávající index právě aktivního řádku. Zatím jej nastavte na libovolné číslo. Stav předejte komponentě `Lyrics` a vyzkoušejte, že dokážete zvýraznit řádek na libovolném indexu.
1. Nyní budeme chtít, aby komponenta `Lyrics` odscrollovala na zvýrazněný řádek. K tomu bude potřeba založit *ref*, kterou nastavíme na aktuálně zvýrazněný řádek.
1. Vyrobte efekt, který byde reagovat na změnu *prop* `currentLineIndex`. Pomocí vámi vytvořené *ref* zavolá na elementu s aktuálním řádkem metodu `scrollIntoView`. Aby metoda hladce odscrollovala na začátek rodičovského prvku, poradíme, že je ji potřeba zavolat takto:
   ```js
   scrollIntoView({
     block: 'start',
     inline: 'nearest',
     behavior: 'smooth',
   });
   ```
1. Vyzkoušejte, že když v hlavní komponentě `App` změníte stav s aktulním indexm řádku, komponenta `Lyrics` odscrolluje na správný řádek a zvýrazní jej.
