---
title: Úkolníček
demand: 3
---

Budeme vytvářet jednoduchou aplikaci pro evidenci úkolů. Klasický ToDo list, který musí každý programátor za život naprogramovat alespoň 137x.

## Založení projektu

1. Tentokrát už použijeme React, takže si opět založ zcela nový projekt pomocí `npm create vite@latest ukolnicek` a v následujících volbách vyber `React` a potom `TypeScript`.
2. Z komponenty App odstraň výchozí ukázkový kód a nech si tam třeba jenom nadpis.
3. Projekt spusť, ať víš, že všechno funguje. (Uvidíš jenom nadpis.)
4. Vytvoř si složku `components`, do které budeš později dávat nové komponenty.


## Komponenta Item

1. Vytvoř novou komponentu `Item`. Soubory pojmenovávej s příponou `.tsx`.
2. Komponenta bude přijímat následující props:
   - `title` - název úkolu
   - `description` - popis úkolu
   - `done` - boolean, zda je úkol splněný nebo ne
3. Vytvoř interface `ItemProps` a nastav ho jako typ pro props komponenty.
4. Komponenta zobrazí div, ve kterém budou dva odstavce. V prvním odstavci bude tučným písmem název úkolu. Ve druhém odstavci bude popis úkolu.
5. Vytvoř si v CSS soubor pro komponentu, naimportuj ho do komponenty a přidej do něj třídu `.done` a nastav do ní přeškrtnuté písmo `text-decoration: line-through;`.
6. Pokud má prop `done` hodnotu `true`, přidej divu třídu `done`.
7. Naimportuj komponentu do hlavní App a zkus ji použít. Vyzkoušej si, že TypeScript hlásí chybu, když neuvedeš všechny potřebné props nebo do nich dáš hodnoty nevhodného typu.
8. **BONUS:** Pokud chceš (a máš čas) můžeš v CSS nastavit pro div i nějakou výchozí třídu, která mu přidá hezký vzhled, např. rámeček, padding, apod.


## Komponenta List

1. Vytvoř komponentu `List`, která bude zobrazovat seznam položek v úkolníčku.
2. Komponenta bude přijímat dvě props:
   - `title` - název seznamu (např. "Domácí práce", "Nákup" apod.)
   - `items` - pole položek v seznamu, každá položka je typu `ItemData`, který je nadefinovaný v předchozí komponentě, budeš ho odtamtud potřebovat naimportovat
3. Vytvoř s těmito vlastnostmi interface `ListProps` a nastav ho jako typ pro props komponenty.
4. Zařid, aby se pomocí `map` v komponentě zobrazil seznam položek, tj. přemapuj pole `items` na seznam komponent `Item`.
5. Jako `key` při mapování použij vlastnost `title`. Není to ideální, ale nemáme nic lepšího 😀
