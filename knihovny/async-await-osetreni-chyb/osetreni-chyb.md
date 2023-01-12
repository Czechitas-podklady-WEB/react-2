## Ošetření chybových stavů API

```jsx
function App() {
  const [cislo, setCislo] = useState();

  const nacistData = () => {
    fetch('https://random.zkusmo.eu/reliable')
    .then(resp => resp.json())
    .then(data => setCislo(data.randomNumber))
  }

  const handleClick = () => {
    nacistData();
  };

  return (
    <>
      <div>
        <button onClick={handleClick}>Budiž číslo</button>
      </div>
      <div>Náhodné číslo: {cislo}</div>
    </>
  );
}
```

### Stavové kódy HTTP odpovědi
https://developer.mozilla.org/en-US/docs/Web/HTTP/Status

## Bez ošetření chyb

```js
  const nacistData = () => {
    fetch('https://random.zkusmo.eu/reliable')
    .then(resp => resp.json())
    .then(data => setCislo(data.randomNumber))
  }

```

## Ošetření chyb vracených ze serveru

```js
  const nacistData = () => {
    fetch("https://random.zkusmo.eu/shaky")
      .then((resp) => {
        switch (resp.status) {
          case 200:
            return resp.json();
          case 500:
            alert("Server vrátil chybu.");
            break;
        }
      })
      .then((data) => {
        if (data) {
          setCislo(data.randomNumber);
        }
      });
  }

```

## Ošetření fatálních chyb

```js
  const nacistData = () => {
    fetch("https://random.zkusmo.eu/shaky")
      .then((resp) => {
        switch (resp.status) {
          case 200:
            return resp.json();
          case 500:
            alert("Server vrátil chybu.");
            break;
        }
      })
      .then((data) => {
        if (data) {
          setCislo(data.randomNumber);
        }
      })
      .catch(error => {
        console.error("Chyba komunikace se serverem:", error.message)
        alert("Chyba komunikace se serverem. Jste připojeni k internetu?")
      })
  }
```
