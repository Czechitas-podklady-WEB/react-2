## Testování komponent

Protože pracujeme v Reactu, budeme asi nejčastěji potřebovat otestovat naše komponenty.

### Instalace balíčků

Nejprve si nainstalujeme a nakonfigurujeme všechny potřebné balíčky:

```bash
npm i -D vitest jsdom @testing-library/react @testing-library/user-event @testing-library/jest-dom
```

Instalujeme:
- **jsdom**: knihovna, která částečně emuluje API prohlížeče a Vitest se tak může podívat na HTML výstup komponenty a provádět oproti tomuto výstupu testy.
- **React Testing Library**: knihovna, která nám umožní psát testy, které napodobují, jak s aplikací interaguje uživatel a jaký vidí výstup. Nebudeme tedy řešit, implementační detaily, ale pouze to, zda se komponenta správně chová.

### Konfigurace testovacího prostředí

V projektu si vytvoříme **nový soubor** `vitest.config.ts`, ve kterém pak knihovnu **jsdom** nastavíme jako prostředí pro běh testů:

```ts
import { defineConfig } from 'vitest/config'

export default defineConfig({
  test: {
    environment: 'jsdom',
    globals: true,
    setupFiles: './src/tests/setup.ts',
  },
})
```

Ve složce `tests`, kterou už v projektu máme z dřívějška, si připravme soubor `setup.ts`, do kterého vložme následující řádek:

```ts
import '@testing-library/jest-dom/vitest'
```

Tím se nám zpřístupní ruzné podpůrné funkce pro prácí s DOM elementy v testech.

### Konfigurace pro TypeScript

Aby TypeScript znal testovací funkce, které budeme používat, přidejme následující do souboru `tsconfig.json`:

```json
{
  "compilerOptions": {
    "types": ["vitest/globals", "@testing-library/jest-dom"]
  }
}
```


## Testování komponenty

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
