## Burza

Hook `useRef` se ve **vyjímečných** situacích může hodit i k ukládání hodnot, které nijak nesouvisí s DOMem. Toto se nám hodí například ve chvíli, kdy nechceme mít nějakou hodnotu uloženou ve stavu. 

Pro ilustraci vyrobíme komponentu, která bude zobrazovat kurz eura vůči České koruně. Budeme chtít tako zabrazovat, jestli kurz aktuálně roste nebo klesá. 

Nejdříve vyrobíme funkci, která simuluje změny kurzu. 

```js
const startGenerator = (callback) => {
  setInterval(() => {
    let rate = 25;
    for (let i = 0; i < 100; i++) {
      rate += (Math.random() / 100);
    }
    
    callback(Math.round(rate * 100) / 100);
  }, 1000);
};
```

Poté komponentu, která zobrazuje průběh kurzu nějaké měny.

```js
const ExchangeRate = ({ currency, rate }) => {
  const prevRate = useRef();
  
  useEffect(() => {
    prevRate.current = rate;
  }, [rate]);
  
  return (
    <div>
      Průběžný kurz {currency}: {rate}
      {prevRate.current < rate ? ' ⇑' : ' ⇓'}
    </div>
  )
};
```
