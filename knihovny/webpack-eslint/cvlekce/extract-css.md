---
title: Extrakce stylů
demand: 3
---

Pokud pro zapojení CSS stylů do stránky používáme *style-loader*, tento vloží styly do stránky pomocí prvků `<style></style>`. To se nám v mnoha případech nemusí hodit a chceme, aby Webpack vyrobil klasický soubor `style.css` a nalinkoval ho do naší stránky. K tomu je potřeba místo *style-loaderu* použít *MiniCssExtractPlugin*. 

1. Udělejte si fork [repozitáře](https://github.com/Czechitas-podklady-WEB/extract-css) s jednoduchou stránkou, která používá Webpack a *style-loader*.
1. Nainstalujte závislosti pomocí `npm instal` a spusťte projekt pomocí `npm run start`.
1. Podívejte se pomocí *dev-tools* kde jsou ve stránce vloženy styly.
1. Plugin *MiniCssExtractPlugin* má velmi srozumitelnou [dokumentaci](https://www.npmjs.com/package/mini-css-extract-plugin). Následujte ji a nakonfigurujte Webpack tak, aby generoval separátní soubor s CSS styly.
