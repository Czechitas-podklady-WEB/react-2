## React context

Ve složitějších aplikacích potkáme situace, kdy potřebujeme povýšit stav opravdu vysoko, někdy až do kořene samotné aplikace. Pokud je strom komponent hluboký, snadno se nám stane, že budeme vysoce povýšený stav předávat pomocí props skrze mnoho úrovmí. Této sitauci se v React terminologii říká :term{cs="vrtání props" en="props drilling"}. Pokud je situace už neúnosná, můžeme se props drillingu vyhnout použitím React contextu. 

Pomocí React contextu můžeme zařídit, že nějaká část naší aplikace má přistup k určitým hodnotám bez nutnosti předávat je pomocí props. Typickým příkladem je napříkad informace o přihlášeném uživateli. Mnoho komponent na různých místech v aplikaci potřebuje informaci o tom, zde je přihlášený nějaký uživatel. Provrtávat props o uživateli do všech těchto komponent by byla ohromná a nevděčná práce.

Práci s přihlášením si vyzkoušíme ve cvičení. Zde pro ilustraci použijeme jinou situaci, která se týká naší aplikace Hračkorama. Představme si, že bychom chtěli zobrazovat ceny produktů podle toho, jakou má uživatel nastavenou měnu. Uživatelská nastavení mohou být také dobrým příkladem hodnot, které je potřeba mít dostupné na mnoha místech aplikace. 

V naší aplikaci budeme chtít mít dostupný takovýto objekt:

```js
{
  currency: 'CZK',
}
```

Za tímto účelem vytvoříme React context s názvem `SettingsContext`. Pro context vytvoříme separátní soubor `settings-context.js`.

```js
import React, { createContext } from 'react';

export const SettingsContext = createContext();
```

Nyní je potřeba tu část aplikace, kde chceme náš context používat, obalit speciální komponentou zvanou context provider. My chceme context používat v celé aplikaci, dáme tedy provider rovnou do kořene. 

```jsx
import { SettingsContext } from './settings-context';

const App = () => {
  return (
    <SettingsContext.Provider value={{ currency: 'CZK' }}>
      <div className="container">
        <Header />
        <Banner />
        <Cart />
      </div>
    </SettingsContext.Provider>
  );
};
```

V každé komponentě, která se nachází ve stromě komponent uvnitř context provideru, pak máme přístup k hodnotě předané pomocí prop `value`. Použijeme k tomu hook `useContext`.Takto například můžeme získat aktuální měnu uvnitř komponenty `CartProduct`.

```jsx
import { SettingsContext } from "../../settings-context";

const CartProduct = ({ name, price }) => {
  const { currency } = useContext(SettingsContext);
  
  return (
    <div className="cart-product">
      <span>{name}</span>
      <span>{price} {currency}</span>
    </div>
  )
};
```

### Vlastní hook

Je zvykem pro použití contextu vytváří vlastní hook, který má přiléhavější název a zlepšuje čitelnost kódu. 

```js
import React, { createContext, useContext } from 'react';

export const SettingsContext = createContext();

export const useSettings = () => useContext(SettingsContext);
```

Pak nám stačí v komopnentě `CartProduct` psát jednodušeji:

```jsx
import { useSettings } from "../../settings-context";

const CartProduct = ({ name, price }) => {
  const { currency } = useSettings();
  
  return (
    <div className="cart-product">
      <span>{name}</span>
      <span>{price} {currency}</span>
    </div>
  )
};
```
