## Komponenty a props

Každá aplikace v Reactu se skládá z komponent. Komponenty jsou dílky stavebnice, ze kterých naši aplikace postupně skládáme.

Komponenta v Reactu je funkce, která na svém výstupu vrací JSX. Toto JSX se na stránce vykreslí v místě, kde naši komponentu použijeme.

```jsx
const App = () => {
	return (
		<>
			<h1 className="title">Moje stránka</h1>
			<p>Textový obsah stránky</p>
		</>
	);
};
```

Název funkce, která tvoří komponentu, **musí začínat velkým písmenem**. Takto vytvořenou komponentu pak můžeme používat jako běžnou HTML značku.

```jsx
import React from 'react';
import { createRoot } from 'react-dom/client';

const App = () => {
	return (
		<>
			<h1 className="title">Moje stránka</h1>
			<p>Textový obsah stránky</p>
		</>
	);
};

createRoot(document.querySelector('#app')).render(
	<App />
);
```

### Komponenty a props

Komponenty jsou mnohem užitečnější, když do nich můžeme předat data, se kterými komponenta může pracovat. V terminologii Reactu se říká, že do komponenty předáváme *props* (zkráceno z *properties*).

V místě, kde komponentu používáme, přidáme props jako atributy HTML značky. Do komponenty se props dostanou jako jeden objekt, kde každá prop je jedna vlastnost tohoto objektu. Pro jednodušší používání props uvnitř komponenty můžeme objekt destrukturovat do proměnných.

```jsx
import React from 'react';
import { createRoot } from 'react-dom/client';

const ShoppingItem = (props) => {
  const { name, amount } = props;

  return (
    <div className="item">
      <span className="item__name">{name}</span>
      <span className="item__amount">{amount}</span>
    </div>
  );
};

const App = () => {
	return (
		<>
		  <header>
      	<h1>Nákupní seznam</h1>
    	</header>
    	<main className="shopping-list">
      	<ShoppingItem name="Mléko" amount="1 l" />
      	<ShoppingItem name="Máslo" amount="250 g" />
      	<ShoppingItem name="Rohlíky" amount="8 ks" />
    	</main>
    </>
	);
};

createRoot(document.querySelector('#app')).render(
	<App />
);