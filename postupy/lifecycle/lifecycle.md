## Životní cyklus komponenty

Jako ilustrační příklad pro následující výklad si vezměme jednoduchou komponentu `ProductItem`, která představuje nějaké zboží v e-shopu.

```js
const ProductItem = ({ name, price, amount }) => {
  const [inCart, setInCart] = useState(false);

  return (
    <div className="product-item">
      <h2>{name}</h2>
      <p>Price: {price}</p>
      <button>Add to cart</button>
    </div>
  );
};
```

Všimněte si, že komponenta `ProductItem` je vlastně obyčejná JavaScriptové funkce. V moderním Reactu se již zcela výhradně používají :term{cs="funkční komponenty" en="function components"}. Každá komponenta je pak obyčejná funkce vracející JSX. Sám React pak funkci volá během jejích životního cyklu a vrácené JSX vykreslí do DOMu prohlížeče.

:term{cs="Životním cyklem" en="lifecycle"} komponenty označujeme fáze, kterými komponenta prochází během své existence v aplikaci. Komponenta během svého životního cyklu projde těmito třemi fázemi:

1. **Mount**, neboli fáze **připojení**. Jde o první volání funkce komponenty Reactem a život komponenty zde začíná. Výsledkem této fáze je první vytvoření DOMu komponenty a jeho vložení do stránky. Tato fáze nastává pouze jednou a často se jí říká :term{cs="úvodní vykreslení" en="initial render"}.

2. **Update**, neboli fáze **aktualizace** komponenty. Je to fáze, kdy React znova volá funkci komponenty aby aktualizoval jeji DOM. Tato fáze za život komponenty může nastat mnohokrát a říká se jí :term{cs="překreslení" en="re-render"}.

3. **Unmount**, neboli fáze **odpojení** komponenty nastává pouze jednou a to ve chvíli, kdy je komponenta odstraněna z DOMu stránky. V tuto chvíli se funkce komponenty jíž nevolá.

Ve starších verzích Reactu, kdy se komponenty vytvářely výhradně jako javascriptové třídy *(class components)*, měla komponenta přímo metody, které se spouštěly v konkrétních fázích životního cyklu.

### Reakce na jednotlivé fáze

Každé překreslení komponenty znamená zavolání její funkce. To můžeme snadno zachytit například pomocí `console.log` přímo v těle. 

```js
const ProductItem = ({ name, price, amount }) => {
  const [inCart, setInCart] = useState(false);

  console.log('render');

  return (
    <div className="product-item">
      <h2>{name}</h2>
      <p>Price: {price}</p>
      <p>In stock: {amount}</p>
      <button>Add to cart</button>
    </div>
  );
};
```

Toto se ale hodí výhradně pro ilustrační a ladící účely. Provádět vedlejší efekty přímo v těle funkce je velké zlo a v praxi se tomu chceme vyhnout. Pro spuštění kódu v jednotlivých fázích životního cyklu vždy používáme `useEffect`.
