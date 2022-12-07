## Nastavení Webpacku

Ve všech našich Reactových projektech v tomtu kurzu používáme pro sestavení výsledného projektu Webpack. Ten vždy pracuje tak nějak tiše na pozadí a dělá za nás nějakou tajemnou magii, o které moc nepřemýšlíme, dokud dobře funguje, a zoufáme si, když se něco rozbije.

Do kompotencí každého zkušenějšího webového vývojáře patří vědět alespoň základně, co Webpack dělá, jak to dělá, jak jej nastavit pro konkrétné projekt a jak vyřešit případné potíže, kterých je vždy pestrá nabídka. Je tedy na čase pustit se hloubějí do vod zatím neprobádaných a lépe se s tímto nástrojem seznámit.

### Testovací projekt

Abychom si vyzkoušeli, jak přesně Webpack funguje, vytvoříme si úplně základní projekct v prostředí Node.js a NPM. Založíme si někde na disku složku s názvem `wpsandbox` a uvnitř spustíme

```
npm init -y
```

Tento příkaz vygeneruje základní `package.json`. 

Webpack slouží především ke spojování více JavaScriptových souborů do jednoho. V projektu proto vytvoříme složku `src` a v něm soubory `index.js` a `greet.js`, které se později budeme snaži spojit.

`greet.js`:

```js
export const greet = (name) => {
  return `Hello ${name}!`;
};
```

`index.js`:
```js
import { greet } from "./greet.js";

document.querySelector('#app').innerHTML = `
  <h1>${greet('World')}</h1>
`;
```

Nyní nainstalujeme *Webpack* jako vývojovou závislost (přepínač `-D`).

```
npm install -D webpack webpack-cli
```

Tímto jsme *Webpack* nainstalovali lokálně jako závislost do našeho projektu. To mimo jiné znamená, že *Webpack* nemůžeme spustit jen tak v terminálu příkazem `webpack`. To bychom jej museli nainstalovat globálně do operačního systému a tomu je dobré se spíše vyhnout, ať si systém nezaplavelujeme zbytečnými balíčky. 

Abychom mohli *Webpack* spouštět lokálně, je potřeba vyrobit si v `package.json` nové skripty

```
"scripts": {
  "build": "webpack --mode=development",
  "build:prod": "webpack --mode=production",
},
```

Skript `build` vygeneruje výstup vhodný pro vývoj, skript `build:prod` generuje výstup vhodný k produkčnímu nasazení. Rozdíly si ukážeme později v lekci.

Nyni musíme pomocí konfiguračního souboru *Webpacku* říct, co má dělat. Vytvořím tedy vedle složky `src` soubor `webpack.config.js`. Na začátek může být jeho obsah extrémně jednoduchý:

```js
module.exports = {
  entry: './src/index.js',
  devtool: false,
  output: {
    filename: 'bundle.js',
  },
};
```

- Pomocí vlastnosti `entry` *Webpacku* říkáme, od kterého JavaScriptového souboru má začít zpracování našeho projektu.
- `devtool: false` říká, že chceme výstup, který je jakž takž čitelný pro člověka. Bez tohoto nastavení se v tom, co *Webpack* vygeneruje, nedá vůbec vyznat.
- Pomocí vlastnosti `output` *Webpacku* říkáme, kam se má uložit vygenerovaný výstup Vlastnost `filename` udává název výsledného vygenerovaného souboru.

Nyní můžeme spustit vývojové sestavení

```
npm run build
```

*Webpack* nám vytvoří složku `dist` a v ní soubor `bundle.js`. Na vlastní nebezečí do něj můžete nahlédnout. Po delší snaze se vám v něm možná podaří najít i útržky vašeho kódu obaleného spustou technických věcí, kterým rozumí jen ti nejzasvěcenější.
