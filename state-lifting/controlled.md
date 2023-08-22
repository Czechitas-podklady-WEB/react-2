## Controlled komponenty

Pokud nějaké komponenta, například `CartItem`, spravuje stav jiné komponenty, například  `Amount`, říkáme, že komponenta `Amount` je takzvaně :term{cs=kontrolovaná en=controlled}. Pokud naopak komponenta spravuje svůj vlastní stav, říkáme, že je :term{cs=nekontrolovaná en=uncontrolled}.

V našem příkladu z předchozí lekce jsme tedy udělali z komonenty `Amount` kontrolovanou komponentu. K vyřešení našeho problému to ale nestačí. Potřebujeme stav povýšit až do komponenty `Cart`. To znamená, že komponenta `Cart` bude muset spravovat stav pro všechny produkty najednou. Máme však štěstí, protože každý produkt v poli produktů už obsahuje položku `amount`. Stačí tedy toto pole použít jako stav. Můžeme jej pojmenovat třeba `cartProducts`.

Nejprve upravíme komponentu `CartItem` tak, aby už nepoužívala stav `count`.

```jsx
const CartItem = ({ product, onAmountChange }) => {
  return (
    <div className="cart-item">
      <CartProduct name={product.name} price={product.price} />
      <Amount value={product.amount} onChange={onAmountChange} />
    </div>
  )
};
```

Všimněte si callbacku `onAmountChange`, který potřebujeme, abychom se dozvěděli o aktualizacích hodnoty uvnitř komponenty `Amount`. 

Nyní si pouze musíme dát dobrý pozor na správnou aktulizaci stavu `cartProducts`.

```jsx
const Cart = () => {
  const [cartProducts, setCartProducts] = useState(products);

  const handleAmountChange = (index, amount) => {
    const newProducts = [...cartProducts];
    newProducts[index].amount = amount;
    setCartProducts(newProducts);
  }

  return (
    <div className="cart">
      <div className="cart__head">
        <h2>Košík</h2>
        <span>Položek: 1</span>
      </div>
      <div className="cart__items">
        {cartProducts.map((product, index) => (
          <CartItem 
            product={product}
            onAmountChange={(amount) => handleAmountChange(index, amount)}
          />
        ))}
      </div>
    </div>
  )
};
```

Konečně jsme ve fázi, kdy můžeme spočítat celkový počet položek v košíku. Výpočet provedeme přímo v těle komponenty `Cart`, aby se aktualizoval s každou změnou stavu.

```jsx
  let productCount = 0;
  cartProducts.forEach((product) => productCount += product.amount);

  return (
    <div className="cart">
      <div className="cart__head">
        <h2>Košík</h2>
        <span>Položek: {productCount}</span>
```
