## Imutabilita

Klíčem k pochopení podivností z předchozí sekce je fakt, že hodnoty v JavaScriptu se dělit do dvou kategorií podle toho, jestli jde už jednou vytvořená hodnota změnit nebo ne.

Pokud například vytvoříme nějaké pole, můžeme jej dále měnit: nahrazovat prvky za jiné, přidávat prvky apod. 

```js
> const x = [1, 2, 3]
> x.push(8)
> x[0] = 5
> x
[5, 2, 3]
> x.push(8)
> x
[5, 2, 3, 8]
```

Vidíme, že pole uložené v proměnné :var[x] se mění. Podobně můžeme zacházet i s objekty.

```js
> const time = { hours: 5, mins: 21 }
> time.hours = 8
> time
{ hours: 8, mins: 21 }
> time.secs = 35
> time
{ hours: 8, mins: 21, secs: 35 }
```

Zajímavé je, že s řetězci takové věci dělat nelze. Řetězce nenabízají žádnou metodu `push` a jí podobné. Jednou vytvořený řetězec zůstává navždy stejný. Pokud chceme k řetězcí přidat písmenko, musím použít operátor sčítání a vytvořit tak řetězec nový. 

```js
> const name = 'Petr'
> name + 'a'
'Petra'
> name
'Petr'
```

Vidíme, že proměnná :var[name] pořád obsahuje hodnotu `Petr`. 

Pokud nějaká hodnota nejde změnit, říkáme odborně, že je takzvaně :em[immutable]. Řetězce jsou vždy immutable a to jak v JavaScriptu tak ve většině ostatních jazyků. Naopak objekty a pole jsou :em[mutable]. 

Imutabilita má dalekosáhlé důsledky. Ty hlavní prozkoumáme ve zbytku této lekce.