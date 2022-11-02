## Přístup k DOMu

Před tím, než jsme začali používat React jsme interaktivitu stránky zajišťovali přímou manipulací s DOMem. React se nás naopak snaží od DOMu co nejvíce odstínit. V ideálním Reactovém světě bychom s DOMem vůbec nepřišli do styku a nechali bychom ho umouněným dělníkům vanilla JavaScriptu. Svět však dokonalý není a i v Reactu čas od času potřebujeme přistup k DOM elementům. 

Co v Reactu určitě dělat nechceme je přistupovat k DOMu pomocí `document.qeurySelector`. Při každém překreslení komponenty se může stát, že React v závislosti na hodnotých stavu a props vymění starý DOM element za nový a element vybraný pomocí `querySelector` už dávno na stránce nemusí být.

V Reactu máme v podstatě tři cesty jak se legitimním způsobem dostat k DOM elementům:

- V posluchačích událostí skrze `event.target`.
- Interackí přímo s objekty `document` a `window`.
- Pomocí hooku `useRef`.

Ve zbytku lekce rozebereme, v jakých případech tyto způsoby používáme.

### Přístup pomocí `event.target`

Tuto možnost používáme hlavně v situacích, kdy propojujeme hodnotu nějakého `input` prvku se stavem.

```jsx
const EmailInput = ({ initialValue }) => {
  const [email, setEmail] = useState(initialValue);

  const handleEmailChange = (e) => {
    setEmail(e.target.value);
  }

  return (
    <input type="email" value={email} onChange={handleEmailChange} />
  );
};
```

Toto je zcela standardní způsob a nehrozí nám žádné potíže, neboť při vyvolání události máme v `event.target` vždy aktuální DOM element, na kterém událost vznikla.

### Interakce s `document` a `window`

Objekty `document` a `window` jsou stabilní a během života aplikace se nemění. Můžeme k tedy z Reactu přistupovat bezpečně. Toto se nám hodí hlavně při reakci na události, které vznikají na těcho objektech. Například:

- stisky kláves událostmi `keyup`, `keydown` apod. na `document`,
- scrollování stránky pomoc události `scroll` na `window`,
- události `online`, `offline` na `window`,
- ud8lost `beforeunload` na `window`.

Zde si musíme dávat pozor především na uzavírání zastaralých hodnot stavu nebo props v posluchačích a používat techniky, které jsme probírali v lekci o zastaralých hodnotách.

### Hook `useRef`

Občas potřebujeme na konkrétním DOM elementu zavolat nějakou jeho metodu, například `focus` na `input` prvku, `play` na přehrávači audia apod. Pro takové případy nám React poskytuje přístup k DOM elementům skrze hook `useRef`. Podrobněji jej rozebereme v další sekci.
