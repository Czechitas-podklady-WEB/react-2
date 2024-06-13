---
title: Cvrlikání
demand: 3
---

Úkolem tohoto cvičení je vytvořit velmi jednoduchou aplikaci napodobující Twitter. Uživatel do textového políčka zadá krátký text a ten se poté objeví v seznamu zveřejněnýcn zpráv.

Abychom nemuseli používat backend, situaci si zjednodušíme tím, že budeme zobrazovat pouze zprávy zadané jedním uživatelem.

Návrh HTML a CSS máte k dispozici [zde](https://github.com/Czechitas-podklady-WEB/cvrlikani-zadani). Můžete jej přesně následovat, nebo se jím pouze inspirovat.

1. Na svém GitHubu si založte repozitář `cvrlikani`. Naklonujte jej k sobě do počítače.
1. V naklonované složce založte nový React projekt s ESLintem pomocí
   ```
   npm create vite@latest .
   ```
   Vyberte projekt v Reactu s TypeScriptem.
1. Podle návodu na předchozí stránce si do projektu přidejte Prettier a nastavte si ho dle svých představ.
1. Rozmyslete si, jak bude váš projekt strukturovaný.
   - Jaké bude obsahovat komponenty? Jak se budou jmenovat?
   - Jaké budou vaše komponenty obshovat stavy? Jaká data budete ve stavech ukládat?
   - Jak spolu budou komponenty komunikovat?
1. Jakmile máte v hlavě dobrý plán toho, co je třeba udělat, postupujte podle něj a naprogramujte funkční aplikaci.
1. Během vývoje se řidťe ESLintem a dbejte na dobrou kulturu kódu. Všímejte si, kde vám Prettier formátuje kód. Je to proto, že se o hezké formátování kódu obvykle moc nestaráte? Nebo má Prettier jen jiný názor na to, jak by měl kód vypadat? Zkusíte si konfiguraci upravit, aby kód vypadal podle vašich představ? (Ne vždy to jde.)

## Nápady na rozšíření:

- Umožněte přidávat ke zprávám lajky. Ignorujte fakt, že si svůj vlastní příspěvek můžete lajkovat několikrát.
- Umožněte některé zprávy označit záložkou, abyste se k takto označeným příspěvkům mohli vrátit.
- Přidejte možnost smazat nepohodlnou zprávu.
- Přidejte další stránky, na kterých uvidíte přehled svých zpráv, které jste si uložili do záložek nebo jim dali lajk.
