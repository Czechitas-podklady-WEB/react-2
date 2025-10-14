## Předávání dat mezi komponentami

Představte si, že jsme v situaci, když potřebujeme poslat data z dceřiné komponenty do rodičovské komponenty. V Reactu to obvykle řešíme tak, že:
- v rodičovské komponentě vytvoříme funkci
- funkci jako prop předáme do dceřiné komponenty
- když potřebujeme komunikovat (poslat data), tak v dceřiné komponentě funkci zavoláme a data jí předáme jako parametr

Protože jsme v TypeScriptu, nesmíme zapomenout, že pro props dceřinné komponenty vytváříme `interface` a v něm musíme správně nastavit typ funkce, kterou komponenta od rodiče dostane.

```ts
function Parent = () => {

  const handleFormSubmit = () => {
    // kód funkce
  }

  return (
    <>
      <h1>Rodičovská komponenta</h1>
      <Child onFormSubmit={handleFormSubmit} />
    </>
  )
}
```

```ts
interface ChildProps {
  onFormSubmit: () => void;
}

function Child = ({onFormSubmit}: ChildProps) {

  const handleSubmit = () => {
    onFormSubmit(/* data, která chceme poslat */)
  }

  return (
    <form onSubmit={handleSubmit}>
      ...
    </form>
  )
}
```

Pokud chceme do rodičovské komponenty poslat nějaká data, musíme tento fakt zohlednit při nastavování typu funkce.
