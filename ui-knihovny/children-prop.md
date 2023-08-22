## Skládání komponent

React je založený na práci s komponentami. Komponenty jdou do sebe vnořovat a díky tomu mohou být naše komponenty malé funkční celky, ze kterých skládáme větší díly celé naší aplikace. My jsme doposud vždy věděli, jakou konkrétní komponentu chceme použít uvnitř jiné komponenty a mohli jsme ji proto jednoduše naimportovat a v rodičovské komponentě použít.

Jsou ale situace, kdy naše rodičovská komponenta dopředu neví, jaké jiné komponenty (nebo obecně JSX kód) bude obsahovat. Představte si například, že vytváříte komponentu Sidebar - pruh na straně webu, do kterého můžete skládat další *widgety*. Může v nich být třeba kalendář akcí, odkazy na nejnovější články, informace o počasí, reklama, atd. Obsah Sidebaru neznáme dopředu - může se měnit v závislosti na nastavení naší aplikace (např. v administraci webu).

Naše komponenty jsme zatím vždy používali jako nepárové značky, do kterých jsme posílali props.

```jsx
<AlmostPerfectComponent title="Skvělá komponenta" />
```

Nyní potřebujeme napsat komponentu Sidebar tak, aby akceptovala a uměla zobrazit jakékoliv potomky do ní pošleme. Třeba takto:

```jsx
<Sidebar title="Můj sidebar">
  <Events />
  <News />
  <Weather />
</Sidebar>
```

### Prop Children

V Reactu je to naštěstí velmi jednoduché. V každé komponentě je k dispozici speciální prop nazvaná `children`, která obsahuje všechny do komponenty vnořené potomky. To mohou být další komponenty nebo třeba i obyčejné HTML značky (nebo přesněji, JSX elementy).

Obsah prop `children` pak můžeme přímo vypsat do výstupu komponenty.

```jsx
const Sidebar = ({children}) => {
  return (
    <aside className="sidebar">
      <h2>Sidebar</h2>
      { children }
    </aside>
  );
}
```

Prop `children` tedy budeme využívat ve chvíli, kdy potřebujeme napsat komponentu, která má obalit další prvky nebo komponenty, ale my dopředu nevíme, jaké to budou.

Časté použití jsou například různá dialogová okna, sidebary, nastylované boxy, ve kterých může být libovolný obsah, nebo obecné komponenty, které například řídí rozložení prvků na stránce.

