## Burza

Hook `useRef` se ve **vyjímečných** situacích může hodit i k ukládání hodnot, které nijak nesouvisí s DOMem. Toto se nám hodí například ve chvíli, kdy nechceme mít nějakou hodnotu uloženou ve stavu. 

Pro ilustraci vyrobíme komponentu, která bude zobrazovat kurz eura vůči České koruně. Budeme chtít tako zabrazovat, jestli kurz aktuálně roste nebo klesá. 

Nejdříve vyrobíme funkci, která simuluje změny kurzu. 

```ts
const startGenerator = (callback: (n: number) => void) => {
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

```tsx
interface ExchangeRateProps {
  currency: string;
  rate: number;
}

const ExchangeRate = ({ currency, rate }: ExchangeRateProps) => {
  const prevRate = useRef<number>(0);
  
  useEffect(() => {
    prevRate.current = rate;
    //current value does not trigger re-renders. 
    //useRef is useful when you want to persist values across renders without causing the component to re-render
  }, [rate]);
  
  return (
    <div>
      Průběžný kurz {currency}: {rate}
      {prevRate.current < rate ? ' ⇑' : ' ⇓'}
    </div>
  )
};
```
