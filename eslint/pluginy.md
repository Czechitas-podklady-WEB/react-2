## ESLint pluginy

Pro některé projekty nám pravidla obsažená přímo v ESLintu nestačí. Pokud například pracujeme v Reactu, budeme chtít pravidla pro správné psaní React komponent. Kdybychom chtěli používat TypeScript, budeme potřebovat speciální pravidla pro formátování kódu v TypeScriptu.

K rozšiřování pravidel a funkcí ESLintu slouží pluginy. Jde o velmi podobný koncept jako pluginy ve Webpacku.

Pro naše účely se hodí následující pluginy

- [eslint-plugin-import](https://www.npmjs.com/package/eslint-plugin-import): tento plugin kontroluje cesty a názvy souborů při importech, aby nás upozornil na špatné importované soubory,
- [eslint-plugin-react](https://www.npmjs.com/package/eslint-plugin-react): základní pravidla pro kontrolu kódu v Reactu,
- [eslint-plugin-react-hooks](https://www.npmjs.com/package/eslint-plugin-react-hooks): vynucuje pravidla pro React hooky,
- [eslint-plugin-jsx-a11y](https://www.npmjs.com/package/eslint-plugin-jsx-a11y): kontroluje JSX v Reactu, a hledá prohřešky proti přístupnosti.

Pluginy nainstalujeme klasickým příkazem

```
npm install -D eslint-plugin-import eslint-plugin-react eslint-plugin-react-hooks eslint-plugin-jsx-a11y
```

Díky zmíněným pluginům můžeme vyrobit ESLint konfiguraci pro moderní Reactový projekt:

```
module.exports = {
  env: {
    browser: true,
    es2021: true,
  },
  extends: [
    'plugin:react/recommended',
    'airbnb',
  ],
  parserOptions: {
    sourceType: 'module',
  },
  plugins: [
    'react',
  ],
  rules: {},
};
```

Toto je už hodně instalování a nastavování. Nástroj `create-czechitas-app` má proto speciální generátor zvaný `react-eslint`, který vytváří Reactový projekt s už nakonfigurovaným ESLintem. Pro vytvoření nového projektu tak stačí napsat

```
npx create-czechitas-app myapp react-eslint
```
