## Webpack DevServer

Abychom mohli naše webové aplikace spouštět, *Webpack* umožňuje použít lokální vývojový server. Abychom je mohli spustit, musíme jej nejdříve nainstalovat jako vývojovou závislost:

```
npm install -D webpack-dev-server
```

Poté do `package.json` přidáme skript:

```
"start": "webpack serve --mode=development"
```

Pak už můžeme naši aplikaci spustit pomocí

```
npm run start
```

V základu *DevServer* nevyžaduje žádnou konfiguraci. Můžeme však chtít nastavit například následující věci.

1. Často chceme, aby server fungoval v módu SPA, tedy aby na všechny GET dotazy na HTML vracel vždy `index.html`. To zařídíme pomocí `historyApiFallback`.
1. *Webpack DevServer* ve výchozím nastavení nevytváří složku `dist` a soubory si drží v operační paměti. Pokud složku generovat chceme, použijeme vlastnost `writeToDisk`.

Konfigurace pak může vypadat takto:

```
devServer: {
  historyApiFallback: true,
  devMiddleware: {
    writeToDisk: true,
  },
},
```

Dokumentaci ke všem nastavením vývojového serveru najdete [zde](https://webpack.js.org/configuration/dev-server/).
