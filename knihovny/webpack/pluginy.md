## Pluginy

V předchozí části jsme zařídili rozbití keše pro soubor s výsledným JavaScriptem. Tím jsme si ale způsobili potíž, protože teď dopředu nevime, jak se výsledný soubor bude jmenovat a nemůžeme jej tedy vložit do `index.html`. Zde si musíme pomoct *pluginem*.

Webpack umožňuje rozšiřovat své schopnosti jednak pomocí loaderů, jednak pomocí pluginů. Pluginy jsou prográmky, které nějakým způsobem vstupují do procesu sestavování a mohou do něj přidat nějakou funkčnost, změnit vytvořený výstup apod.

Jedním z důležitých pluginů je *HtmlWebpackPlugin*, který umí upravit náš existující soubor `index.html` a automaticky do něj vložit výstupu Webpacku. 

Jako vždy musíme plugin nejdříve nainstalovat

```
npm install -D html-webpack-plugin
```

Plugin poté vložíme do naší konfigurace pod klíč `plugins`.

```js
plugins: [
  new HtmlWebpackPlugin({
    template: 'src/index.html',
  }),
],
```

Zde říkáme, že chceme použít náš vlastní `index.html` a do něj chceme vložit výsledný JavaScript. Je poté třeba:

1. odstranit z `index.html` prvek `script`,
1. odstranit z `index.js` import souboru `index.html`, protože nyní už jej bude zpracovávat plugin,
1. odstranit z konfigurace modulů pravidlo pro assety typu `.html`.

