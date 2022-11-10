## Knihovna Formik

Teď když víme, jak vlastní hook pro zpracování formuláře v principu funguje, mohli bychom si ho rozšířit i o další funkcionalitu, např. kontrolu správnosti vyplněných polí, neboli validaci.

V ekosystému Reactu existuje spousta už hotových řešení pro zpracování a validaci formulářů. Pojďme si práci zjednodušit ještě víc a použít oblíbenou knihovnu **Formik**.

Domovskou stránku knihovny a dokumentaci k ní najdeme na [formik.org](https://formik.org/).

Knihovnu do projektu přidáme pomocí:
```bash
npm install --save formik
```

Budeme pokračovat s naším příkladem, ale náš formulářový hook nahradíme sofistikovanějším Formikem, který má i spoustu dalších možností.

Formik obsahuje hook `useFormik`, který opět *úplně náhodou* funguje velmi podobně jako hook, který jsme si před chvíli naprogramovali sami. Podrobnosti v [dokumentaci](https://formik.org/docs/api/useFormik).

Naše komponenta bude vypadat takto:

```jsx
import { useFormik } from 'formik';

const Form = () => {
	const formik = useFormik(
		initialValues: {
			firstName: 'Jana',
			lastName: 'Novotná'
		},
		onSubmit: (formData) => {
			console.log(formData);
		}
	);

	return (
		<form onSubmit={formik.handleSubmit}>
			<label htmlFor="firstName">Jméno</label>
			<input
				type="text"
				id="firstName"
				name="firstName"
				value={formik.values.firstName}
				onChange={formik.handleChange}
			/>
			<label htmlFor="lastname">Příjmení</label>
			<input
				type="text"
				id="lastName"
				name="lastName"
				value={formik.values.lastName}
				onChange={formik.handleChange}
			/>
			<button type="submit">Odeslat</button>
		</form>
	);
}
```

### Validace formuláře

Náš formulář funguje stejně jako předtím. V předchozím příkladu jsme ale neřešili validaci formulářových polí.

Formik se nestará jen o aktuální (a výchozí) hodnoty jednotlivých formulářových polí, ale sleduje u každého formulářového prvku i validační chyby a vybere správnou chybovou zprávu.

Můžeme si napsat validační funkci, která od Formiku dostane jako parametr objekt se všemi hodnotami. Ve funkci si můžeme každou hodnotu zkontrolovat. Z funkce vracíme objekt, který obsahuje chyby pro špatně vyplněná pole.

Je-li formulářový prvek nevalidní, vytvoříme v objektu vlastnost se jménem formulářového prvku, a do její hodnoty dáme chybovou zprávu pro toto pole.


```jsx
const validate = (values) => {
	const errors = {};

	if (!values.firstName) {
		errors.firstName = 'Povinné pole';
	} else if (values.firstName.length > 15) {
		errors.firstName = 'Musí být dlouhé maximálně 15 znaků';
	}

	if (!values.lastName) {
		errors.lastName = 'Povinné pole';
	} else if (values.lastName.length > 20) {
		errors.lastName = 'Musí být dlouhé maximálně 20 znaků';
	}

	return errors;
};
```

Funkci pak předáme do hooku `useFormik`. Ve formuláři pak můžeme využít objekt `errors` k zobrazení chybových zpráv.

Naše komponenta bude vypadat následovně:

```jsx
const Form = () => {
	const formik = useFormik(
		initialValues: {
			firstName: 'Jana',
			lastName: 'Novotná'
		},
		validate: validate,
		onSubmit: (formData) => {
			console.log(formData);
		}
	);

	return (
		<form onSubmit={formik.handleSubmit}>
			<label htmlFor="firstName">Jméno</label>
			<input
				type="text"
				id="firstName"
				name="firstName"
				value={formik.values.firstName}
				onChange={formik.handleChange}
			/>
			{ formik.errors.firstName ? <p>{formik.errors.firstName}</p> : null }

			<label htmlFor="lastname">Příjmení</label>
			<input
				type="text"
				id="lastName"
				name="lastName"
				value={formik.values.lastName}
				onChange={formik.handleChange}
			/>
			{ formik.errors.firstName ? <p>{formik.errors.firstName}</p> : null }

			<button type="submit">Odeslat</button>
		</form>
	);
}
```

Protože Formik volá událost `handleChange` při každém stisku klávesy a pokaždé všechna pole také validuje, zobrazí se nám hned při prvním napsaném písmenu chyby i u polí, ke kterým jsme se při vyplňování formuláře zatím nedostali.

Formik kromě objektů `initialValues`, `values` a `errors` obsahuje i objekt `touched`, ve kterém pro každý formulářový prvek obsahuje `true/false` hodnotu, zda už uživatel dané pole navštívil a začal ho upravovat.

Aby vše fungovalo správně, musíme na každý prvek přidat ještě událost `onBlur`, která se volá pokaždé, když uživatel opustí daný prvek (ztratí *focus*).

```jsx
<input
	type="text"
	id="firstName"
	name="firstName"
	value={formik.values.firstName}
	onChange={formik.handleChange}
	onBlur={formik.handleBlur}
/>
```

My potom můžeme využít objekt `touched` k tomu, abychom chyby zobrazili jen u těch polí, která už se uživatel pokusil vyplnit.

```jsx
{formik.touched.firstName && formik.errors.firstName ? (
  <p>{formik.errors.firstName}</p>
) : null}
```
