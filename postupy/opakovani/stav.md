## Stav

*Stav* (state) je základem každé interaktivní komponenty. Stav si můžeme představit jako vlastnosti předmětu v reálném světě, které se mohou během životnosti věci měnit. Například u auta se průběžně mění stav nádrže, rychlost, počet najetých kilometrů, apod. Pokud naše komponenta představuje například položku v úkolníčku, může mít stav splněno/nesplněno.

Pro vytvoření stavu v Reactu používáme funkci `useState`. Jako parametr do ní předáme vychozí hodnotu stavu. Funkce vrátí pole, které obsahuje dva prvky - první je samotný stav, druhá je funkce, pomocí které můžeme stav měnit.

```jsx
import React, { useState } from 'react';

const Auto = () => {
  const [tankLevel, setTankLevel] = useState('full');

  return <div className="auto">Tank level: {tankLevel}</div>;
};
```

Když chceme hodnotu stavu změnit, použijeme funkci, kterou jsme dostali z `useState` pro tento účel.

```jsx
setTankLevel('empty');
```
