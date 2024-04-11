## Princip fungování Reactu a založení nového projektu

React je framework/knihovna pro tvorbu uinteraktivních živatelských rozhraní deklarativním způsobem. Jako vývojáři v Reactu vytváříme komponenty, ze kterých skládáme celou aplikaci. Komponenty jsou uzavřené a samostatné a starají se o svůj vlastní stav. React pak zajišťuje efektivní vykreslování celé aplikace a aktualizaci jednotlivých komponent, když dojde ke změně dat uvnitř aplikace.

### Založení nového projektu

V praxi byl dlouho standardem pro zakládání nových projektů v Reactu **create-react-app**, ale dnes už to přestává platit. Již existují modernější a vhodnější nástroje. Často má každá firma či vývojář vytvořené vlastní workflow, jak nový projekt založit a co je jeho součástí. Protože **create-react-app** se snažil být výchozím a univerzálním startovním bodem pro obrovské množství různých projektů, obsahuje velké množství balíčků, které zabírají hodně místa a založení nového projektu může i dlouho trvat.

Pro příklady a úkoly v rámci kurzu nám stačí jen pár množstí nezbytně nutných balíčků. V předchozím kurzu React 1 (nebo v DA: Web) jsme vytvářeli projekty pomocí našeho vlastního **kodim-app**. Mimo kurzy Czechitas se ale v praxi s **kodim-app** nepotkáme, takže v Kurzu React 2 budeme používat nástroj **Vite**, který pro zákládání projektů dnes doporučují i sami autoři Reactu.

**kodim-app** z Reactu 1 je interně na **Vite** založený, takže se budete cítit jako doma a možná rozdíl ani nepoznáte.

Projekty budeme základat na příkazové řádce pomocí příkazu:

```sh
npm create vite@latest muj-projekt
```

Objeví se menu, kde vybereme, že chceme vytvořit projekt v **Reactu** a že ho budeme psát v **JavaScriptu**. Později v kurzu budeme vybírat **TypeScript**, až se ho naučíme.

Vytvoří se složka `muj-projekt` s nakonfigurovaným projektem. Musíme ale ještě spustit instalaci balíčků. Přejdeme na příkazové řádky do složky projektu a spustíme **npm install**.

```sh
cd muj-projekt
npm install
```

Když pak budeme chtít projekt spustit, použijeme příkaz:
```sh
npm run dev
```

Kód naší aplikace se nachází ve složce `src`. Výchozím bodem projektu je soubor `index.jsx`.

### JSX

JSX (JavaScript XML) je způsob, jakým se v Reactu vytváří obsah stránky. Pomocí JSX můžeme s HTML obsahem pracovat jako s jakoukoliv jinou hodnotou a můžeme ho například vložit do proměnné, předat jako hodnotu do funkce nebo je z funkcí vracet, ukládat je do polí, a podobě. JSX nebalíme do úvozovek, nejedná se o textový řetězec.

Přestože JSX vypadá jako HTML, nejedná se o čisté HTML, ale jsou zde drobné rozdíly. Např. atribut `class` musíme v JSX nahradit atributem `className`.

```jsx
const obsah = <h1 className="title">Titulek stránky</h1>;
```

### Základ aplikace v Reactu

Abychom mohli JSX obsah vložit na stránku, musíme v kódu založit React aplikaci. To se dělá pomocí metody `createRoot` objektu `ReactDOM`, který naimportujeme z balíčku `react-dom/client`. Do funkce `createRoot` předáme DOM element, do kterého se buda naše aplikace v Reactu vykreslovat. To obvykle bývá prázdný `div` element s `id` nastaveným na `root`.

Funkce vrátí objekt, na kterém zavoláme metodu `render` a předáme do ní JSX obsah naší aplikace, který se má vykreslit na stránku.

Minimální podoba React aplikace pak může vypadat například takto.

```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'

const appRoot = ReactDOM.createRoot(document.geElementById('root'));
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