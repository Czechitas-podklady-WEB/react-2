---
title: Pošta
demand: 4
---

Pokračuj v předchozím příkladu, kde jsi vytvořila typy pro emailovou zprávu a schránku.

Vytvoř postupně následující funkce:
1. `getUnread` - funkce bude jako parametr přijímat emailovou schránku typu `Inbox` a vrátí **pole** nepřečtených zpráv typu `EmailMessage`.

   Pro výběr nepřečtených zpráv použij metodu pole `filter`.

   V `main.ts` funkci zavolej, výsledek vypiš do konzole a přesvědč se, že se ti vrátily jen nepřečtené zprávy.

2. `markAsRead` - funkce bude jako parametr přijímat dvě hodnoty:
   - emailovou schránku typu `Inbox`
   - `id` zprávy (číslo), kterou chceme označit jako přečtenou.

   Funkce vrátí **nové pole** (typu `Inbox`, tj. pole emailových zpráv), kde bude zpráva s předaným `id` označená jako přečtená.

   Pro vytvoření nového pole se zprávami použij metodu pole `map`.

   V `main.ts` funkci zavolej. Jako parametr předej id zprávy, o které víš, že je nepřečtená. Výsledné pole vypiš do konzole a podívej se, zda je zpráva označená jako přečtená.


## Bonus

Pokud už se nudíš, vytvoř navíc ještě funkci

3. `findBySender`, která jako parametr bude přijímat:
   - poštovní schránku typu `Inbox`
   - emailovou adresu (string)

   Najdi ve schránce všechny zprávy, které ve vlastnosti `from` mají uvedenou emailovou adresu, a vrať z funkce jejich pole (tj. pole zpráv typu `EmailMessage`).

   V `main.ts` funkci vyzkoušej a nech si vyhledat zprávy s konkrétním odesílatelem.
