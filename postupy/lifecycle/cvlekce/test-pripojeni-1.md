---
title: Test připojení 1
demand: 3
---

V některých webových aplikacích se nám může hodit komponenta informující uživatele, že došlo k výpadku internetového připojení a aplikace tedy nemusí fungovat správně. Zkusíme společně takovou komponentu vytvořit. 

1. Udělejte si fork [repozitáře](https://github.com/Czechitas-podklady-WEB/test-pripojeni) se zadáním. Spusťte aplikaci a prozkoumejte zdrojový kód. 
1. Prohlédněte si komponentu `Offline`, která zobrazuje informaci zda jsem přpojeni k internetu. Zatím komponenta nefunguje a v podstatě nic užitečného nedělá.
1. Pomocí správného použití `useEffect` zařiďte, aby se při každém mountu této komponenty vypsalo do konzole `mounted`. Zkuste přepínat mezi stránkami _Domů_ a _Test Připojení_ a sledujte, kdy se vypíše zpráva do konzole. 
1. Zařiďte podobnou věc i pro unmount komponenty. Opět přepínejte mezi stránkami a sledujte, kdy se komponenta mountuje a kdy unmountuje. 
1. Uvnitř komponenty `Offline` napište funkci `handleOffline`, která bude reagovat na událost odpojení od internetu. Nastavte v ní stav `isOnline` na `false`. 
1. Při mountu komponenty zapojte tuto funkci jako posluchač události `offline` na objektu `window`:
   ```js
   window.addEventListener('offline', handleOffline);
   ```
1. Na stránce _Test připojení_ otevřete _Developer tools_ → _Network_ a přejděte do offline módu. Komponenta by měla zobrazit patřičnou zprávu. 
1. Podobným postupem jako výše vytvořte posluchač události `online` a zařiďte, aby se stav komponenty správně aktualizoval, pokud v developer tools přejdeme opět do online módu.
1. Vyzkoušejte, že vaše řešení správně funguje.

