## Princip fungování Reactu a založení nového projektu

React je framework/knihovna pro tvorbu uinteraktivních živatelských rozhraní deklarativním způsobem. Jako vývojáři v Reactu vytváříme komponenty, ze kterých skládáme celou aplikaci. Komponenty jsou uzavřené a samostatné a starají se o svůj vlastní stav. React pak zajišťuje efektivní vykreslování celé aplikace a aktualizaci jednotlivých komponent, když dojde ke změně dat uvnitř aplikace.

### Založení nového projektu

V praxi je standardem pro zakládání nových projektů v Reactu **create-react-app** nebo má každá firma či vývojář vytvořené vlastní workflow, jak nový projekt založit a co je jeho součástí. Protože **create-react-app** se snaží býct výchozím a univerzálním startovním bodem pro obrovské množství různých projektů, obsahuje velké množství balíčků, které zabírají hodně místa a založení nového projektu může i dlouho trvat.

Pro účely našeho kurzu je to kanón na vrabce. Pro příklady a úkoly v rámci kurzu nám stačí jen pár množstí nezbytně nutných balíčků. Vytvořili jsem vlastní **create-czechitas-app**, pomocí kterého budeme nové projekty vytvářet. Na příkazové řádce použijeme:

```sh
npx create-czechitas-app muj-projekt
```

Vytvoří se složka `muj-projekt`, kam se nainstalují potřebné balíčky, nastaví se Webpack a vytvoří se základní kostra vzorového projektu, kterou si můžeme dále upravovat.

Kód naší aplikace se nachází ve složce `src`. Výchozím bodem projektu je soubor `index.jsx`.

### JSX

JSX (JavaScript XML) je způsob, jakým se v Reactu vytváří obsah stránky. Pomocí JSX můžeme s HTML obsahem pracovat jako s jakoukoliv jinou hodnotou a můžeme ho například vložit do proměnné, předat jako hodnotu do funkce nebo je z funkcí vracet, ukládat je do polí, a podobě. JSX nebalíme do úvozovek, nejedná se o textový řetězec.

Přestože JSX vypadá jako HTML, nejedná se o čisté HTML, ale jsou zde drobné rozdíly. Např. atribut `class` musíme v JSX nahradit atributem `className`.

```jsx
const obsah = <h1 className="title">Titulek stránky</h1>;
```

### Základ aplikace v Reactu

Abychom mohli JSX obsah vložit na stránku, musíme v kódu založit React aplikaci. To se dělá pomocí funkce `createRoot`, kterou naimportujeme z balíčku `react-dom/client`. Do funkce `createRoot` předáme DOM element, do kterého se buda naše aplikace v Reactu vykreslovat. To obvykle bývá prázdný `div` element s `id` nastaveným na `app`.

Funkce vrátí objekt, na kterém zavoláme metodu `render` a předáme do ní JSX obsah naší aplikace, který se má vykreslit na stránku.

Minimální podoba React aplikace pak může vypadat například takto.

```jsx
import React from 'react';
import { createRoot } from 'react-dom/client';

const appRoot = createRoot(document.querySelector('#app'));
appRoot.render(<h1 className="title">Moje stránka</h1>);
```

### Fragment

Metoda `render` jako parametr akceptuje pouze jeden JSX element. Pokud bychom chtěli na stránce vykreslit např. nadpis a odstavec, nebude náš příklad fungovat.

```jsx
appRoot.render(
	<h1 className="title">Moje stránka</h1>
	<p>Textový obsah stránky</p>
);
```

Můžeme samozřejmě vše zabalit do `divu` nebo jiného prvku, ale pak máme v aplikaci prvky, které tam nutně nepotřebujeme a mohou nám třeba i zoůsobit problémy se stylováním.

React nabízí speciální element, kterému říká *fragment*. Vypadá jako prázdná HTML značka, do které můžeme zabalit další elementy, ale která se ve výsledné stránce neobjeví.

```jsx
appRoot.render(
	<>
		<h1 className="title">Moje stránka</h1>
		<p>Textový obsah stránky</p>
	</>
);
```