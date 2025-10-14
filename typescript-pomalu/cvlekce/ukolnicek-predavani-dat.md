---
title: Úkolníček - předávání dat
demand: 4
---

Pokračujeme s aplikací Úkolníček, ve které jsme v předchozím cvičení vytvořili komponentu `Form`, kter data z formulářových polí ukládá do svého interního stavu a při odeslání formuláře je vypíše do konzole.

My ale potřebujeme, aby se při odeslání formuláře poslala data z formuláře do rodičovské `App`, kde nový úkol přidáme do seznamu úkolů.

1. V komponentě `App` vytvoř funkci `handleFormSubmit`, která bude jako parametr přijímat objekt s vlastnostmi `title` a `description`. Interface pro tento objekt máš už vytvořený v komponentě `Item`.
2. V `App` máš použitou komponentu `Form`, která zobrazuje formulář pro zadání nového úkolu. Ke komponentě `Form` přidej prop `onFormSubmit` a jako hodnotu do ní vlož funkci `handleFormSubmit`.
3. Uprav komponentu `Form` tak, aby přijímala prop `onFormSubmit`. Budeš pro komponentu muset vytvořit *interface* `FormProps`, kde správně nastavíš typ přijímané funkce.
4. Při odeslání formuláře v komponentě `Form` zatím vypisujeme data z formuláře do konzole. Zařiď aby se zavolala funkce `onFormSubmit` a jako parametr do ní pošli stejná data, jako do konzole. Tím zavoláme `handleFormSubmit` funkci v rodičovské komponentě `App` a pošleme do ní data z formuláře.
5. V komponentě `App` ve funkci `handleFormSubmit` vezmi data, která funkce dostane jako parametr, a přidej je do pole úkolů uloženého ve stavu `tasks`.
6. Vyzkoušej, že když vyplníš a odešleš fomulář, v seznamu úkolů se na konci objeví nový úkol.

## Bonus

- Zařiď, aby se po přidání nového úkolu vymazala formulářová pole.
- Pokud jsi to ještě neudělala, nastyluj formulář a seznam úkolů tak, aby vše vypadalo *krásně* a *cool* 😀
