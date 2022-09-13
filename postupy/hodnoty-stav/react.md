## React

Všechny doposud vysvětlené pojmy mají velký význam při práci se stavem v Reactu. Představte sí následující komponentu. 

```js
const TimeDisplay = () => {
  const [hours, setHours] = useState(13);
  const [minutes, setMinutes] = useState(24);
  const [seconds, setSeconds] = useState(58);
   
  // ...
};
```

Mít tři stavy, které v podstatě reprezentují jednu věc je strochu nešikovné. Radějí bychom měl jeden stav například takto. 

```js
const TimeDisplay = () => {
  const [time, setTime] = useState({
    hours: 13,
    minutes: 24,
    seconds: 58,
  });
  
  // ...
};
```

React se ke stavu chová, jako by byl vždy immutable. Při každé změně stavu tedy musí vzniknout nový objekt. Pokud chceme například k našemu času přidat sekundu, jistě víte, že to nelze provést přímo takto:

```js
time.seconds = time.seconds + 1
```

React se nemá jak dozvědět, že jsme nějak změnili objekt ve stavu. Mohli bychom zkusit třeba následujíví nápad:

```js
time.seconds = time.seconds + 1
setTime(time);
```

Možná vás překvapí, že tento pokus zafunguje. React nijak neporovnává, dokonce ani mělce, zda do stavu náhodou necpete stejnou hodnotu jaká už v něm je. Prostě pokaždé, když zavoláte změnu stavu, React komponentu přerenderuje. 

Tento způsob změny stavu je však nešikovný. Zanáší do kódu zmatek, protože najednou si může stavovou proměnnou měnit kde chce a jak chce. Násladně může zapomenout důsledně volat změnu stavu a najednou už stavová proměnná neodpovídá tomu, co se zobrazuje na stránce.

Mnohem čistší postup je důsledně se chovat k hodnotě ve stavu jako by byla immutable. Píšeme pak

```js
setTime({ ...time, seconds: time.seconds + 1 });
```

Takto máme všechny změny stavu jasně spojené z voláním metody `setTime` a nikde jinde se žádné další změny dít nemůžou. 

Uplně stejný princip platí, pokud máme ve stavu pole. Chceme-li jej změnit, děláme to pouze pomocí operací, které vytvářejí nové pole a původní hodnotu nechávají nezměněnou. 