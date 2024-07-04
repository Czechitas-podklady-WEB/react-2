---
title: Test komponenty
demand: 3
---

### Příprava

1. Založte si nový projekt pomocí Vite a vymažte vzorový kód, abyste dostali prázdnou reactí aplikaci.
1. Nainstalujte a nastavte Vitest podle návodu na předchozích stránkách.

### Část 1: Unit test funkce

1. V projektu si vytvořte složku `utils` a v ní soubor `birthdays.ts`. Pro jednoduchost nebudeme používat žádné API, ale vytvoříme si v souboru natvrdo pole s několika jmény a daty narození, např.:
   ```ts
	 const birthdays = [
		 {
			 name: 'Jana',
			 birthday: '17. 3. 1996',
		 },
		 {
			 name: 'Petr',
			 birthday: '21. 9. 2001',
		 },
		 {
			 name: 'Alena',
			 birthday: '4. 5. 1983',
		 },
	 ]
	 ```
1. Naprogramujte funkci `getBirthday`, která jako parametr dostane jméno a vrátí narozeniny daného člověka. Pokud jméno v seznamu neexistuje, funkce vrátí hodnotu `undefined`.
1. Vytvořte unit test, který otestuje, zda se funkce chová správně v obou případech.

### Část 2: Testování komponenty

1. Vytvořte komponentu `Birthday`, která jako *props* bude přijímat `name` a jako výstup bude zobrazovat text *Jana má narozeniny 17.3. 1996.* Pro zjištění data narození použijte dříve vytvořenou funkci.
1. V případě, že funkce vrátí jako datum narození `undefined` (tj. jméno není v seznamu), zobrazí se text *Nevíme, kdy má Jana narozeniny.*
1. Napište pro komponentu test, který ověří, že se komponenta správně vykresluje a obsahuje správný text podle toho, zda použijete v seznamu existující nebo neexistující jméno.
