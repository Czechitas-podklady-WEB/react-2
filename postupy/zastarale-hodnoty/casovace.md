## Časovače

K problémum se zastaralými hodnotami v React dochází vždy, když funkce vytvořené v těle komponenty pužíváme mimo JSX. V takovím případě nemá React nad našimi funckemi kontrolu a nemůže vyměňovat staré funkce za nové. To nastává v případě

1. událostí, které obsluhujeme mimo React jako `document/keyUp`, `window/offline` apod.,
1. časovačů jako `setTimeout` a `setInterval`.

U časovačů je situace jiná, než u událostí, protože za běhu časovače není už možné vyměnit funkci, kterou časovač vykonává. Postup s ruční výměnou funkce nám je tady k ničemu.

Dejme tomu, že bychom chtěli v naší komponentě `Counter` zvyšovat hodnotu automaticky každou vteřinu. S následujícím postupem bychom pohořeli.

```jsx
const Counter = () => {
  const [count, setCount] = useState(0);

  const handleTimer = (e) => {
    setCount(count + 1);
  };

  useEffect(() => {
    const timerId = window.setInterval(handleTimer, 1000);
    return () => window.clearInterval(timerId);
  }, []);

  const handleClick = () => {
    setState(count + 1);
  };

  return (
    <button onClick={handleClick}>Počet: {count}</button>
  );
};
```

V časovači už totiž bude naždy použita pouze první verze funkce `handleTimer` vznklá při prvním vykreselní komponenty. V této funkce je navždy uzavřena proměnná `count` s prvotní hodnotou 0.

Nebude nám, než využít techniku "vyhnutí se uzávěrům" a napsat časovač takto:

```js
const handleTimer = (e) => {
  setCount((oldCount) => oldCount + 1);
};
```

V tomto případě proměnnou `count` vůbec nepoužíváme, takže se do naší funkce nauzavře. Díky tomu můžeme tuto funkcí volat opakovaně, i když už je dávno zastaralá.

V tomto příkladu je také smysluplnější vyrobit funkci `handleTimer` přímo uvnitř `useEffet`. Nepobtřebujeme totiž, aby React zbytečně při každém renderu vytvářel nové a nové verze této funkce, které stejně k ničemu neopužijeme.

```jsx
  useEffect(() => {
    const handleTimer = (e) => {
      setCount((oldCount) => oldCount + 1);
    };

    const timerId = window.setInterval(handleTimer);
    return () => window.clearInterval(timerId);
  }, []);
```

Dopad této změny na chod aplikace je naprosto zanedbatelný. Náš kód bude pouze malinko uklizeněšjí, což nikdy není na škodu. Můžeme pak večer lépe usínat s hřejivým pocite, že věcem rozumíme, a víme, co děláme.
