## Motivace

Sdílení dat a komunikace mezi komponentami je jedna z největších výzev v architektuře Reactových aplikací. Důležítá techníka používaná pro sdílení dat je takzvaný :em[state lifting]. Jde o přesunutí stavových dat z komponenty do některého z jejích předků. Díky tomu získají k těmto datům přístup další komponenty vw stromě.

### Ukázka

Představme si situaci, kdy vytváříme komponentu `EmailInput`, která umí ověřit validitu zadávaného e-mailu. Taková komponenta může vypadat například takto:

```js
const EmailInput = () => {
  const [email, setEmail] = useState('');
  
  return (
    <div className="validated-input">
      <input 
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      { 
        email.includes('@') 
        ? null 
        : <div className="invalid-msg">Invalid email address</div>
      }
    </div>
  )
};
```

Můžeme ji pak použít v nějakém formuláři naší aplikace:

```js
const App = () => {
  return (
    <div className="container-sm">
      <h1>Registrace</h1>
      <form>
        <label>Email: <EmailInput /></label>
        <button type="submit">Submit</button>
      </form>
    </div>
  );
};
```

Nyní bychom chtěli vytvořit funkci `handleSubmit`, která provede odeslání dat z formuláře na server. Tady ovšem narazíme na problém: řetězec se zadaným e-mailem je uzavřený ve stavu komponenty `EmailInput`. K tomuto stavu nemá komponenta `App` přístup. Co si počít?

Narazili jsme na klasickou situaci, kdy rodičovská komponenta potřebuje přístup k datům některého ze svých potomků. Přesně v tomto případě použijeme state lifting a přesuneme stav do z komponenty `EmailInput` do komponenty `App`. 

```js
const App = () => {
  const [email, setEmail] = useState('');
  
  return (
    <div className="container-sm">
      <h1>Registrace</h1>
      <form>
        <label>
          Email:
          <EmailInput
            value={email}
            onChange={(value) => setEmail(value)}
          />
        </label>
        <button type="submit">Submit</button>
      </form>
    </div>
  );
};
```

Komponenta `EmailInput` obdrží hodnotu e-mailu skrze prop `value` a její změnu komunikuje pomocí callbacku `onChange`. 

```js
const EmailInput = ({ value, onChange }) => {
  return (
    <div className="validated-input">
      <input 
        type="email"
        value={value}
        onChange={(e) => onChange(e.target.value)}
      />
      { 
        value.includes('@') 
        ? null 
        : <div className="invalid-msg">Invalid email address</div>
      }
    </div>
  )
};
```
