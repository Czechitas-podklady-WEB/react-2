---
title: Test komponenty
demand: 3
---

Vytvoř jednoduchou komponentu `Collapse`. Komponenta bude mít dvě props: `title` a `description`. V komponentě bude stav, který bude určovat, zda je komponenta "sbalená" nebo "rozbalená".

Na počátku se v komponentě zobrazá pouze titulek. Při kliknutí na titulek se rozbalí textový popis pod titulkem. Při další kliknutí se pois znovu schová.

Představ si to jako komponentu, kterou použiješ při vytváření častých otázek a odpovědí (FAQ) na webu. Standardně vidíme jenom otázky, ale po kliknutí na otázku se nám ukáže odpověď.

Až budeš mít komponentu hotovou, bude zapotřebí ji otestovat. Proveď následující testy:

- Zobrazí komponenta správný text titulku a popisu podle předaných props?
- Po spuštění komponenty je vidět titulek a popis je schovaný?
- Když klikneme na titulek, je rozbalený popisek viditelný na stránce?
- Pokud klikneme ještě jednou, je popisek znovu schovaný?

### Nápověda

Záleží a tom, jak si komponentu naprogramuješ, ale pro testování, zda je nebo není zobrazený popisek můžeš použít metody `toBeInTheDocument()` (pokud text zobrazuješ/schováváš pomocí podmíněného zobrazení) nebo pomocí metody `toBeVisible()` (pokud popisek zobrazuješ/schováváš nastavováním CSS vlastnosti `display`).

Múžeš použít i negaci pomocí `not`, chceš-li zjistit že prvek neexistuje/není vidět.

```ts
expect(screen.findByText('description')).not.toBeInTheDocument();
```