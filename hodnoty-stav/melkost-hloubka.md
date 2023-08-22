## Mělkost a hloubka

Pokud pracujeme s mutable hodnotami, můžeme narazit v podstatě na dvě situace. 

1. Dvě proměnné odkazují skutečně na tutéž hodnotu.
   ```js
   > const x = [1, 2, 3]
   > const y = x
   > x === y
   true
   ```
1. Dvě proměnné odkazují dvě různé hodnoty, které ale mají stejnou strukturu.
   ```js
   > const x = [1, 2, 3]
   > const y = [1, 2, 3]
   > x === y
   false
   ```

Tomuto způsobu porovnávání říkáme mělké porovnání. Mělké proto, že nás nezajímá hlubší struktura hodnoty, ale pouze povrchně zjišťujeme, zda jde o tutéž hodnotu nebo nikoliv. 

V praxi však často potřebujeme hluboké porovnání, tedy takové, kde skutečně zjišťuje, jestli jsou dvě hodnotu strukturně stejné. JavaScript standardně neobsahuje žádný operátor, který by uměl hluboké porovnávání. Musíme k tomu použít knihovnu. Jedna z možností je balíček [fast-deep-equal](https://www.npmjs.com/package/fast-deep-equal). Můžeme jej použít v NodeJS/Webpacku/Reactu

```
npm install fast-deep-equal
```

```js
import equals from 'fast-deep-equal';

const x = [1, 2, 3];
const y = [1, 2, 3];

console.log('shallow:', x === y);
console.log('deep:', equals(x, y));
```