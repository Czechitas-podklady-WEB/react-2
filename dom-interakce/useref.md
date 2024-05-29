## Hook `useRef`

Pro ilustraci uvažme komponentu, která po kliknutí na tlačíko *zaplatit* zobrazí políčko pro zadání čísla karty.

```tsx
const Payment = () => {
  const [cardIinputVisible, setCardIinputVisible] = useState<boolean>(false);

  const handlePay = () => setCardIinputVisible(true);

  return (
    <div className="payment">
      <button onClick={handlePay}>Zaplatit</button>
      {cardIinputVisible ? <input type="text" /> : null}
    </div>
  );
};
```

Při zobrazení políčka do něj chceme ihned přesunout focus. K tomu ale potřebujeme přístup k DOM elementu políčka, abychom na něm mohli zavolat metodu `focus()`. 

Díky hooku `useRef` můžeme získat přístup k libovolnému elementu vyrobenému pomocí JSX. Nejdříve na začátku komonenty založeníme takzvanou *ref*. 

```ts
const cardInputRef = useRef<HTMLInputElement>(null);
```

React nám do proměnné `cardInputRef` vloží speciální objekt, který předáme pomocí *prop* z názvem `ref` našemu inputu v JSX.

```tsx
<input type="text" ref={cardInputRef} /> : null}
```
      
Objekt v proměnné `cardInputRef` má jedinou vlastnost vlastnost `current`. Pokud prvek, kterému jsme naši *ref* nastavili na stránce není, vlastnost `current` má hodnotu `undefined`. Jakmile se prvek na stránce objeví, ve vlastnosti `current` máme uložený aktuální DOM element tohoto prvku. Můžeme pak napsat efekt, ve kterém na tento prvek přeneseme focus.

```js
  useEffect(() => {
    if (cardIinputVisible && document.activeElement !== cardInputRef.current) {
      cardInputRef.current.focus();
    }
  }, [cardIinputVisible]);
```

Celá komponenta pak bude vypadat takto:

```tsx
const Payment : React.FC = () => {
  const [cardIinputVisible, setCardIinputVisible] = useState<boolean>(false);
  const cardInputRef = useRef<HTMLInputElement>(null!);

  useEffect(() => {
    if (cardIinputVisible && document.activeElement !== cardInputRef.current) {
      cardInputRef.current.focus();
    }
  }, [cardIinputVisible]);
  


  const handlePay = () => setCardIinputVisible(true);

  return (
    <div className="payment">
      <button onClick={handlePay}>Zaplatit</button>
      {cardIinputVisible ? <input type="text" ref={cardInputRef}/> : null}
    </div>
  );
};
```

Důležité je, že hodnota v proměnné `cardInputRef` je stabilní přes všechna vykreslení. Jde tedy o pořád tentýž objekt, který nezastará a můžeme jej beze strachu uzavřít do libovolné funkce uvnitř komponenty. Jediné, co se mění je obsah vlastnosti `current` tak, aby vždy obsahovala aktální DOM element nebo `undefined`, pokud referencovaný element na stránce ještě není vykreslený.
