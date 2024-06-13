---
title: Registrační formulář
demand: 3
---

1. Začněte s čistým projektem vytvořeným pomocí `npm create vite my-app -- --template react-ts`.
1. Do projektu nainstalujte knihovnu Formik.
1. Vytvořte komponentu, která bude obsahovat registrační formulář do e-shopu. Formulář bude obsahovat:
   * Registrační údaje
     - **email** - povinné pole, max 30 znaků
     - **heslo** - povinné pole, max 50 znaků
     - **potvrzení heslo** - povinné pole, max 50 znaků
     - **telefon** - povinné pole, max 20 znaků
   * Fakturační údaje
	   - **jméno** - jméno a přijmení nebo název firmy, volitelné pole, max 40 znaků
     - **ulice** - volitelné pole, max 30 znaků
     - **město** - volitelné pole, max 20 znaků
     - **psč** - volitelné pole, max 6 znaků
   * Ostatní
     - **preferované odběrné místo** - výběr z alespoň 5 českých měst (select)
     - **odběr newsletteru** - dva radiobuttony, ano/ne
     - **poznámka** - textarea pro libovolný komentář, nepovinné pole, max. 100 znaků
   * Souhlas
	   - **souhlas se zpracováním osobních údajů** - checkbox, musí být zaškrtnutý, jinak nelze uživatele zaregistrovat
1. Nastavte pole tak, aby se pro všechna pole správně provedla validace.
1. Při odeslání formuláře pouze hodnoty vypište do konzole.
1. Volitelně se pokuste formulář hezky nastylovat.



