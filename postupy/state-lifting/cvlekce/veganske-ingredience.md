---
title: Veganské ingredience
demand: 3
---

Navážeme na aplikaci pro výběr ingrediencí na pizzu. Budeme chtít povolit pouze vegancské ingredience podle preference uživatele. Preference budeme míž uložené v contextu.

1. V projektu již známým postupem založte nový context `PrefsContext` včetně hooku `usePrefs`.
1. V komponentě `App` vytvořte pravdivostní stav `veganOnly` nastavený prvotně na hodnotu `true`. Obalte obsah aplikace providerem pro váš context a jako hodnotu contextu nastavte objekt s vlastností `veganOnly`.
1. Všimněte si, že CSS komponenty `Check` umožňuje udělat zaškrtávací tlačíko disabled. Uvnitř této komponenty tedy použijte context pomocí `usePrefs` a nechte zpřístupněné pouze vegnaské ingredience podle toho, jaká je hodnota vlastnosti `veganOnly`.
1. Podobně jako v předchozím cvičení vyrobte pro aplikaci hlavičku `Header`. Umožněte v ní uživatelí vybrat, zda chce všechny nebo jen veganské ingredience. Opět bude potřeba do contextu přidat funkci, pomocí které může komponenta `Header` změnit obsah contextu. 
