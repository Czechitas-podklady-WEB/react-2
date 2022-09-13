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

React se ke stavu chová, jako by byl vždy immutable. Při každé změně stavu tedy musí vzniknout nový objekt. Pokud chceme například přidat sekundu, musím psát

```js
setTime({ ...time, seconds: time.seconds + 1});
```

