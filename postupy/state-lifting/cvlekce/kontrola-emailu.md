---
title: Kontrola emailu
demand: 3
---

Vytvořte jednoduchý formulář obsahující políčko pro zadání e-mailu. Políčko by mělo ověřovat, že jde o validní e-mailovu adresu. Při odeslání formuláře data zatím pouze vypíšeme do konzole. 

Komponentu `EmailInput`, která jednoduchým způsobem validuje zadaný e-mail, máme předepsanou.

```jsx
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

Všimněte si, že jde o *uncontrolled* komponentu, která spravuje svůj vlastní stav. Budeme chtít tento stav povýšit a udělat z `EmailInput` *controlled* komponentu.

1. Založte si nový React projekt. Vytvořte komponentu `OrderForm`, ve které bude jednoduchý formulář s komponentou `EmailInput` a tlačítkem *submit*. Zapojte komponentu do aplikace a vyzkoušejte, že `EmailInput` správně validuje zadaný e-mail.
1. Pozorujte, že pokud bychom chtěli formulář odeslat, nemáme se z komponenty `OrderForm` jak dostat k uživatelem zadanému e-mailu uzavřenému (jako stav) uvnitř komponenty `EmailInput`.
1. Povyšte stav komponenty `EmailInput` na úroveň komponenty `OrderForm`. Budeme potřebovat znát nejen samotný e-mail, ale také to, zda je validní. Hodnota stavu tedy bude objekt s touto strukturou:
   ```js
   {
     value: 'pokusnik.kokosnik@example.com',
     valid: true,
   }
   ```
1. Tento stav předáme do komponenty `EmailInput` pomocí *prop* s názvem `email`. Komponenta `EmailInput` navíc bude očekávat *callback prop* `onChange`, která bude komponentě `OrderForm` posílat všechny změny zevnitř `EmailInput`.
