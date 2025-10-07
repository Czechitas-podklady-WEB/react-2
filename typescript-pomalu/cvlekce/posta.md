---
title: Pošta
demand: 3
---

Představ si, že budeš programovat e-mailového klienta, třeba něco jako Gmail. K tomu bude zapotřebí vytvořit několik různých typů.

## Založení projektu

1. Pomocí vite si vytvoř vlastní nový projekt pomocí `npm create vite@latest posta`. Jako framework vyber `Vanilla` a jako jazyk vyber `TypeScript`. V tomto a dalším cvičení nebudeme React potřebovat. Stačí nám čistě typescriptový projekt, kde potřebné věci budeme vypisovat do konzole.
2. Úplně vymaž ukázkový kód v souboru `main.ts` a přidej řádek:
   ```ts
   console.log('Pošta')
   ```
3. Smaž soubor `counter.ts`.
4. Spusť skript `npm run dev` a přesvedč se v prohlížeči, že v konzoli je text "Pošta". Stránka bude prázdná bílá, to je v pořádku.
5. Vytvoř si soubor `email.ts` a typy a funkce z následujících kroků vytvářej v něm.
6. Všechny typy (a později funkce) z tohoto souboru exportuj.
7. Proměnné s konrétními hodnotami zakládej vždy v souboru `main.ts`. Pokud budeš proměnné potřebovat nastavit typ, nejprve ho naimportuj ze souboru `email.ts`.


## Kontakt

Vytvoř interface `EmailContact`. Každý kontakt (to může být odesílatel nebo příjemce emailu) bude obsahovat celé jméno a emailovou adresu. Vlastnosti pojmenuj `name` a `email`.

V `main.ts` založ proměnnou s tímto typem a dej do ní nějakou hodnotu.

## Zpráva

Následně vytvoř interface `EmailMessage` pro emailovou zprávu. Každá zpráva by měla obsahovat následující údaje:
- `id` - číslo
- `from` - odesílatel, typ emailový kontakt
- `to` - příjemce, může jich být více, půjde o pole emailových kontaktů
- `cc` - kopie, opět jich může být více, pole emailových kontaktů
- `bcc` - skrytá kopie, stejně jako `cc`
- `subject` - předmět emailu
- `body` - obsah emailu
- `priority` - může nabývat hodnot `low`, `normal` nebo `high` (vytvoř si na to typ `Priority`, který bude hodnotu omezovat na tyto tři možnosti)
- `sendAt` - datum, jako typ použij `Date` s velkým "D" na začátku
- `isRead` - boolean, říká, zda je zpráva přečtená

V `main.ts` založ proměnnou s tímto typem a dej do ní nějakou hodnotu.

Do vlastnosti `sendAt` vlož hodnotu `new Date()`, což bude aktuální datum a čas, nebo můžeš zkusit datum ve tvaru `new Date('2025-12-24T18:30:00')`, pokud bys chtěla vložit třeba datum štědrovečerní večeře.

## Inbox

Jednotlivé e-mailové zprávy je potřeba mít uložené v poštovní schránce. Každá emailová schránka má svůj název, vlastníka a seznam zpráv.

Vytvoř typ `EmailInbox` jako pole emailových zpráv

V `main.ts` vytvoř proměnnou s tímto typem a vlož do ní několik zpráv. Můžeš použít zprávy uložené v proměnných, které jsi vytvořila v předchozích krocích.

## Bonus

Pokud se nudíš, můžeš zkusit doplnit následující:

- emaily mají přílohy, vytvoř si interface `EmailAttachment`, který bude mít vlastnosti
  * `filename` (jméno souboru)
  * `size` (velikost v bytech)
  * `contentType`, který bude obsahovat tzv. MIME type přiloženého souboru (viz. dokumentace MDN: [Common Media Types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/MIME_types/Common_types))
- pokud chceš, můžeš použít union values type a `contentType` přílohy omezit např. jen na obrázky GIF, JPEG, PNG a dokumenty DOCX a XLSX z Wordu a Excelu)
- do interface pro emailovou zprávu přidej vlastnost `attachments` a nastav ji tak, že může obsahovat pole příloh
