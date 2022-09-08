---
title: Nábytek XXXMuck
demand: 3
---

Vyrobte v Reactu jednoduchý e-shop pro nový nábytkový řetězec XXXMuck. Web bude sestávat ze dvou stránek: nabídka produktů a detail produktu.

1. Pomocí `create-czechitas-app` vytvořte základ webové aplikace. 
1. Prohlédněte si [design hlavní stránky](assets/homepage.png) obchodu. Nemusíte jej přesně dodržet, stačí jej brát jako inspiraci. Než začnete programovat, rozvrhněte si strukturu stránky do srozumitelně pojmenovaných komponent. Hlavní stránka nechť je celá obsažena v komponentě `HomePage`.
1. Prostudujte si výstup následujicícho [API endpointu](https://apps.kodim.cz/react-2/xxxmuck/products), který vrací seznam produktů ve formátu JSON.
1. Vytvořte jednotlivé komponenty a sestavte z nich výslednou stránku. Data pro jednotlivé produkty načtěte z API. 
1. Pomocí příkazu `npm install react-router-dom` nainstalujte React Router.
1. Přidejte do vašeho projektu routování. Komponenta `HomePage` bude mít cestu `/`. 
1. Vytvořte zatím prázdnou komponentu `ProductPage` u zapojte ji pod cestu `/product`.
1. Dotvořte komponentu `ProductPage` dle [dodaného designu](assets/productpage.png).
1. Zařiďte, že po kliknutí na produkt na hlavní stránce se zobrazí stránka `ProductPage`. Zatím nebudeme této stránce nijak předávat vybraný produkt. 
1. Na `ShippingPage` zobrazte vybraný produkt. K tomu je potřeba si předat `id` produktu v URL stránky a použít hook `useParams`. Jednotlivé produkty pod jejich `id` najdete na [tomto endpointu](https://apps.kodim.cz/react-2/xxxmuck/products/2c6VoCaD).