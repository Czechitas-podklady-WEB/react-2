## Životní cyklus komponenty

Životním cyklem (lifecycle) komponenty označujeme fáze, kterými komponenta prochází během své existence v aplikaci. Reactí komponenta během svého životního cyklu projde třemi fázemi:

1. **Mount**, neboli fáze **připojení**, nastává ve chvíli, kdy je komponenta vytvořena a vložena do DOM v prohlížeči. Jinými slovy, život komponenty zde začíná. Tato fáze může nasat pouze jednou a často se jí říká :term{cs="úvodní vykreslení" en="initial render"}.

2. **Update**, neboli fáze **aktualizace** komponenty, která nastane ve chvíli, kdy se komponenta aktualizuje a :term{cs="překreslí" en="re-render"}.

3. **Unmount**, neboli fáze **odpojení** komponenty nastáve ve chvíli, kdy je komponenta odstraněna z DOM.

Ve starších verzích Reactu, kdy se komponenty vytvářely výhradně jako javascriptové třídy *(class components)*, měla komponenta přímo metody, které se spouštěly v konkrétních fázích životního cyklu.

My píšeme tzv. funkční komponenty, kde pro spuštění kódu v jednotlivých fázích životního cyklu používáme `useEffect`.
