## Formuláře v Reactu

Základní práci s formulářovými prvky (`input`, `select`, `button`, apod.) známe už z dřívějška. Nikdy jsme se ale nevěnovali zpracování formulářů ve větším měřítku. Formuláře a formulářové prvky jsou nedílnou součástí téměř každé webové aplikace a může se stát, že jich ve své aplikaci můžeme mít klidně i desítky. Pak je vhodné mít nějaký obecný a univerzální přístup ke zpracování formulářů, abychom pro každý formulář nemuseli opakovaně psát de facto stejný kód stále dokola.

Připomeňme si, jak jsme doposud s formuláři pracovali. Obvykle jsme:
- pro každé pole vytvořili stavovou proměnnou,
- ke každému prvku jsme přidali událost `onChange`, ve které jsme měnili stav podle hodnoty zadané v poli,
- na formulář jsme přidali událost `onSubmit`, která se zavolá při odeslání formuláře.

Kód naší komponenty může vypadat například takto:

```jsx
const Form = () => {
  const [firstName, setFirstName] = useState('');
  const [lastName, setLastName] = useState('');

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(firstName, lastName);
  }

  return (
    <form onSubmit={handleSubmit}>
      <label htmlFor="firstname">Jméno</label>
      <input
        type="text"
        id="firstName"
        name="firstName"
        value={firstName}
        onChange={(e) => { setFirstName(e.target.value); }}
      />
      <label htmlFor="lastname">Příjmení</label>
      <input
        type="text"
        id="lastName"
        name="lastName"
        value={lastName}
        onChange={(e) => { setLastName(e.target.value); }}
      />
      <button type="submit">Odeslat</button>
    </form>
  );
}
```

Náš příklad zatím obsahuje dvě pole a nevypadá složitě. Představíme-li si formulář, který má polí dvacet, a podobných formulářů máme v aplikaci několik, už nám takto jednoduchý přístup začne překážet. Celý postup práce s formuláři chceme pokud možno co nejvíce zobecnit a zautomatizovat.

Nevýhodou našeho příkladu je třeba nutnost používat konkrétní funkce pro nastavování stavu pro jednotlivé hodnoty. Pojďme náš příklad upravit tak, aby používal jeden společný objekt pro všechna data ve formuláři.

```jsx
const Form = () => {
  const [formData, setFormData] = useState({});

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(formData);
  }

  const handleChange = (e) => {
    setFormData({
      ...formData,
      [e.target.name]: e.target.value
    });
  }

  return (
    <form onSubmit={handleSubmit}>
      <label htmlFor="firstname">Jméno</label>
      <input
        type="text"
        id="firstName"
        name="firstName"
        value={formData.firstName}
        onChange={handleChange}
      />
      <label htmlFor="lastname">Příjmení</label>
      <input
        type="text"
        id="lastName"
        name="lastName"
        value={formData.lastName}
        onChange={handleChange}
      />
      <button type="submit">Odeslat</button>
    </form>
  );
}
```

Náš kód se tolik nezměnil, ale má obrovskou výhodu. Nyní můžeme do JSX přidávat další a další formluářové prvky, ale v kódu, který se o formulář stará už nemusíme nic měnit. V objektu `formData` bude pro každý vyplněný formulářový prvek vlastnost se jménem prvku (hodnota jeho atributu `name`).

Uvedený kód není příliš složitý a celkem dobře se používá. Pokud bychom ale měli v aplikaci formulářů hodně, museli bychom v každém části tohoto kódu opakovat. Pojďme si celou věc ještě více zjednodušit a zobecnit tím, že si napíšeme vlastní *hook* na zpracování formulářů.
