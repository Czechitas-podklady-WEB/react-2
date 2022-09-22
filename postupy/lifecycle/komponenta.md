## Funkční komponenty v Reactu a useEffect

My v našem kurzu používáme tzv. :term{cs="funkční komponenty" en="function components"}. To jsou jednoduše funkce, které React spustí a jejich výsledek nějakým způsobem použije. Např. JSX vrácené z komponenty vykreslí do DOM prohlížeče.

Je velmi důležité si uvědomit, že React skutečně spustí celou funkci tvořící naši komponentu pokaždé, když potřebuje komponentu překreslit. Později se vrátíme k tomu, jaké to má důsledky.

### Překreslení komponenty

React **naplánuje** :term{cs="vykreslení" en="render"} komponenty pokaždé, když se změní *stav* uvnitř komponenty, nebo její *props*. Všimněte si zvýrazněného slova **naplánuje**.

Když pomineme úvodní vykreslení komponenty, tak k jejímu překreslení dojde pokaždé, když se změní stav komponenty nebo její props. K překreslení však nedojde úplně okamžitě. React se pokusí najít ten nejlepší moment, aby optimalizoval výkon aplikace na co největší rychlost.

### useEffect

Ve funkční komponentě reagujeme na životní cykly komponenty pomocí `useEffect`. To se týká jak úvodního vykreslení, aktualizace komponenty, nebo jejího zániku.

```jsx
import React, {useEffect} from 'react';

function Item({amount}) {

	useEffect() {
		() => {
			console.log('překreslení komponenty')
		}
	}

	return (
		<div>Zboží - {amount} ks</div>
	)
}
```

Jako první parametr do `useEffect` předáváme vždy funkci, které se má vykonat. Druhý parametr ovlivňuje, kdy se má efekt spustit.

Chceme-li, aby se náš efekt spouštěl po **každé aktualizaci komponenty**, tak druhý parametr úplně vynecháme.

```jsx
useEffect() {
	() => {
		// spustí se po každé aktualizaci komponenty
		// včetně úvodního vykreslení
	}
}
```

Když jako druhý parametr uvedeme prázdné pole, spustí se efekt pouze po **prvním vykreslení komponenty**. To nejčastěji používáme např. k úvodnímu načtení dat z API do komponenty, nastartování časovačů, apod.

```jsx
useEffect() {
	() => {
		// spustí se jenom po úvodním vykreslení
	},
	[]
}
```

Chceme-li, aby se náš kód spustil jako reakce na změnu stavu nebo konkrétních props, uvedeme do pole seznam závislostí (stavové proměnné nebo props). To můžeme použít například ve chvíli, kdy chceme z API načíst vyfiltrovaná data, protože uživatel do hledání začal psát název zboží, apod.

```jsx
useEffect() {
	() => {
		// spustí se po změně prop 'amount'
	},
	[amount]
}
```

Pokud je uvnitř komponenty použit `useEffect` vícekrát, spouští se v takové pořadí, v jakém jsou uvedeny v kódu.

### Odpojení komponenty

Jsou situace, kdy potřebujeme spustit kód ve chvíli, kdy komponenta zaniká. Například potřebujeme odstranit spuštěné časovače, nepotřebné posluchače událostí. Prostě když po sobě komponenta potřebuje uklidit.

Pokud funkce, která se spouští v `useEffect`, vrátí další funkci, tak se tato funkce zavolá těsně před tím, než komponenta zanikne.

```jsx
useEffect() {
	() => {
		// tento kód se spustí
		// jenom po úvodním vykreslení

		return () => {
			// tento kód se spustí předtím,
			// než komponenta zanikne
		}
	},
	[]
}
```
