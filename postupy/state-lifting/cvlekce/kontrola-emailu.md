---
title: Kontrola emailu
demand: 3
---

V tomto cvičení budeme pracovat s komponentou `EmailInput`, která jednoduchým způsobem validuje zadaný e-mail. Kód komponenty:

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

Všimněte si, že jde o uncontrolled componentu, která spravuje svůj vlastní stav. Budeme chtít tento stav povýšit a udělat z `EmailInput` controlled componentu.

1. Založte si nový React projekt. V komponentě `App` vytvořte jednoduchý formulář s komponentou `EmailInput` tlačítkem submit. Vyzkoušejte, že komponenta `EmailInput` validuje zadaný e-mail.
1. Pozorujte, že pokud bychom chtěli formulář odeslat, nemáme se z komponenty `App` jak dostat k uživatelem zadanému e-mailu uzavřenému (jako stav) uvnitř komponenty `EmailInput`.
1. Povyšte stav komponenty `EmailInput` na úroveň komponenty `App`. Budeme potřebovat znát nejen samotný e-mail, ale také to, zda je validní. Hodnota stavu tedy bude objekt s touto strukturou:
   ```js
   {
     value: 'pokusnik.kokosnik@gmai.com',
     valid: true,
   }
   ```
1. Tento stav předáme do konponenty `EmailInput` pomocí prop s názvem `email`. Komponenta `EmailInput` navíc bude očekávat callback prop `onChange`, která bude komponentě `App` posílat všechny změny zevnitř `EmailInput`.
