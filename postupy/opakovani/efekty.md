## Efekty

Tzv. *efekty* používáme ve chvíli, kdy potřebujeme zareagovat na určité situace, které nastávají během vykreslování komponenty. Například chceme určitý kód spustit ve chvíli, když se komponenta poprvé objeví na stránce.

Efekty jsou velmi podobné událostem. Když uvnitř komponenty něco nastane, chceme spustit funkci, která na to zareaguje. K vytvoření efektu používáme funkci `useEfect`.

```jsx
const App = () => {
  useEffect(() => {
    console.log('aplikace se spustila');
  }, []);

  return (
    <>
      <h1>Aplikace</h1>
      <p>Textový obsah naší super appky.</p>
    </>
  );
};
```

Funkce useEffect má dva parametry. Prvním je funkce, která se má zavolat a druhý parametr říká, za jakých okolností se má naše funkce volat.

- Když druhý parametr chybí, funkce se spustí při každém překreslení komponenty.
- Prázdné pole `[]` znamená, že se efekt spustí pouze ve chvíli, kdy se komponenta poprvé objeví na stránce.
- Připadně do pole můžeme napsat název stavové proměnné a efekt se spustí pokaždé, když dojde ke změně tohoto stavu.
