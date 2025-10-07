---
title: Úkolníček - pokračování
demand: 3
---

Pokračujeme s aplikací Úkolníček, ve které jsme v předchozím cvičení vytvořili komponenty `Item` a `List`

## Komponenta Form

Nyní potřebujeme v aplikaci vytvořit formulář, kam půjde zadat nový úkol, který chceme přidat do seznamu.

1. Vytvoř novou komponentu `Form`. Komponenta zatím nebude mít žádné props, ale něco přidáme později.
2. V komponentě vytvoř formulář pomocí značky `<form>` a dovnitř přidej následující formulářové prvky:
   - `<input type="text" name="title" />` pro zadání názvu úkolu
   - `<textarea name="description" />` pro zadání popisu úkolu
   - `<button type="submit">Přidat</button>` jako odesílací tlačítko

   K prvkům přidej label s popiskem polí a ostatní náležitosti, které má přístupný formulář splňovat.
3. V komponentě založ funkci `handleSubmit` a nastavit ji, aby se volala při odeslání formuláře (událost `onSubmit`).
4. Ve funkci budeš potřebovat *event object*, abys mohla zabránit výchozí akci prohlížeče pomocí `e.preventDefault()`.
