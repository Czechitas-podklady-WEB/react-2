## Moduly

Centrální myšlenka, kolem které se točí konfigurace Webpacku jsou takzvané moduly. Z hlediska Webpacku je modul všechno, co můžeme importovat nebo nějak jinak zahrnout do svého projektu jako závislost.

V zásadě máme dvě kategorie modulů. 

1. Nativní moduly, které umí Webpack zpracovat sám. Sem patří JavaScriptové moduly a asset moduly, které probereme v této sekci
1. Moduly, i kterých musíme Webpacku říct, jakým způsobem je má načíst. Tyto moduly probereme v sekci o *loaderech*.

### Asset moduly

Pokud chceme do našeho projektu zahrnovat i jiný typ modulu než JavaScript, například CSS styly, obrázky, fonty apod., musime Webpacku říct, jakým způsobem je má zpracovat a jak je má zapojit do našeho projektu.

K nastavení zpracování modulů slouží konfigurační vlastnost `module`. Pomocí této konfigurace můžeme například říct, že některé moduly chceme zpracovat jako assety. To znamená, že neřešíme, co v nich je, pouze je zkopírujeme někam do výsledného projektu. 

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

### Regulární výrazy v modulech

To, jakého je modul typu, testujeme podle názvu souboru, nejčastěji dle přípony. K otmu se nejčastějí používají takvzané *regulární výrazy* jako například `/\.png$/`. Regulární výrazy jsou jakési šablony, pomocí kterých můžeme testovat řetězce, zda vyhovují nějaké struktuře. Téma regulárních výrazů je velmi obsáhlé, proto zde jak pár základních pravidel.

- Regulární výrazy se píší do lomítek: `/vyraz/`.
- Můžme používat speciální znaky:
  - `.` - libovolné písmeno,
  - `?` - nepovinná část,
  - `$` - konec řetězce,
  - `^` - začátek řetězce,
  - `|` - nebo,
  - `(`, `)` slouží k uzávorkování.
- Pokud chceme speciální znak jako součást řetězce, je potřeba jej uvodit zpětným lomítkem. Například `\.`, `\?` apod.

Výraz `/\.png$/` tedy znamená "všechny soubory, které končí příponou `.png`. 

Kdybychom chtělí například všechny JPG a JPEG soubory, napíšeme `/\.jpe?g$/`. Když budeme chtít JPG i PNG a třeba ještě SVG soubory, napíšeme `/\.(png|jpe?g|svg)$/`. Tímto teste tak zpracujeme všechny nejběžnější soubory s obrázky.

Musíme pak ale upravit vygenerovaný soubor, aby měl správnou příponu.

```js
{
  test: /\.(png|jpe?g|svg)$/,
  type: 'asset/resource',
  generator: {
    filename: 'img/[name].[ext]'
  },
},
```

### HTML soubory

Html soubory můžeme zpracovávat také jako asset moduly. Stačí přidat další pravidlo.

```js
{
  test: /\.html$/,
  type: 'asset/resource',
  generator: {
    filename: '[name].[ext]'
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

Opět jej musím importovat v hlavním `index.js`, jinak jej Webpack nezpracuje.

```js
import './index.html';
```

Po sestavení projektu už máme dobrý základ webové aplikace s JavaScriptem. Abychom aplikaci spustili, budeme potřebovat server. 
