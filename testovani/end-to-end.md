## End-to-end testy

Nástroje pro end-to-end testování nám umožňují testovat aplikaci přesně tak, jako by ji používal reálný uživatel. Dělají to tak, že nastartují opravdový prohlížeč, otevřou v něm požadovanou stránku, na které klikají, vyplňují formuláře, apod. Nakonec zjistí, zda se celá aplikace chová správně bez nečekaných překvapení - od back-endu až po front-end, včetně databáze, API. Od začátku do konce, neboli end-to-end.

Jen pro úplnost, pokud byste na to někde narazili, end-to-end testy se někdy označují také jako e2e testy.

Nástrojů pro end-to-end testování opět existuje celá spousta. Z těch nejznámějších je to třeba Cypress nebo aktuálně si velkou popularitu získává Playwright, takže si vše vyzkoušíme právě s ním.

## Playwright

Stejně jako předtím Vitest, i [Playwright](https://playwright.dev/) si musíme do našeho projektu nejprve nainstalovat:

```bash
npm init playwright@latest
```

Instalace se nás zeptá na několik otázek:
- Kam chceme umístit testy? → Nechme výchozí složku `test`.
- Přidat GitHubActions worksflow? → Prozatím vyberme **NE**. GitHub Action je téma na celou další lekci.
- Nainstalovat Playwright prohlížeče? → Vyberme **ANO**.

Playwright nám vytvořil v projektu 2 složky:
- `tests`, kam budeme dávat svoje skutečné testy
- `tests-example`, kde je vzorový soubor se spoustou jednoduchých i komplikovaných testů pro vzorovou aplikaci na webu Playwrightu, ze kterých můžeme čerpat znalosti.

Cokoliv budeme potřebovat, najdeme vždy v [dokumentaci Playwright](https://playwright.dev/docs/intro).

Uvidíte, že spoustu věcí budeme dělat stejně nebo velmi podobně jako v případě Vitestu.

### Náš první end-to-end test

Testy pro Playwright budeme psát do složky `tests` a soubory se opět budou jmenovat `*.test.ts` nebo `*.spec.ts`. Zoložíme si tedy například soubor `first.test.ts`.

Stejně jako u Vitestu si s Playwrightu naimportujeme `test` a `expect`. Metoda `describe` je v Playwrightu součástí objetu `test`
```ts
import { test, expect } from '@playwright/test'

// test suite (skupina testů)
test.describe('Home page', () => {

  // test
  test('something to test', async ({page}) => {

    // assertion
    await expect(page).toHaveTitle('Homepage')
  })

})
```

Všimněte si, že funkce, kterou předáváme metodě `test` jako druhý argument je asynchronní a jako parametr dostává objekt, že kterého si destrukturujeme `page`. Přes objekt `page` budeme přistupvat ke stránce zobrazené v prohlížeči, který si Playwright spustil na pozadí.

Protože v rámci end-to-end testů testujeme skutečnou stránku ve skutečném prohlížeči, musíme na ní nejprve navigovat, než nad ní budeme provádět jakékoliv testy.
```ts
test('something to test', async ({page}) => {
  // navigujeme na požadovanou stránku
  await page.goto('http://localhost:5173')

  // assertion
  await expect(page).toHaveTitle('Homepage')
})
```

### Spuštění testu

Samozřejmě to také znamená, že celý projekt musíme před spuštěním testů nejprve spustit přes lokální vývojový server:
```bash
npm run dev
```

Test spustíme pomocí:
```bash
npx playwright test
```

Příkaz si můžeme přidat jako *script* do `package.json` pro snadnější spouštění ve VS Code.

### Výsledky testu

Po proběhnutí testu si můžeme zobrazit report:
```bash
npx playwright show-report
```

### UI pro playwright

Nebo můžeme testy spustit s parametrem `--ui`, který nám spustí grafické rozhraní v prohlížeči, přes které můžeme testy spouštět.
```bash
npx playwright test --ui
```

Další možnost je nainstalovat si [rozšíření do VS Code](https://marketplace.visualstudio.com/items?itemName=ms-playwright.playwright) pro spouštění Playwright testů.


## Interakce se stránkou

Playwright obsahuje spoustu funkcí pro interakci se stránkou. Můžeme vybírat prvky podle jejich rolí, textu který obsahují, a spoustu dalšího. Playwright umí na prvky klikat, vyplňovat formuláře, apod.

### Vybírání prvků

Metoda `getByRole` objektu `page` vybere na stránce prvek podle jeho účelu. Například chceme zjistit, zda má stránka viditelný **nadpis** se správným textem:

```ts
test('something to test', async ({page}) => {
  // navigujeme na požadovanou stránku
  await page.goto('http://localhost:5173')

  // assertion
  await expect(
    page.getByRole('heading', {
      name: 'Home page'
    })
  ).toBeVisible()
})
```

Nebo chceme zjistit, že je na stránce odkaz obsahující určitý text:
```ts
await expect(
  page.getByRole('link', {
    name: 'Odkaz'
  })
).toBeVisible()
```

Podobné metodě `getByRole` jsou další metody pro vybírání prvků na stránce:
- `getByText`
- `getByTitle` nebo `getByAltText`
- `getByLabel` a `getByPlaceholder` pro formuláře

Více v [dokumentaci pro lokátory](https://playwright.dev/docs/locators).

### getByTestId

Trochu jinak funguje metoda `getByTestId`, která vyžaduje, aby měl prvek na sobě data atribut `data-testid="whatever"`.

Tato metoda by se měla používat hlavně v případě, že nemůžeme prvek najít podle jeho role nebo textu. Můžeme tak například otestovat, že je danný prvek prázdný:

```ts
test('shoping list is empty', async ({page}) => {
  await expect(page.getByTestId('shopping-list')).toBeEmpty()
})
```

### Interakce s prvky (klikání, apod.)

Napišme si další test, který otestuje, zda se po kliknutí na odkaz dostaneme na správnou stránku:

```ts
test('should redirect on click', async ({page}) => {
  await page.goto('http://localhost:5173')
  await page.getByRole('link', { name: 'Odkaz' }).click()

  // assertion
  await expect(page).toHaveTitle('Cilova stranka')
})
```

Další možnosti jako např. vyplňování formulářových polí najdeme v [dokumentaci pro akce](https://playwright.dev/docs/input).


## beforeEach - spouští se před každým testem

Pokud v rámci skupiny testů v každém testu vždy provádíme tu stejnou akci, např. jdeme na jednu konkrétní stránku, můžeme si vše zjednodušit použitím metody `beforeEach`, které naš funkcí spustí před každým testem:

```ts
test.beforeEach(async ({page}) => {
  await page.goto('http://localhost:5173')
})
```


