---
title: Pizza ingredience
demand: 3
---

V tomto cvičení vdechneme život aplikaci, která umožňuje vybrat si různé ingredience na objednávanou pizzu. Uživatel uvidí seznam ingrediencí a bude moci si zaškrtnout, které ingredience chce na své pizze.

1. Naklonujte si [repozitář](https://github.com/Czechitas-podklady-WEB/pizza-zadani) se zadáním projektu. Prohlédněte si strukturu kódu a vyzkoušejte si fungování aplikace. 
1. Budeme chtít abychom dokázali zobrazit počet zašrktnutých ingrediencí a jejich celkovou cenu. Všimněte si, že komponenta `Check` je *uncontrolled*, spravuje tedy svůj vlastní stav.
1. Jako první krok povyšte stav komponenty `Check` o jednu úroveň nahoru, tedy do komponenty `Topping`. Komponenta `Check` tak bude mít *props* `checked` a `onChange`.
1. Abychom dokázali zobrazit počet zaškrnutých ingrediencí, bude potřeba povýšit stav až do komponenty `ToppingsSelect`. Podobně jako v lekci k tomu využijte připravené pole toppings. Každý objekt obsahuje vlastnost `selected`, který by se měla měnit v závislosti na tom, co uživatel zaškrtnul.
1. Rozšiřte aplikaci tak, aby zobrazovala také celkovou cenu.
