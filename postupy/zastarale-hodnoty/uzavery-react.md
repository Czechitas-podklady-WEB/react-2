## Uzávěry v Reactu

Pro ilustraci vyrobím v Reactu úplně obyčejné tlačítko, které počítá, kolikrát jsme na něj kliknuli.

```jsx
const Counter = () => {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    setCount(count + 1);
  };

  return (
    <button onClick={handleClick}>Počet: {count}</button>
  );
};
```

Takové tlačítko bude zcela bez problémů fungovat. Co kdybychom z nějakého důvodu chtěli počet navýšit třeba stiskem mezerníku. Tady si musíme vypomoct `useEffectem`, protože potřebujeme posluchač přidat přímo na `document`.

```jsx
const Counter = () => {
  const [count, setCount] = useState(0);

  const handleKeyUp = (e) => {
    if (e.code === 'Space') {
      setCount(count + 1);
    }
  };

  useEffect(() => {
    document.addEventListener('keyup', handleKeyUp);
    return () => document.removeEventListener('keyup', handleKeyUp);
  }, []);

  const handleClick = () => {
    setState(count + 1);
  };

  return (
    <button onClick={handleClick}>Počet: {count}</button>
  );
};
```

Bohužel, mačkání klávesy mezerník nedělá to, co bychom si představovali. MOžná tušíte, že na vině budou uzávěry.

Funkce `handleClick` i `handleKeyUp` používá proměnnou `count`, což je proměnná z nadřazeného bloku. Každá z těchto funkcí je tedy uzávěrem proměnné `count`. Jak už víme z minula, pokaždé, když se změní stav komponenty, React spustí její funkce znova, takže se znova vytvoří i funkce `handleClick` a `handleKeyUp` a v nich uzavřená nová hodnota stavu. U funkce `handleClick` není problém, protože React pri aktualizaci DOMu komponenty vymění novou `handleClick` za starou `handleClick`. Funkci `handleKeyUp` jsme však na `document` přidali sami a to pouze při mountu komponenty. React o tom nic neví, takže ná nemůže pomoct a na události `keyUp` pořád visí stará `handleKeyUp`, ve které je uzavřena stará hodnota stavu.

V takovém případě říkáme, že ve funkci je :term{cs="zastaralý stav" en="stale state"}. Máme několik možností, jak z této situace ven:

1. úplně se vyhnout uzávěrům,
1. postarat se o výměnu staré funkce za novou sami.

### Vyhnutí se uzávěrům

React nabízí možnost, jak se vyhnout použití uzávěru tím, že funkci `setCount` nepředáme přímo novou hodnotu stavu, ale funkci, která dostane starou hodnotu a vyrobí z ní novou.

```js
const handleKeyUp = (e) => {
  if (e.code === 'Space') {
    setCount((oldCount) => oldCount + 1);
  }
};
```

Vidíme, že funkce v sobě neuzavírá hodnotu stavu `count`, pouze vytváří funkci, kterou React použije k vygenerování nové nodnoty pro stav.

Pokud je nastavování stavu složitější process, tento postup může být hodně těžkopádný až zcela nerealizovatelný. Máme tedy druhou možnost.

### Samostatná výměna funkce

V tomto případě upravíme `useEffect` tak, že jej učiníme závislý na hodnotě stavu.

```js
useEffect(() => {
  document.addEventListener('keyup', handleKeyUp);
  return () => document.removeEventListener('keyup', handleKeyUp);
}, [count]);
```

V takovémto případě se uklízací funkce nespouští při unmountu, ale těsně před tím, než se efekt vyvolá znova. V uklízecí funkci je uzavřena stará funkce `handleKeyUp`, můžeme ji tedy z události `keyUp` odebrat tesně před tím, než tam přidáme dalším spuštěním efektu funkci novou.
