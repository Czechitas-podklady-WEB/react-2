---
title: Úkolníček - pokračování
demand: 3
---

Pokračujeme s aplikací Úkolníček, ve které jsme v předchozím cvičení vytvořili komponenty `Item` a `List`

## Komponenta Form

Nyní potřebujeme v aplikaci vytvořit formulář, kam půjde zadat nový úkol, který chceme přidat do seznamu.

1. Vytvoř novou komponentu `Form`. Komponenta zatím nebude mít žádné props, ale přidáme je později. Komponentu rovnou naimportuj a použij v `App`, abys v dalších krocích viděla, jak tvůj formulář vypadá.
2. V komponentě vytvoř formulář pomocí značky `<form>` a dovnitř přidej následující formulářové prvky:
   - `<input type="text" name="title" />` pro zadání názvu úkolu
   - `<textarea name="description" />` pro zadání popisu úkolu
   - `<button type="submit">Přidat</button>` jako odesílací tlačítko

   K prvkům přidej label s popiskem polí a ostatní náležitosti, které má přístupný formulář splňovat.
3. V komponentě založ funkci `handleSubmit` a nastavit ji, aby se volala při odeslání formuláře (událost `onSubmit`).
4. Ve funkci budeš potřebovat *event object*, abys mohla zabránit výchozí akci prohlížeče pomocí `e.preventDefault()`. To znamená, že tvoje funkce musí přijímat parametr `e` a ty mu musíš nastavit správný typ podle toho, jakou událost popisuje (tj. odeslání formuláře).
5. Za `e.preventDefault()` přidej zatím jen `console.log('odeslano')` a vyzkoušej, že po odeslání formuláře nedojde k obnovení stránky a že se v konzoli objeví text "odesláno".

## Stav pro formulářová pole

Hodnoty z formuláře chceme uložit do stavu, abychom při psaní do políček ve formuláři měli ve stavu vždy aktuální hodnoty.

1. Naimportuj z Reactu `useState` a vytvoř pomocí něj nový stav, který se bude jmenovat `formData`. Ve stavu bude uložený objekt, jehož vlastnosti se budou jmenovat stejně jako políčka ve formuláři. V našem případě to bude:
   ```ts
   {
     title: '',
     description: '',
   }
   ```
2. Správně bychom měli nadefinovat typ pro hodnotu, kterou budeme do stavu ukládat. Vytvoř *interface* s názvem `FormDataStructure`, který bude popisovat vlastnosti zmíněné v bodě 1.
3. Přidej vytvořený datový typ k `useState` tímto způsobem:
   ```ts
   const [formData, setFormData] = useState<FormDataStructure>({
     title: '',
     description: '',
   })
   ```
4. K oběma formulářovým polím přidej atribut `value` a nastav mu příslušnou hodnotu ze stavu. Aby se hodnoty uložené ve stavu propsaly do políček formuláře.
5. Vytvoř v komponentě funkci `handleChange`, se bude volat jako reakce na událost `onChange` u obou formulářových polí.
6. V komponentě budeš potřebovat *event object* a musíš mu nastavit správný typ. Protože se funkce volá jako reakce na událost `onChange` u prvku `<input>` a také prvku `<textarea>`, půjde o složený typ.
7. Zařiď, aby se hodnota formulářového pole zapsala do adekvátní vlastnosti objektu uloženého ve stavu `formData`.

   Název prvku, který událost vyvolal, budeš mít v `e.target.name`, a hodnotu formulářového pole v `e.target.value`.

   Vzpomeň si, že k vlastnostem objektů můžeš přistupovat nejen pomocí tečky `objekt.vlastnost`, ale také pomocí hranatých závorek `objekt['vlastnost']`.
8. Do funkce `handleSubmit`, která se volá při odeslání formuláře, doplň `console.log`, který vypíše obsah stavu `formData` do konzole. Ověř si, že když do formuláře něco vyplníš a formulář odešleš, objeví se ti v konzoli prohlížeče správné hodnoty.

## Bonus

Pokud se nudíš...

- Přidej do formuláře ještě roletku (select) nazvanou `priority`, ve které půjdou vybrat možnosti  *low*, *normal* a *high*. Standardně bude vybraná možnost normal.
- Uprav adekvátně i stav, kam se hodnota z roletky ukládá, a propoj stav s formulářovým prvkem.
- Vrať se k předchozím komponentám `Item` a `List` a obě uprav je tak, aby počítaly s tím, že každý úkol má nyní také nastavenou prioritu.
- V komponentě `Item` zařiď, aby se u názvu úkolu objevila:
  * modrá šipka `↓` pro nízkou prioritu
  * červená dvojšipka `↑↑` pro vysokou prioritu
  * u úkolů s normální prioritou se nezobrazuje nic
