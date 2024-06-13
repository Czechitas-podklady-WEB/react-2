## Vlastní hook na zpracování formulářů

Co je :term{cs="vlastní hook" en="custom hook"}? Kromě zabudovaných hooků v Reactu (`useState`, `useEffect`, `useRef`, apod.) si mohou vývojáři psát i hooky vlastní. Hook může obsahovat logiku, která jde pak jednoduše sdílet mezi komponentami. To se nám *úplně náhodou* hodí, protože chceme udělat obecné zpracování formulářů, použitelné ve všech formulářích naší rozsáhlé aplikace.

Vlastní hook je velmi podobný normální React komponentě. Je to funkce, která může obsahovat vlastní stav, vlastní efekty, další pomocné funkce. Hook obvykle nevrací JSX jako klasická komponenta, ale vystavuje navenek některé ze svých interních stavů nebo metod.

Vlastní hooky musí na začátku svého jména obsahovat slovo `use`, nazvěme tedy náš hook `useForm`.

Do hooku potřebujeme vyseparovat stav a logiku, která se stará o náš formulář.

```tsx
const useForm = () => {
  const [formData, setFormData] = useState<Record<string, string>>({});

  const handleChange = (e: ChangeEvent<HTMLInputElement>) => {
    setFormData({
      ...formData,
      [e.target.name]: e.target.value
    });
  }

  const handleSubmit = (e: FormEvent) => {
    e.preventDefault();
    // ...
  }

  return { formData, handleChange, handleSubmit };
}
```

Všimněte si, že hook na konci vrací stavovou hodnotu a funkce pro zpracování událostí při změně pole a odeslání formuláře.

V naší komponentě hook použijeme následovně.

```jsx
const Form = () => {
  const {formData, handleChange, handleSubmit} = useForm();

  return (
    <form onSubmit={handleSubmit}>
      <label htmlFor="firstname">Jméno</label>
      <input
        type="text"
        id="firstname"
        name="firstname"
        value={formData.firstname}
        onChange={handleChange}
      />
      <label htmlFor="lastname">Příjmení</label>
      <input
        type="text"
        id="lastname"
        value={formData.lastname}
        onChange={handleChange}
      />
      <button type="submit">Odeslat</button>
    </form>
  );
}
```

Kód naší komponenty se nám použitím hooku krásně zjednodušil. Ale ještě potřebujeme upravit několik drobností.

Do hooku chceme jako parametr předat výchozí hodnoty formulářových polí.

Všimněte si také, že uvnitř hooku jsem odstranili specifický kód, který se prováděl při odeslání formuláře. V našem příkladu sice šlo jenom o `console.log`, ale na principu to nic nemění.

Protože hook chceme používat univerzálně pro více formulářů, nemůžeme v něm mít kód specifický pro konkrétní formulář. Data z každého formuláře bude potřeba zpracovat jinak, odeslat na jiný API endpoint, apod. Funkce pro zpracování konkrétního formuláře musí zůstat v komponentě, kde je daný formulář, ale můžeme ji do hooku předat jako callback v podobě druhého parametru, který zavoláme v případě odeslání formuláře.

Náš hook bude vypadat následovně:

```tsx
const useForm = (
  initialValues: Record<string, string> = {},
  onSubmit: (fromData: Record<string, string>) => void) => {
  const [formData, setFormData] = useState<Record<string, string>>(initialValues);

  const handleChange = (e: ChangeEvent<HTMLInputElement>) => {
    setFormData({
      ...formData,
      [e.target.name]: e.target.value
    });
  }

  const handleSubmit = (e: FormEvent) => {
    e.preventDefault();
    onSubmit(formData);
  }

  return { formData, handleChange, handleSubmit };
}
```

Naše komponenta zůstane zůstane v podstatě beze změny, pouze do hooku jako parametry předáme výchozí hodnoty formuláře a funkci, která se zavolá při odeslání formuláře.

```tsx
const Form = () => {
  const [formData, handleChange, handleSubmit] = useForm(
    {
      firstName: 'Jana',
      lastName: 'Novotná'
    },
    (formData) => {
      console.log(formData);
    }
  );

  return (
    <form onSubmit={handleSubmit}>
      <label htmlFor="firstName">Jméno</label>
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

Náš vlastní hook nyní můžeme používat pro libovolný počet formulářů v různých komponentách naší aplikace.
