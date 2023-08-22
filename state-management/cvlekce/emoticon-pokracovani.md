---
title: Emotikon - pokračování
demand: 4
---

Pokračujte s kódem z předchozího cvičení. Nyní musíme do aplikace.

1. Aplikace nám správně zobrazuje obličej, který máme nastavený jako výchozí hodnotu v kontextu. My ale samozřejmě chceme, abychom mohli obličej i měnit pomocí záložek v pravé straně aplikace.
1. Jednotlivé záložky tvoří komponenty `EyesSelector`, `MouthSelector` a `ColorSelector`. Zaměřme se nyní na výběr očí, ale postup bude stejný pro všechny tři komponenty.
1. Uvnitř komponenty importujeme pole dat ze souboru `src/data.js`. Pomocí mapování zobrazuje pro každou položku v poli obrázek představující jeden typ očí.
1. Přidejte do komponenty náš *context* a získejte z něho hodnotu pro vybrané oči. Nezapomeňte, že hodnota je ID očí, ne jejich index v poli.
1. Na obrázek, jehož ID odpovídá hodnotě `eyes` z *contextu* přidejte třídu `active`, abychom viděli, které oči jsou právě vybrané. Pokud máte vše správně, měl by se kolem vybrané položky objevit tlustší černý rámeček.
1. Naše komponenta zatím funguje tak, že při kliknutí na obrázek se zavolá funkce `handleClick`, která do konzole vypíše ID vybraného obrázku. My nechceme ID vypisovat do konzole, ale potřebujeme jeho hodnotu dostat do stavu `settings` uvnitř komponenty `App`. Tento stav se totiž propíše do hodnoty našeho contextu a my budeme mít vybrané oči přístupné v celé aplikaci.
1. Vytvořte v `App` funkci `changeEyes`, která jako parametr přijme hodnotu (ID vybranýchočí) a nastaví jí do vlastnosti `eyes` stavu `settings`.
1. Tuto funkci přidejte do contextu, aby k ní měli přístup všechny komponenty, které ji budou potřebovat.
1. Uvnitř komponenty `EyesSelector` funkci z contextu naimportujte a zařiďte, aby se zavolala se správným parametrem, když se klikne na obrázek očí.
1. Pokud jste vše udělali správně, můžete nyní klikáním na různé oči měnit hlavní emotikon.
1. Opakujte celý postup i pro ústa a barvy.

