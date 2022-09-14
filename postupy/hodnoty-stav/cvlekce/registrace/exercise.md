---
title: Registrace
demand: 3
---

Vytvořte v Reactu komponentu `Registraction`, která bude představovat registrační formulář do nějaké webové aplikace

::fig{src=assets/registrace.png size=70}

1. Založte React project a komponentu `Registration`. 
1. V komponentě vytvořte jeden stav `user`. Ve stavu bude objekt reprezentující všechan data ve formuláři. Objekt bude mít následující strukturu:
   ```js
   {
      username: '',
      email: '',
      password: '',
      passwordConfirm: '',
   }
   ```
1. Provažte obsah formuláře se stavem `user`.
1. Budeme chtít, aby se ve formuláři automaticky vyplnilo políčko User Name, pokud uživatel zadá validní email a pokud je User Name prázdné. Validní email poznáme tak, že obsahuje zavináč. Do User Name se pak vyplní část emailu před zavináčem. 
1. Tlačítko pro odeslání formuláře nechť vypíše stavový objekt do konzole. 