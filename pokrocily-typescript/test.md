## Test

Zkus si sama v hlavě zodpovědět na následující otázky, než se podíváš na odpověď.

### 1. Je veškerý validní javascriptový kód zároveň validním typescriptovým kódem?

Ano! TypeScript je tzv. "superset" JavaScriptu. To znamená, že obsahuje a umí totéž, co JavaScript, jenom ho rozšiřuje o typy. To nám hodně ulehčuje přechod na TS ve velkých projektech - náš projekt může kombinovat `.js` a `.ts` soubory.

::fig{src=assets/js-vs-ts.png size=70}


### 2. Co znamená otazník v typu `{ name?: string; }` ?

Property `name` je nepovinné.

### 3. Jaký je rozdíl mezi `null` a `undefined`?

Představte si, že máte knihovnu, ve které nejsou žádné knížky, protože jste tam žádné nedali.

Pokud jste na to jenom zapomněli, value knihovny by byla `undefined`. Knihovna existuje (proměnná je deklarovaná), ale nic v ní není, protože tam nikdo nic nedal.

Pokud jste do knihovny ale nic nedali schválně, víte, že tam nic nemá být, můžete jí přiřadit hodnotu naznačující	"prázdnost" - `null`.

`Null` musí někdo přiřadit, `undefined` je defaultně vše, co nemá nic přiřazené.

### 4. Co pro TypeScript znamená, když za proměnnou napíšu `as const`?

Typ proměnné se bude řídit literal types, místo např. `string[]` bude přijímat pouze specifické stringy, které jsou v proměnné uložené.

### 5. Co je to `type inference`?

TypeScript si spoustu typů odvodí sám i bez naší pomoci. Pokud do proměnné vložíme string `"hello"`, nemusíme specifikovat, že je to proměnná typu `string`.

Stejně tak pokud třeba `useState("hello")` rovnou dostane "hello" jako initial hodnotu, TypeScript už ví, že do něj může	nastavit pouze `string`. Pokud by ale initial hodnota byla prázdná `useState(null)`, TypeScript by si myslel, že žádnou jinou hodnotu než `null` state mít nemůže a musíme ho otypovat samy jako `useState&lt;string | null&gt;(null)`.

### 6. Proč by TypeScript měl být `devDependency`?

`devDependencies`, tj. development dependencies, obsahují všechno, co potřebujete pouze při vývoji, ne	do produkce/při nasazení (deploy) svojí stránky. Cokoli je tak označené, to např. Vite může při zpracování vašeho kódu přeskočit.

TypeScript sem patří proto, že aby mohl běžet v JavaScriptovém prostředí (třeba prohlížeč), musí být zkompilovaný (přepsaný) do JavaScriptu. Vy jste se s tím nesetkaly, protože za vás kompilaci na pozadí řeší React při každém `npm start` nebo `npm build`.

### 7. Lze vytvořit nový typ ze dvou již existujících typů?

```ts
interface NewType extends OldType {
  newTypeProperty1: string;
  newTypeProperty2: string;
}
```

nebo

```ts
type NewType & OldType = {
  newTypeProperty1: string;
  newTypeProperty2: string;
}
```

### 8. Můžeme TypeScriptu "lhát" a zpětně ho přesvědčit, že je nějaké proměnná jiného typu než si myslí?

Bohužel můžeme. Stačí za proměnnou přidat `as NewType`. Ideálně bychom to dělat neměli, protože pak ztrácí TypeScript smysl, ale může se stát, že si potřebujeme jen něco otestovat a tohle nám může pomoct. Kde se nám ještě může hodit je pokud od nepořádného kolegy dostaneme nějaké ošklivé `any`, ale my víme, že to je string a potřebujeme zjistit jeho délku, `as string` by nám pomohlo (a pak šup to `any` opravit!).

::fig{src=assets/as-any.png size=70}
