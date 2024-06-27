## Testování komponent

Protože pracujeme v Reactu, budeme asi nejčastěji potřebovat otestovat naše komponenty.

### jsdom

Abychom mohli testovat komponenty, potřebujeme do projektu přidat knihovnu `jsdom`, která částečně emuluje API prohlížeče a Vitest se tak může podívat na HTML výstup komponenty.

```bash
npm install --save-dev jsdom
```

Knihovnu **jsdom** musíme v konfiguračním souboru `vite.config.ts` nastavit jako prostředí pro běh testů:

```ts
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],

  // ⬇️ přidáme tento blok ⬇️
  test: {
    environment: 'jsdom',
  }
})
```

### React Testing Library

Dále budeme potřebovat i React Testing Library, která nám umožní psát testy, které napodobují, jak s aplikací interaguje uživatel a jaký vidí výstup.

Nebudeme tedy řešit, implementační detaily, ale pouze to, zda se komponenta správně chová.

```bash
npm install --save-dev @testing-library/react @testing-library/jest-dom
```

Protože React Testing Library pro nás bude renderovat jednotlivé komponenty, je zapotřebí, aby po sobě vždy uklidila a provedla tzv. *cleanup*. Abychom to nemuseli dělat manuálně u každého testu, můžeme si připravit malý soubor, který nastaví automatický cleanup po každém testu.

Ve složce `tests` v kořenové složce projektu si připravme soubor `setup.ts`:

```ts
import { afterEach } from 'vitest'
import { cleanup } from '@testing-library/react'
import '@testing-library/jest-dom/vitest'

// runs a clean after each test case (e.g. clearing jsdom)
afterEach(() => {
  cleanup();
})
```

A zároveň nastavme Vite, aby s tímto souborem počítalo a umělo použít nové assertion metody z React Testing Library.

Upravme ještě jednou soubor `vite.config.ts`:

```ts
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],

  test: {
    environment: 'jsdom',

    // ⬇️ doplníme následující 2 řádky ⬇️
    globals: true,
    setupFiles: './tests/setup.ts',
  }
})
```

### Testování komponenty

Nyní můžeme v našich testech renderovat jednotlivé komponenty a kontrolovat, jestli mají požadovaný výstup.

Mějme jednoduchou komponentu `Header.tsx`, která vypadá třeba takto:

```tsx
interface HeaderProps {
	title: string;
}

export const Header:React.FC<HeaderProps> = ({title}) => {
	return (
		<header>
			<h1>{title}</h1>
		</header>
	)
}
```

Ve stejné složce vytvoříme soubor `Header.test.tsx`:

```tsx
import { describe, test, expect } from 'vitest'
import { render, screen } from '@testing-library/react'

import { Header } from './Header'

describe('Header component', () => {
	test('renders headline', () => {
		render(<Header title="React component test" />);
		screen.debug();
	})
})
```

`screen.debug()` nám ukáže, jak vypadá HTML naší aplikace a my si můžeme zkontrolovat, zda je na výstupu vše v pořádku. To samozřejmě není žádný automatický text, kdybychom vždy museli manuálně zkontrolovat HTML. `screen.debug()` je takový `console.log()` pro Reactí aplikace - občas se při hledání chyb hodí, ale existují lepší způsoby.

Řádek s *debug* zakomentujme a nahraďme ho například tímto:

```ts
expect(screen.getByText('React component test')).toBeInTheDocument()
```

Vykreslila-li se komponenta správně a na "obrazovce" ke text, který jsme do komponenty předali jako *prop*, test v pořádku projde.

### Vyhledávání prvků na stránce

Pomocí jakých metod můžeme vyhledávat obsah na stránce:
- [dokumentace React Testing Library](https://testing-library.com/docs/react-testing-library/cheatsheet)

### Matchers

Matcher je metoda, kterou použijeme pro vyhodnocení testu. V předchozích kapitole to byla třeba metoda `toEqual()`, která uměla porovnavat očekávaný a skutečný výsledek. Pro React/DOM elementy používá React Testing Library metody z knihovny `jest-dom`, kterou už jsem si nainstalovali.

To mohou být metody jako `toBeInTheDocument()`, která zjistí, zda se daný text nachází ve výstupu. mezi další může patřit například `toBeVisible()`, `toContainHTML()`, `toBeChecked()`, apod. Kompletní výčet najdeme v dokumentaci:
- [dokumentace jest-dom](https://github.com/testing-library/jest-dom?tab=readme-ov-file#table-of-contents)
