## Asset moduly

*Webpack* umí sám od sebe zpracovávat pouze JavaScriptové importy. Souborům, které v našem kódu importujeme se říká *moduly*. Pokud chceme do našeho projektu zahrnovat i jiný typ modulu než JavaScript, například CSS styly, obrázky, fonty apod., musime *Webpacku* říct, jakým způsobem je má zpracovat a jak je má zapojit do našeho projektu.

K nastavení zpracování modulů slouží konfigurační vlastnost `module`. Můžeme například říct, že některé moduly chceme zpracovat jako assety. To znamená, že neřešíme, co v nich je, pouze je zkopírujeme někam do výsledného projektu. 

Takto můžeme například říct, že všechny PNG obrázky jsou assety a že se mají ve výsledném sestavení vložit pod svým jménem do složky `img`. 

```js
module: {
  rules: [
    {
      test: /\.png$/,
      type: 'asset/resource',
      generator: {
        filename: 'img/[name].png'
      },
    },
  ],
},
```

Celý konfigurační soubor pak bude vypadat takto:

```js
module.exports = {
  entry: './src/index.js',
  devtool: false,
  output: {
    filename: 'bundle.js',
  },
  module: {
    rules: [
      {
        test: /\.png$/,
        type: 'asset/resource',
        generator: {
          filename: 'img/[name].png'
        },
      },
    ],
  },
};
```

Pro test naší konfigurace do `src` ve našem projektu vložím [obrázek smajlíka](assets/smiley.png) a do souboru `index.js` přidáme řádek

```js
import './smiley.png';
```

Po sestavení projektu bychom měli náš obrázek najít ve složce `dist/img`. 

### HTML soubory

Html soubory můžeme zpracovávat také jako asset moduly. Stačí přidat další pravidlo.

```js
{
  test: /\.html$/,
  type: 'asset/resource',
  generator: {
    filename: '[name].html'
  },
},
```

Soubory HTML necháme *Webpack* kopírovat přímo do výstupní složky. Nyní stačí ve složce `src` vyrobit soubor `index.html` takto:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>WP Sandbox</title>

  <script type="module" src="/bundle.js"></script>
</head>
<body>
  <div id="app"></div>  
</body>
</html>
```

Opět jej musím importovat v hlavním `index.js`, jinak jej *Webpack* nezpracuje.

```js
import './index.html';
```

Po sestavení projektu už máme dobrý základ webové aplikace s JavaScriptem. Abychom aplikaci spustili, budeme potřebovat server. 
