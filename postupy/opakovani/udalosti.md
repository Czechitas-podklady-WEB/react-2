## Události

Události tvoří základ pro jakoukoliv interaktivitu v aplikaci. Pomocí událostí reagujeme na uživatelský vstup a případně i další události, které mohou v prohlížeči nastat.

```jsx
const App = () => {
  const handleClick = () => {
    alert('ahoj');
  };

  return (
    <button className="greet" onClick={handleClick}>
      Pozdrav
    </button>
  );
};
```

Reagujeme-li na událost, kde potřebujeme o události další informace, můžeme v našem posluchači události přijmout tzv. *event object*. Například při reakci na změnu textového políčka se můžeme v posluchači zeptat na jeho aktuální hodnotu.

```jsx
const App = () => {
  const handleChange = (event) => {
    console.log(event.target.value);
  };

  return <input type="text" onChange={handleChange} />;
};
```