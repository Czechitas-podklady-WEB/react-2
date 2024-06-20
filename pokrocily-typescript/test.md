## Test

<details>
	<summary>
		Je veškerý validní javascriptový kód zároveň validním typescriptovým kódem?
	</summary>
	<p>
		Ano! TypeScript je tzv. "superset" JavaScriptu. To znamená, že
		obsahuje a umí totéž, co JavaScript, jenom ho rozšiřuje o typy.
		To nám hodně ulehčuje přechod na TS ve velkých projektech - náš
		projekt může kombinovat <code>.js</code> a <code>.ts</code> soubory.
	</p>
	::fig{src=assets/js-vs-ts.png size=70}
</details>

<details>
	<summary>
		Co znamená otazník v typu <code>{ name?: string; }</code>
	</summary>
	<p>Property <code>name</code> je nepovinné.</p>
</details>

<details>
	<summary>
		Jaký je rozdíl mezi <code>null</code> a <code>undefined</code>?
	</summary>
	<p>Představte si, že máte knihovnu, ve které nejsou žádné knížky, protože jste tam žádné nedali.</p>
	<p>
		Pokud jste na to jenom zapomněli, value knihovny by byla <code>undefined</code>.
		Knihovna existuje (proměnná je deklarovaná), ale nic v ní není, protože tam nikdo nic nedal.
	</p>
	<p>
		Pokud jste do knihovny ale nic nedali schválně, víte, že tam nic nemá být, můžete jí přiřadit
		hodnotu naznačující	"prázdnost" - <code>null</code>.
	</p>
	<p>
		<code>Null</code> musí někdo přiřadit, <code>undefined</code> je defaultně vše,
		co nemá nic přiřazené.
	</p>
</details>

<details>
	<summary>
		Co pro TypeScript znamená, když za proměnnou napíšu
		<code>as const</code>?
	</summary>
	<p>
		Typ proměnné se bude řídit literal types, místo např. <code>string[]</code> bude
		přijímat pouze specifické stringy, které jsou v proměnné uložené.
	</p>
</details>

<details>
	<summary>
		Co je to <code>type inference</code>?
	</summary>
	<p>
		TypeScript si spoustu typů odvodí sám i bez naší pomoci. Pokud do proměnné vložíme string <code>"hello"</code>, nemusíme specifikovat, že je to proměnná typu <code>string</code>.
		Stejně tak pokud třeba <code>useState("hello")</code> rovnou dostane "hello" jako initial
		hodnotu, TypeScript už ví, že do něj může	nastavit pouze <code>string</code>.
		Pokud by ale initial hodnota byla prázdná <code>useState(null)</code>, TypeScript by si myslel,
		že žádnou jinou hodnotu než <code>null</code> state mít nemůže a musíme ho otypovat sami
		jako <code>useState&lt;string | null&gt;(null)</code>.
	</p>
</details>

<details>
	<summary>
		Proč by TypeScript měl být <code>devDependency</code>?
	</summary>
	<p>
		<code>devDependencies</code>, tj. development dependencies, obsahují všechno, co potřebujete
		pouze při vývoji, ne	do produkce/při nasazení (deploy) svojí stránky. Cokoli je tak označené, to např. Vite může při zpracování vašeho
		kódu přeskočit. TypeScript sem patří proto, že aby mohl běžet v JavaScriptovém prostředí (třeba prohlížeč), musí být
		zkompilovaný (přepsaný) do JavaScriptu. Vy jste se s tím nesetkaly, protože za vás kompilaci na pozadí řeší React
		při každém <code>npm start</code> nebo <code>npm build</code>.</p>
</details>

<details>
	<summary>
		Lze vytvořit nový typ ze dvou již existujících typů?
	</summary>
	<p>
	</p>
	<pre><code class="codeblock">
interface NewType extends OldType {
newTypeProperty1: string;
newTypeProperty2: string;
}</code></pre>

nebo

	<pre><code class="codeblock">
type NewType &amp; OldType = {
newTypeProperty1: string;
newTypeProperty2: string;
}</code></pre>
</details>

<details>
	<summary>
		Můžeme TypeScriptu "lhát" a zpětně ho přesvědčit, že je nějaké proměnná jiného typu než si myslí?
	</summary>
	<p>Bohužel můžeme. Stačí za proměnnou přidat <code>as NewType</code>. Ideálně bychom to dělat neměli, protože pak
		ztrácí TypeScript smysl, ale může se stát, že si potřebujeme jen něco otestovat a tohle nám může pomoct. Kde se nám
		ještě může hodit je pokud od nepořádného kolegy dostaneme nějaké ošklivé <code>any</code>, ale my víme, že to je
		string a potřebujeme zjistit jeho délku, <code>as string</code> by nám pomohlo (a pak šup to <code>any</code>
		opravit!).</p>
		::fig{src=assets/as-any.png size=70}
</details>
</div>