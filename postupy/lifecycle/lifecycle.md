## Životní cyklus komponenty

Jako ilustrační příklad pro následující výklad si vezměme jednoduchou komponentu `MenuItem`, která představuje položku v nějaké menu. 

```js
const MenuItem = ({ text }) => {
  const [active, setActive] = useState(false);

  return (
    <div className={`menu-item${active ? ' active' : ''}`}>
      {text}
    </div>
  );
};
```

Na začátek je dobré zdůraznit, že každá komponenta v Reactu je obyčejná JavaScriptová funkce. React potom tuto funkci volá v různých fázích životního cyklu komponenty. 

:term{cs="Životním cyklem" en="lifecycle"} komponenty označujeme fáze, kterými komponenta prochází během své existence v aplikaci. Komponenta během svého životního cyklu projde třemi fázemi:

1. **Mount**, neboli fáze **připojení**. Jde o první volání funkce komponenty Reactem a život komponenty zde začíná. Výsledkem této fáze je vytvoření DOMu komponenty a jeho vložení do DOMu stránky. Tato fáze nastává pouze jednou a často se jí říká :term{cs="úvodní vykreslení" en="initial render"}.

2. **Update**, neboli fáze **aktualizace** komponenty. Je to fáze, kdy React znova volá funkci komponenty aby aktualizoval jeji DOM. Tato fáze za život komponenty může nastat mnohokrát a říká se jí :term{cs="překreslí" en="re-render"}.

3. **Unmount**, neboli fáze **odpojení** komponenty nastáve. Nastává pouze jednou a to ve chvíli, kdy je komponenta odstraněna z DOMu stránky. V tuto chvíli se funkce komponenty nevolá. 

Ve starších verzích Reactu, kdy se komponenty vytvářely výhradně jako javascriptové třídy *(class components)*, měla komponenta přímo metody, které se spouštěly v konkrétních fázích životního cyklu.

### Reakce na jednotlivé fáze

Každé překreslení komponenty znamená zavolání její funkce. To můžeme snadno zachytit například pomocí `console.log` přímo v těle. 

```js
const MenuItem = ({ text }) => {
  const [active, setActive] = useState(false);

  console.log('render');

  return (
    <div className={`menu-item${active ? ' active' : ''}`}>
      {text}
    </div>
  );
};
```

Toto se ale hodí výhradně pro ilustrační a ladící účely. Provádět vedlejší efekty přímo v těle funkce je velké zlo a v praxi se tomu chceme vyhnout. Pro spuštění kódu v jednotlivých fázích životního cyklu vždy používáme `useEffect`.
