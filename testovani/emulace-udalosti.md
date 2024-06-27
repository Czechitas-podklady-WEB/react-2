## Emulace událostí

V běžné aplikaci samozřejmě nemáme jen statické komponenty, u kterých bychom testovali pouze, zda na výstupu generují správný titulek nebo něco podobného.

Běžně máme komponenty, které obsahují stav, a jako reakci na nastalou událost mohou stav změnit.

React Testing Library nám umožňuje události na elementech vyvolávat a poté zkontrolovat, zda se výstup adekvátně změnil.

Představme si typický příklad komponenty `Counter.tsx` s počitadlem kliků:

```tsx
import { useState } from 'react'

export const Counter : React.FC = () => {
  const [count, setCount] = useState(0)

  return (
    <>
      <h2>Count: {count}</h2>
      <button onClick={() => {setCount((prev) => prev + 1)}}>Click me</button>
    </>
  )
}
```

Nyní bychom potřebovali napsat test, který by zjistil, zda se po kliknutí na tlačítko změní hodnota v nadpisu. Vytvoříme si soubor `Counter.test.tsx`.

Můžeme použít funkci `fireEvent` a simulovat kliknutí na elementu, který jsme předtím vybrali jako prvek, který obsahuje text `'Click me'`. Zároveň si najdeme na obrazovce prvek, který obsahuje výchozí text `'Count: 0'`, a následně očekáváme, že po simulovaném kliknutí se změnil stav komponentě, komponenta se překreslila a náš elment nyní obsahuje text `'Count: 1'`.

```tsx
import { describe, test, expect } from 'vitest'
import { render, screen, fireEvent } from '@testing-library/react'

import { Counter } from './Counter'

describe('Counter component', () => {
	test('click button to increase count', () => {
		render(<Counter />);

		const count = screen.getByText('Count: 0')
		const button = screen.getByText('Click me')

		fireEvent.click(button)

		expect(count.textContent).toBe('Count: 1');
	})
})
```