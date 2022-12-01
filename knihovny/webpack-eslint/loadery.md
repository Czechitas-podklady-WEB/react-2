## Loadery

V předchozí části jsme viděli asset moduly, které jsou jednodušší na zpracování, protože Webpack se nemusí snažit pochopit, co je uvnitř souboru. Prostě jej vezme a někam zkopíruje. 

Často ovšem chceme importovat modul, jehož obsah je potřeba nějak zpracovat. Příkladem budiž CSS styly, kde je potřeba mimo jiné najít všechny obrázky, které se v CSS používají, a zahrnout je jako závislosti do projektu. 

Webpack sám o sobě umí zpracovat pouze JavaScript. Pokud chceme zpracovat CSS, musíme Webpacku říct, jak to má udělat pomocí takzvaného *loaderu*. Pro zpracování CSS slouží takzvaný `css-loader`, který si musíme do projektu nainstalovat.

```
npm install -D css-loader
```

Pro import CSS souborů pak vytvoříme tuto konfiguraci uvnitř `rules`.

```js
{
  test: /\.css$/,
  use: 'css-loader',
}
```

Abychom naše nastavení otestovali, vytvoříme si soubor `style.css`. 

```css
.h1 {
  color: blue;
}

.smiley-face {
  background-color: url(smiley.png);
}
```

Upravím náš hlavní `index.js`, tak, že zde importujeme naše styly a zároveň smažeme import obrázku, protože ten už máme zmíněný v CSS pomocí `url()`.

```js
import { greet } from "./greet.js";
import './style.css';
import './index.html';

document.querySelector('#app').innerHTML = `
  <h1>${greet('World')}</h1>
  <div class="smiley-face"></div>
`;
```

Když nyní projekt sestavíme, měli bychom vidět, že obrázek `smiley.png` se do projektu zapojil i když jsme jej neimportovali. To je právě práce loaderu `css-loader`, který projde naše CSS a všechny obrázky označí jako závislosti, aby je pak Webpack zpracoval podobně jako importy.

### Načítání stylů

Pokud naši stránku nyní spustíme, zjistíme, že v ní ale žádné styly nejsou. Udělali jsme něco špatně? Nikoliv. Loader `css-loader` slouží pouze k načtení stylů z CSSka ale už neříká, co se má s těmito styly udělat.

Pokud chceme naše styly zapojit do stránky pomocí `<style></style>` prvků, použijeme k tomu `style-loader`, který zapojíme za `css-loader`. Nový loader opět musíme nainstalovat

```
npm install -D style-loader
```

a zapojit za `css-loader`

```js
{
  test: /\.css$/,
  use: ['style-loader', 'css-loader'],
}
```

Sice to vypadá, že jsem nový loader zapojili před, nikoliv za `css-loader`, Webpack však loadery spouští od konce, tedy nejříve `css-loader`, který načte styly a pak `style-loader`, který je zapojí do stránky.

Po všech těchto eskapádách bychom už měli mít funkční stránku se vším všudy.
