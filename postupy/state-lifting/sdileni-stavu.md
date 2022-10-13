## Sdílení stavu

Nejčastějí chceme pomocí contextu sdílet nějaký stav. V naší ukázce by ve stavu byl uložený objekt se nastavením měny. Ten bychom pak použili jako hodnotu v context provideru.

```jsx
const App = () => {
  const [settings, setSettings] = useState({
    currency: 'CZK',
  });
  
  return (
    <SettingsContext.Provider value={settings}>
```

Zároveň je však třeba všem, kdo context používají poskytnout příležitost jej nějak změnit. Například nastavit jinou měnu. K tomu si vyrobíme funkci `setCurrency`.

```jsx
const App = () => {
  const [settings, setSettings] = useState({
    currency: 'CZK',
  });
  
  const setCurrency = (currency) => {
    setSettings({ ...settings, currency });
  }

  return (
    <SettingsContext.Provider value={{ ...settings, setCurrency }}>
```

Díky tomu, že takto do contextu pošleme i funkcu `setCurrency`, kdokoliv uvnitř contextu si pak může tuto funkci z contextu vytáhnout a použít ji k nastavení měny.

```js
const { currency, setCurrency } = useSettings();
```
