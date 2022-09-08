## Zobrazování seznamů

Téměř v každé webové aplikaci narazíme na potřebu zobrazit nějaký seznam. Může jít o výpis zboží v e-shopu, obsah nákupního košíku, seznam úkolů v to-do listu, program kina nebo třeba nepřečtené zprávy ve schránce.

Když v Reactu do JSX předáme pole, které obsahuje JSX elementy, React všechny tyto elementy vypíše postupně do stránky.

```jsx
const workDays = [
  <li>pondělí</li>,
  <li>úterý</li>,
  <li>středa</li>,
  <li>čtvrtek</li>,
  <li>pátek</li>,
];

const App = () => (
  <>
    <h1>Pracovní dny</h1>
    <ul className="days">{workDays}</ul>
  </>
);
```

Pro vypisování seznamů dat uložených v poli můžeme použít metodu `map` pole a přemapovat datana JSX elementy. Jako JSX element samozřejmě může sloužit i námi vytvořená komponenta.

```jsx
const User = ({ login }) => {
	return (
		<div className="user__login">{login}</div>
	);
}

const names = ['petr', 'jana', 'marek', 'eva', 'lenka', 'ondra'];
const userElements = names.map((name) => <User login={name} />);

const App = () => (
  <>
    <h1>Uživatelé</h1>
    <main className="users">
			{userlements}
		</main>
  </>
);
```

### Key prop

Když naši aplikaci spustíme, React si pravděpodobně bude v konzoli stěžovat chybovou hláškou.

```
Warning: Each child in a list should have a unique "key" prop.
```

React nám říká, že každá komponenta v seznamu by měla mít unikátní klíč. React tyto klíče potřebuje k tomu, aby uměl rychle aktualizovat obsah stránky, když v seznamu přibyde nová položka nebo naopak jinou ze seznamu odstraníme.

Jako klíč může sloužit cokoliv, ale musí jít v rámci seznamu o unikátní hodnotu. V případě, že načítáme data z nějakého API, má každý záznam obvykle svoje `id`, které je pro klíč ideální. V našem jednoduchém příkladu můžeme jako klíč použít jméno uživatele.

```jsx
const userElements = names.map((name) => <User key={name} login={name} />);
```
