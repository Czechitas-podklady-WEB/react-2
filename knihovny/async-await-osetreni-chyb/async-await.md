## async/await
V novějších verzích JavaScriptu existují dvě nová klíčová slova: `async` a `await`. Nepřinášejí novou funkcionalitu, je to pouze **syntactic sugar** pro `Promise`.

## Volání API bez ošetření chyb

```js
const nacistData = async () => {
    const resp = await fetch("https://random.zkusmo.eu/reliable");
    const data = await resp.json();
    setCislo(data.randomNumber);
  };
```

## Ošetření chyb serveru

```js
const nacistData = async () => {
    const resp = await fetch("https://random.zkusmo.eu/shaky");
    switch (resp.status) {
      case 200:
        const data = await resp.json();
        setCislo(data.randomNumber);
        break;
      case 500:
        alert("Server vrátil chybu.");
        break;
    }
  };
```

### Přidáno ošetření fatální chyby

```js
 const nacistData = async () => {
    try {
      const resp = await fetch("https://random.zkusmo.eu/shaky");
      switch (resp.status) {
        case 200:
          const data = await resp.json();
          setCislo(data.randomNumber);
          break;
        case 500:
          alert("Server vrátil chybu.");
          break;
      }
    } catch (error) {
      console.error("Chyba komunikace se serverem:", error.message);
      alert("Chyba komunikace se serverem. Jste připojeni k internetu?");
    }
  };
```

### Přidání sekce finally

```js
 const nacistData = async () => {
    try {
      const resp = await fetch("https://random.zkusmo.eu/shaky");
      switch (resp.status) {
        case 200:
          const data = await resp.json();
          setCislo(data.randomNumber);
          break;
        case 500:
          alert("Server vrátil chybu.");
          break;
      }
    } catch (error) {
      console.error("Chyba komunikace se serverem:", error.message);
      alert("Chyba komunikace se serverem. Jste připojeni k internetu?");
    } finally {
      setLoading(false)
    }
  };
```

