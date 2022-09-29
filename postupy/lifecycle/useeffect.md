## Funkční komponenty v Reactu a useEffect

Je velmi důležité si uvědomit, že React skutečně spustí celou funkci tvořící naši komponentu pokaždé, když potřebuje komponentu překreslit. React **naplánuje** :term{cs="vykreslení" en="render"} komponenty pokaždé, když se změní *stav* uvnitř komponenty, nebo její *props*. Všimněte si zvýrazněného slova **naplánuje**.

### Plánování překreslení

Pro ilustraci rozšiřme malinko komponentu `ProductItem` tak, že po klinutí na tlačítko jakoby přidáme produkt do košíku, což v tuto chvíli bude znamenat pouze změnu stavu `inCart`. 

```jsx
const ProductItem = ({ name, price, amount }) => {
  const [inCart, setInCart] = useState(false);

  const handleBuy = () => {
    setInCart(true);
    console.log(inCart);
  }

  return (
    <div className="product-item">
      <h2>{name}</h2>
      <p>Price: {price}</p>
      <p>In stock: {amount}</p>
      <button onClick={handleBuy}>Add to cart</button>
    </div>
  );
};
```

Všimněte si, že ihned po volání funkce `setInCart` vypíšeme do konzole hodnotu stavu. Pokud čekáte, že se do konzole po kliknutí na tlačítko vypíše `true`, budete zklamáni. Ke změně stavu a k překreslení komponenty nedojde totiž okamžitě. React se pokusí najít ten nejlepší moment, aby optimalizoval výkon aplikace na co největší rychlost. Tento moment rozhodně nastane dávno poté co funkce `handleBuy` skončí. Uvnitř jejího těla tedy bude stav mít stále starou hodnotu. 

### useEffect

Ve funkční komponentě reagujeme na životní cykly komponenty pomocí `useEffect`. To se týká jak úvodního vykreslení, aktualizace komponenty, nebo jejího zániku.

```jsx
const ProductItem = ({ name, price, amount }) => {
  const [inCart, setInCart] = useState(false);

  useEffect(
    () => {
	    console.log('překreslení komponenty')
    },
  );

  // ...
};
```

Jako první parametr do `useEffect` předáváme vždy funkci, které se má vykonat. Druhý parametr ovlivňuje, kdy se má efekt spustit.

Chceme-li, aby se náš efekt spouštěl po **každé aktualizaci komponenty**, tak druhý parametr úplně vynecháme.

```jsx
useEffect(
  () => {
    // spustí se po každé aktualizaci komponenty
    // včetně úvodního vykreslení
  },
);
```

Když jako druhý parametr uvedeme prázdné pole, spustí se efekt pouze po **prvním vykreslení komponenty**. To nejčastěji používáme např. k úvodnímu načtení dat z API do komponenty, nastartování časovačů, apod.

```jsx
useEffect(
  () => {
    // spustí se jenom po úvodním vykreslení
  },
  [],
);
```

Chceme-li, aby se náš kód spustil jako reakce na změnu stavu nebo konkrétních props, uvedeme do pole seznam závislostí (stavové proměnné nebo props). To můžeme použít například ve chvíli, kdy chceme z API načíst vyfiltrovaná data, protože uživatel do hledání začal psát název zboží, apod.

```jsx
useEffect(
  () => {
    // spustí se po změně prop 'amount'
  },
  [amount],
);
```

Pokud je uvnitř komponenty použit `useEffect` vícekrát, spouští se v takové pořadí, v jakém jsou uvedeny v kódu.

### Odpojení komponenty

Jsou situace, kdy potřebujeme spustit kód ve chvíli, kdy komponenta zaniká. Například potřebujeme odstranit spuštěné časovače, nepotřebné posluchače událostí. Prostě když po sobě komponenta potřebuje uklidit.

Pokud funkce, která se spouští v `useEffect`, vrátí další funkci, tak se tato funkce zavolá těsně před tím, než komponenta zanikne.

```jsx
useEffect(
  () => {
    // tento kód se spustí
    // jenom po úvodním vykreslení

    return () => {
      // tento kód se spustí předtím,
      // než komponenta zanikne
    }
  },
  [],
);
```
