## useCallback a znovuvytváření funkcí v komponentě

Nejprve si v krátkosti zopakujme, že v JavaScriptu funkce vykazují referenční rovnost. To znamená, že se považují za shodné, pouze pokud obě ukazují na stejný objekt. Když nadefinujeme dvě funkce s identickým kódem uvnitř, a při porovnání *nebudou sobě rovné*.

```js
const first = () => {
	return 1 + 2; // stejné jako v druhé funkci
}

const second = () => {
	return 1 + 2; // stejné jako v první funkci
}

// Stejná implementace, ale dva různé objekty
first === second; // false

// Stejné objekty
first === first; // true
```

Proč je to pro nás důležité v kontextu Reactu? V předchozích částech jsme si ukázali, že funkce tvořící komponentu v Reactu se vždy celá spustí, kdykoliv dojde k aktualizaci/překreslení komponenty. Máme-li uvnitř komponenty nadefinované nějaké funkce, vytvoří se tyto funkce pokaždé znovu.
