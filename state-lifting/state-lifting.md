## State lifting

Sdílení dat a komunikace mezi komponentami je jedna z největších výzev v architektuře Reactových aplikací. V praxi budeme často v situaci, kdy nějaká komponenta potřeboje data zevnitř některého ze svých potomků. React však nemá žádný nástroj nebo příkaz, jakým by předek mohl z potomka získat data. Tuto situaci musíme vyřešit pomocí techniky s názvem :term{cs="povýšení stavu" en="state lifting"}.

### Ukázka: Hračkorama

K ilustraci výše popsané situace použijeme project e-shopu :i[Hračkorama]. Základ projektu najdete v [tomto repozitáři](https://github.com/Czechitas-podklady-WEB/hrackorama-kosik).

V tuto chvíli nás bude zajímat komponenta `Amount`. Ta umožňuje zvolit počet kusů daného produktu. V komponentě `Cart` budeme chtít zobrazovat celkový počet položek v košíku. Bohužel tato komponenta se nemá jak dostat k číslu ve stavu komponenty `Amount`. Budeme tedy muset provést povýšení stavu.

Nejprve z cvičných důvodů povýšíme stav do kompnenty `CartItem`. To sice náš problém ještě nevyřeší, ale ukázeme si tím základní principy.

Stav `count` nyní bude v komponentě `CartItem`.

```jsx
const CartItem = ({ product }) => {
  const [count, setCount] = useState(product.amount);

  return (
    <div className="cart-item">
      <CartProduct name={product.name} price={product.price} />
      <Amount value={count} />
    </div>
  )
};
```

Stav pak předáme pomocí prop `value` do komponenty `Amount`. Nyní potřebujeme, aby komponenta `Amount` dala vědět o změně své hodnoty.

```jsx
const CartItem = ({ product }) => {
  const [count, setCount] = useState(product.amount);

  const handleAmountChange = (newCount) => {
    setCount(newCount);
  }

  return (
    <div className="cart-item">
      <CartProduct name={product.name} price={product.price} />
      <Amount value={count} onChange={handleAmountChange} />
    </div>
  )
};
```

Komponenta `Amount` pak bude vypadat takto:

```jsx
const Amount = ({ value, onChange }) => {
  const handleIncrement = () => {
    onChange(value + 1);
  }

  const handleDecrement = () => {
    if (value > 0) {
      onChange(value - 1);
    }
  }

  return (
    <div className="amount">
      <button className="amount__btn" onClick={handleDecrement}>–</button>
      <div className="amount__count">{value}</div>
      <button className="amount__btn" onClick={handleIncrement}>+</button>
    </div>
  );
};
```

Chování aplikace se tímto nezměnilo, stav jsme však povýšili o jednu úroveň výše.

<!-- Představme si situaci, kdy vytváříme komponentu `EmailInput`, která umí ověřit validitu zadávaného e-mailu. Taková komponenta může vypadat například takto:

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

Narazili jsme na klasickou situaci, kdy rodičovská komponenta potřebuje přístup k datům některého ze svých potomků. Přesně v tomto případě použijeme state lifting a přesuneme stav z komponenty `EmailInput` do komponenty `App`.

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
``` -->
