---
title: Karaoke - dokončení
demand: 4
---

Je před námi největší dobodružství: propojit přehrávání se zobrazováním aktuální řádky textu.

1. Nejdříve musíme zařídit, aby komponenta `Player` reportovala aktuální čas přehrávání. Na element `audio` můžeme použít událost `onTimeUpdate`, která se při přehrávání vyvolává několikrát za vteřinu. K aktuálnímu času ve vteřinách se pak dostaneme pomocí `e.target.currentTime`. Zkuste prozatím aktuální čas vypisovat do konzole.
1. Do přehávače přidejte *callback prop* `onTimeUpdate`. Tuto funkci zavoleje při každé změně času během přehrávání. Předejte jí jako parametr přímo hodnotu aktuálního času ať se rodičovská komponenta nemusí trápit s vytahováním času z objektu události.
1. V komponentě `App` nastave stav s indexem aktuálního řádku na výchozí hodnotu `-1`. Vytvořte funkci `handleTimeUpdate`, která bude reagovat na změnu času přehrávače. Nyní potřebujeme z aktuálního času spočítat index aktuálního řádku textu písně. Dobře si přečtěte následující popis:
   
   *Aktuální index je index posledního z těch řádků, jejichž čas je ostře menší naž aktuální čas přehrávače*

  Na základě tohoto popisu ve funkci `hadleTimeUpdate` spočíteje aktuální index a nastavte jej do stavu, který se předává komponentě `Lyrics`.
1. Jelikož událost `timeupdate` se vyvolává mnohokrát za vteřinu, je rozumné měnit index ve stavu pouze v případě, že se liší od předchozí hodnoty. Zabráníme tak překreslení celé aplikace mnohokrát za vteřinu.

Nyní by měla vaše aplikace fungovat. Při spuštění přehrávání by měl text průběžně scrollovat na zvýrazněný aktuální řádek textu písně. 
