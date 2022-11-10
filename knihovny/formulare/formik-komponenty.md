## Formik komponenty

Formik je sice užitečný a zjednodušil nám spoustu práce, ale tak jak jsme ho používali doposud je to stále velmi neohrabané a nepříliš elegantní. Postup jsme si ale ukazovali proto, abychom pochopili, jak celá věc interně funguje.

Pro maximální zjednodušení práce nabízí Formik vlastní komponenty, které lze použít pro vytváření formulářů. Jedná se komponenty `Formik`, `Form`, `Field`, `ErrorMessage` a ještě pár dalších.

Komponenty samozřejmě před použitím musíme naimportovat.

```jsx
import { Formik, Field, Form, ErrorMessage } from 'formik';
```

Hlavní komponenta `Formik` zcela nahrazuje použití hooku `useFormik`. Používá ho interně, ale my se jím nemusíme zabývat. Veškeré nastavení formuláře provedeme přes props komponenty.

```jsx
const Form = () => {
	return (
		<Formik
			initialValues={{
				firstName: 'Jana',
				lastName: 'Novotná'
			}}
			validate={validate}
			onSubmit={(values, {setSubmitting}) => {
				console.log(values);
				setSubmitting(false);
			}}
		>


		</Formik>
	);
}
```

Další komponenty pak použijeme uvnitř `<Formik>...</Formik>` pro snadné vytvoření formulářových polí, které už mají veškerou funkcionalitu zabudovanou v sobě.

```jsx
<Form>
	<label htmlFor="firstName">First Name</label>
	<Field name="firstName" type="text" />
	<ErrorMessage name="firstName" />

	<label htmlFor="lastName">Last Name</label>
	<Field name="lastName" type="text" />
	<ErrorMessage name="lastName" />

	<button type="submit">Submit</button>
</Form>
```

Vidíme, že se již nemusíme starat o přidávání událostí na jednotlivá pole, ani o testování, zda u pole existuje nebo neexistuje chybová hláška. Vše je pro nás nastaveno automaticky.

### Komponenta Field

Komponenta `<Field>` automaticky vytváří HTML prvek `<input>` příslušného typu. Potřebujeme-li jiný typ (`<select>`, `<textarea>`), můžeme použít prop `as`. Podrobnosti v [dokumentaci](https://formik.org/docs/api/field).

```jsx
<Field name="city" as="select">
	<option value="Praha">Praha</option>
	<option value="Brno">Brno</option>
	<option value="Ostrava">Ostrava</option>
</Field>

<Field name="comment" as="textarea" />
```

### Komponenta ErrorMessage

Komponenta `<ErrorMessage>` má jako standardní výstup pouze text chybového hlášení pro dané pole. Chceme-li, aby bylo hlášení obaleno do HTML značky, stačí její název uvést jako hodnotu prop `component`.

```jsx
<ErrorMessage name="firstName" component="span" />
```

Podrobnosti a další možnosti v [dokumentaci](https://formik.org/docs/api/errormessage).