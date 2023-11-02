---
title: Karaoke - přehrávač
demand: 3
---

Podle instrukcí níže vyrobte aplikaci, která bude přehrávat písničku a zobrazovat její slova. Zároveň bude zvýrazňovat řádky s textem, který se právě zpívá.

1. Naklonujte si repozitář s [kostrou aplikace](https://github.com/Czechitas-podklady-WEB/karaoke-zadani). Tento repozitář budeme používat pouze jako zdroj HTML, CSS a dalších souborů potřebných pro naši aplikaci.
1. Na GitHubu si založte vlastní repozitář s kostrou Reactové aplikace pomocí `npm init kodim-app@latest .`.
1. Smažte veškerý obsah prvku `.container`. Vložte do aplikace soubor s CSS styly ze zadání. Nezapomeňte zkopírovat také obrázek pozadí.
1. Vytvořte komponentu `Player`, která bude obsahovat `audio` element a tlačítko pro ovládání přehrávání. Pro komponentu vytvořte vlastní složku se styly a obrázky tak, jak jste zvyklí.
1. Komponenta `Player` nechť má *prop* s názvem `src`, do které se pošle soubor s písníčkou. Komponenta tuto nahrávku předá prvku `audio`. Písničku *Lemon tree* stačí vložit do složky `public` aby ji server dokázal najít.
1. V komponentě `Player` zařiďte, aby se tlačítko přehrávače na kliknutí přípínalo mezi ikonami *spustit* a *pauze*. Použijte k tomu stav s názvem `playing`. Prozatím nebudeme nic přehrávat, jen přepínat ikonu na tlačítku.
1. Stále v komponentě `Player` vyrobte *ref* obsahující element audio přehráveče. Pomocí efektu závíslého na stavu `playing` zařiďte, aby přehrávač přehrával nebo přestal přehrávat. Nyní by mělo být možné přehrávač ovládat klikáním na tlačíko.
