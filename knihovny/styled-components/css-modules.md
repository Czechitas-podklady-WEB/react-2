## CSS v Reactu

Doposud jsme v Reactu moc neřešili, jak pracovat s CSS. Byli jsme zvyklí CSS do projektu naimportovat a tím to pro nás většinou skončilo.

```jsx
import 'style.css';
```

U složitějších projektů bychom mohli chtít rozdělit jeden společný CSS soubor na menší kousky tak, aby CSS pro jednotlivé komponenty bylo vždy v samostatném CSS souboru přímo u konkrétní komponenty. Každá komponenta si pak importuje svůj vlastní CSS soubour a vše vypadá krásně a v nejlepším pořádku.

Webpack při kompilaci projektu všechny CSS soubory sloučí do jednoho a ten se pak připojí do HTML osuboru aplikace. Zde mohou potenciálně nastat problémy se špatným pořadím v sestaveném CSS souboru. Pořadí, v jakém se CSS sloučí, zavisí na pořadí importů CSS souborů a jednotlivých komponent v aplikaci. Podle toho, jak dobře nebo špatně je naše CSS napsané, tak mohou nastat problémy s CSS specificitou a přepisováním stylů a naše komponenty mohou zobrazovat CSS jinak, než jsme původně zamýšleli.

V ideálním případě by se nám hodilo, kdyby mohly být styly lokální jen pro naši komponentu.

## CSS moduly

Tento problém řeší projekt [CSS Modules](https://github.com/css-modules/css-modules). CSS moduly zajistí, že třídy v CSS souboru importovaném komponentou budou lokální pro danou komponentu a neovlivní a samy nebudou ovlivněny okolním CSS.

CSS moduly nejsou oficiální specifikace a implementace v prohlížečích. Jedná se proces, který proběhne během sestavení (build) celé naší aplikace za pomoci Webpacku.

### Nastavení Webpacku

Pokud k vytvoření aplikace používáte oficiální Create React App, můžete CSS moduly rovnou použít (viz. dále). Do našeho vlastního Create Czechitas App si musíme podporu pro CSS moduly přidat.

V souboru `webpack.config.js` máme pravděpodobně něco takového:

```js
{
	test: /\.css$/,
	use: ['style-loader', 'css-loader'],
},
```

Abychom zapnuli podporu pro CSS moduly, upravíme konfiguraci následovně:

```js
{
	test: /\.css$/,
	use: [
		'style-loader',
		{
			loader: 'css-loader',
			options: {
				modules: true,
				importLoaders: 1,
			}
		}
	]
},
```

### Použití CSS modulů v komponentě

Představme si, že CSS pro na3i komponentu vypadá třeba takto.

```css
.message {
	margin: 1em 0;
	padding: 1em;
	background-color: silver;
	border: 2px solid black;
	border-radius: 4px;
}

.title {
	color: grey;
}
```

V naším komponentě pak importujeme CSS styl trochu jinak, než jsme byli doposud zvyklí. Všimněte si, že styly importuje do proměnné, zde pojmenované `styles`.

```jsx
import styles from './message.css';
```

Třídy z takto naimportovaného CSS pak v Reactu použijeme následovně.

```jsx
import React from 'react';
import styles from './message.css';

const Message = () => {
	return (
		<div className={styles.message}>
			<h2 className={styles.title}>Message title</h2>
			<p>A very interesting message content.</p>
		</div>
	)
}

export default Message;
```

Když aplikaci spustíme a prozkoumáme ve vývojářských nástrojích v prohlížeči, zjistíme, že Webpack naše CSS třídy přejmenoval na unikátní identifikátory. Tím je zajištěno, že i kdybychom v CSS pro jinou komponentu použili např. třídu s obecným názvem `title`, tak se třídy vzájemně neovlivní a každé CSS bude lokální jen pro danou komponentu, která ho importuje.

### Kompozice CSS tříd

Možná používáte metodiku BEM. Ve chvíli, kdybychom chtěli z naší zprávy udělat např. chybovou hlášku, očekávali byste v HTML nejspíš BEM modifikátor přidaný ke zprávě zhruba takto:

```html
<div class="message message--error"> ... </div>
```

Při práci s CSS moduly je princip jiný. Předpokládá se, že třída, kterou použijeme, obsahuje všechny styly pro daný stav prvku. Abychom ale neduplikovali CSS společné pro všechny stavy, zaváději CSS moduly vlastnost `composes`. Ta se v CSS použije následovně:

```css
.common {
	margin: 1em 0;
	padding: 1em;
	background-color: silver;
	border: 2px solid black;
	border-radius: 4px;
}

.error {
	composes: common;
	border-color: red;
	background-color: #ffdddd;
}

.info {
	composes: common;
	border-color: blue;
	background-color: #ddddff;
}

.title {
	color: grey;
}
```

My pak v Reactu neaplikujeme na prvek více tříd, ale použijeme jen tu jednu konkrétní:

```jsx
const Message = () => {
	return (
		<div className={styles.error}>
			<h2 className={styles.title}>Message title</h2>
			<p>A very interesting message content.</p>
		</div>
	)
}
```

Podívejte se znovu do vývojářských nástrojů, jak CSS moduly tuto situaci vyřešily.
