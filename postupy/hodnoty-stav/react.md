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

Mít čas reprezentovaný jako tři stavy není v podstatě problém. V praxi se ale často hodí sloučít takový stav do jednoho objektu. Mezi tyto situace patří když 

1. tyto stavy často měníme společně,
1. pracujeme s daty ze serveru, které už přijdou jako jeden objekt,
1. hodnota stavu putuje napříč komponentami a jednoduší předávat jednu hodnotu než tři.

Když například budeme chtít přidat jednu minutu, je potřeba občas změnit dva stavy najednou.

```js
const addMinute = () => {
  if (minutes === 59) {
    setHours(hours + 1);
    setMinutes(0);
  } else {
    setMinutes(minutes + 1);
  }
}
```

V Reactu až do verze 17 by se komponenta přerenderovala zbytečně dvakrát. React 18 už umí tyto dvě změny stavu spojit do jedné. I tak je to však nešikovné a raději bychom stav měli v jednom objektu.


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

Pokud nyní chceme přidat minutu, jistě víte, že to nelze provést přímo takto:

```js
if (minutes === 59) {
  time.hours += 1);
  time.minutes = 0;
} else {
  time.minutes += 1;
}
```

React se nemá jak dozvědět, že jsme nějak změnili objekt uvnitř stavu. Mohli bychom zkusit třeba následujíví nápad:

```js
if (minutes === 59) {
  time.hours += 1);
  time.minutes = 0;
} else {
  time.minutes += 1;
}
setTime(time);
```

Možná vás překvapí, že tento pokus zafunguje. React totiž nijak neporovnává, dokonce ani mělce, zda do stavu náhodou necpete stejnou hodnotu jaká už v něm je. Prostě pokaždé, když zavoláte změnu stavu, React komponentu přerenderuje. 

Tento způsob změny stavu je však hodně nešikovný. Zanáší do kódu zmatek, protože takto lze  stavovou proměnnou jednoduše měnit kdykoliv a kdekoliv. Násladně snadno zapomenete důsledně volat změnu stavu a najednou už stavová proměnná neodpovídá tomu, co se zobrazuje na stránce.

Mnohem čistší postup je důsledně se chovat k hodnotě ve stavu jako by byla immutable. Píšeme pak

```js
if (minutes === 59) {
  setTime({ ...time, hours: time.hours + 1, minutes: 0 });
} else {
  setTime({ ...time, minutes: time.minutes + 1 });
}
```

Takto máme všechny změny stavu vždy jasně spojené s voláním metody `setTime` a máme dobrý přehled o tom kdy a jak se stav mění.

Uplně stejný princip platí, pokud máme ve stavu pole. Chceme-li jej změnit, děláme to pouze pomocí operací, které vytvářejí nové pole a původní hodnotu nechávají nezměněnou. 