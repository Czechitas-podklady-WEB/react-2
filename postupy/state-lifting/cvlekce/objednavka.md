---
title: Objednávka
demand: 3
---

Pokračujte ve cvičení :i[kontrola emailu] z předchozí části lekce. Budeme se tvářit, že naše aplikace umožňuje přihlášení a že přihlášeného uživatele máme uloženého v kontextu. 

1. Přidejte do aplikace komponentu `Header`, která bude v pruhu nahoře na stránce zobrazovat jméno přihlášeného uživatele a tlačítko pro odhlášení. Jako jméno zatím použijte nějakou testovací hodnotu. 
1. Ve složce `src` vaší aplikace založte soubor `login-context.js` a v něm vytvořte nový React context s názvem `LoginContext`. Vytvořte také vlastní hook `useLogin`, který umožní váš context používat.
1. V komponentě `App` vytvořte stav `login`, který zatím bude natvrdo obsahovat hodnotu
   ```js
   {
     username: 'PanPokusnik',
     email: 'pokusnik.kokosnik@gmaill.com',
   }
   ```
1. Stále v komponentě `App` obalte veškerý její JSX obsah do komponenty `LoginContext.Provider` abychom mohlí náš context použít v celé aplikaci, tedy v komponentách `Header` i `OrderForm`. 
1. Prop `value` v provideru bude objekt s jednou vlastností `login`, která bude mít hodnotu branou ze stavu `login`.
1. V komponentě `Header` použijte připravený context pomocí funkce `useLogin`. Nastavte uživatelské jméno na `username` získané z contextu.
1. V komponentě `App` připravte funkci `logout`, která nastaví stav `login` na `null`. Tím odhlásíme aktuálního uživatele. Tuto funcki musíme vložit do našeho contextu, aby byla dostupná v komponentě `Header`. 
1. V komponentě `Header` vytáhněte z contextu funkci `logout` a zavolejte ji, když uživatel klikne na „Odhlásit“. Zároveň, pokud je v contextu hodnota vlastnosti `login` nastavena na `null`, místo tlačítka a uživatelského jména zobrazte zprávu „Nejste přihlášen“.
1. Proveďte podobnou věc s komponentou `OrderForm`. Pokud je stav `login` uvnitř `App` nastaven na `null`, komponentu `OrderForm` vůbec nezobrazujte. Uvnitř `OrderForm` použijte context a jako prvotní hodnotu stavu pro `EmailInput` nastavte uživatelův e-mail z contextu. Jde pouze o prvotní hodnotu, `EmailInput` dále bude přijímat vstup od uživatele.
