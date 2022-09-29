## Úklid při odpojení komponenty

Jsou situace, kdy potřebujeme spustit kód ve chvíli, kdy komponenta zaniká. Například potřebujeme odstranit spuštěné časovače, nepotřebné posluchače událostí. Prostě potřebujeme, aby po sobě komponenta uklidila.

Pokud funkce, která se spouští v `useEffect`, vrátí další funkci, tak se tato :term{cs="uklízecí funkce" en="cleanup function"} zavolá těsně před tím, než komponenta zanikne.

```jsx
useEffect(
  () => {
    // tento kód se spustí jenom po úvodním vykreslení
		// zde např. nastartujeme časovače, přidáme event listenery,
		// spustíme načítání dat z API

    return () => {
      // tento kód se spustí předtím, než komponenta zanikne
			// zde zrušíme časovače, odstraníme event listenery,
			// přerušíme nedokončená volání API, apod.
    }
  },
  []
);
```

### Proč potřebujeme uklízecí funkci?

Představme si komponentu, ve které při připojení komponenty nastavíme event listener na celé okno prohlížeče nebo spustíte časovač, který se bude spouštět jednou za *x* vteřin. Tyto event listenery nebo časovače zůstanou aktivní i poté, když komponentu odpojíme.

I když už naše komponenta na stránce nebude, event listenery budou stále fungovat a časovače stále tikat. Pokud bychom se ve spouštěných funkcích odkazovali např. na stav komponenty, máme další problém, protože komponenta a její stav už nemusí existovat. Ale o tom až později.

Ukažmě si jednoduchou komponentu, která při svém připojení do stránky nastartuje časovač, který každou vteřinu vypíše do konzole prohlížeče slovo *"tik"*.

```jsx
const Metronome = () => {

	useEffect(
		() => {
			setInterval(
				() => { console.log("tik"); },
				1000
			);
		},
		[]
	);

	return <div>Metronom, který tiká v konzoli</div>;
}
```

Když takovou komponentu zobrazíme na stránce, uvidíme v konzoli, že se nám každou vteřinu vypíše nové slovo. Když v naší aplikaci komponentu odpojíme (např. tím, že přejdeme na jinou stránku, nebo komponentu pomocí podmíněného zobrazení skryjeme), zjistíme, že časovač stále funguje a nadále tiká v konzoli.

Do komponenty potřebujeme přidat i uklízecí funkci, která při odpojení komponenty časovač zastaví.


```jsx
const Metronome = () => {

	useEffect(
		() => {
			const myTimer = setInterval(
				() => { console.log("tik"); },
				1000
			);

			// funkce vrácená z useEffect,
			// se spustí při odpojení komponenty
			return () => {
				clearInterval(myTimer)
			}
		},
		[]
	);

	return <div>Metronom, který tiká v konzoli</div>;
}
```