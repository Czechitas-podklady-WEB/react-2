Jelikož moderní React přistupuje ke komponentám velmi funkcionálně, často správný běh naší aplikace závisí na principech z funkcionálního programování. Jedním z takových principů jsou takzvané :term{cs="Uzávěry" en="closures"}.

## Uzávěry

Na úvod opět zabrousíme do trochy teorie ohledně toho, jak přesně v JavaScriptu fungují proměnné a funkce. Začneme úplně jednoduchou funkcí ve vanilla JavaScriptu a brzy se dopracujeme opět k Reactu.

Představme si nějakou uplně hloupu hru, ve které klikáme na stránku, a po pěti kliknutích tak vyčerpáme všechny své životy a zemřeme.

```js
const startGame = () => {
  let health = 5;

  const handleClick = () => {
    health -= 1;

    if (health === 0) {
      alert('You are now dead!');
    }
  };

  document.addEventListener('click', handleClick);
};

startGame();
```

Všimněte si, že zde, podobně jako to známe z Reactu, vytváříme funkci uvnitř funkce. Když JavaScriptový engine vykonává nějakou funkci nebo blok kódu, po celou dobu vykonávání si pamatuje všechny lokální proměnné, které v něm byly vytvořeny. Jakmile vykonávání bloku skončí, všechny takto zapamatované proměnné se z paměti uvolní.

To je případ proměnné `health` vytvořené ve funkci `startGame`. Tato proměnná by zanikla ve chvíli, kdy funkce `startGame` skončí. Proměnnou `health` však zároveň používá funkce `handleClick`. Tato funkce se však poprvé spustí až ve chvíli, kdy uživatel klikne na stránku. To už ovšem funkce `startGame` dávno, dávno skončila a proměnná `health` by už byla dávno uvolněná z paměti. Funkce `handleClick` by se tak pokusila přistoupit k již neexistující proměnná a náš program by zhavaroval.

JavaScript tuto prekérní situaci řeší tak, že za nás proměnnou `health` udrží při životě i po skončení funkce `startGame`. Platí totiž, že když nějaká funkce používá proměnnou z nadřazeného bloku, JavaScript engine si zapamatuje, že takovou proměnnou nemá na konci jejího bloku zabít. Funkce si potom tuto proměnnou nese s sebou a udržuje ji při životě. Říkáme pak, že proměnná se do funkce uzavřela a vzniká tak :term{cs="uzávěr" en="closure"}. V našem případě se tedy proměnná `health` **uzavřela** do funkce `handleClick`.

Uzávěr takto zkraje možná zní jako velmi technická záležitost. V Reactu však uzávěry používáme úplně na každém kroku už od úplného začátku. Jen jsme si to zatím ve sladké neznalosti neuvědomovali.
