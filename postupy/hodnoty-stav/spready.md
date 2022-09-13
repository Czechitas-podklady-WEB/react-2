## Spready

V praxi často narazíme na potřebu chovat se k polím a k objektům jako k immutable hodnotám. V JavaScriptu však většina operací na polích i objektech použitou hodnotu modifikuje. Vezměme třeba metodu `unshift`.

```js
> const x = [1, 2, 3];
> x.unshift(8)
> x
[8, 1, 2, 3]
```

Metoda `unshift` naše pole drze změnila. Říkáme, že pracuje takzvaně na místě. Co kdybychom však chtěli původní pole zachovat? V takovém případě nám pomůžou takzvané :em[spready]. Spread můžeme použít na libovolném místě mezi hranatými závorkami, když vytváříme nové pole. Obsah původního pole se pak jakoby "vyleje" na zadané místo. 

```js
> const x = [1, 2, 3];
> const y = [4, 5, 6];
> [8, ...x])
[8, 1, 2, 3]
> [8, ...x, ...y, 7])
[8, 1, 2, 3, 4, 5, 6, 7]
> [...x, 7, 8, ...y])
[1, 2, 3, 7, 8, 4, 5, 6]
> [...x])
[1, 2, 3]
```

Pomocí spreadů můžeme některé běžně používané operace udělat immutable.

**Přidání prvku na začátek**:

Na místě:

```js
> x.unshift(8)
[8, 1, 2, 3]
```

Immutable:

```js
> [8, ...x]
[8, 1, 2, 3]
```

**Přidání prvku na konec**:

Na místě:

```js
> x.push(8)
[1, 2, 3, 8]
```

Immutable:

```js
> [...x, 8]
[1, 2, 3, 8]
```

**Přidání prvku na zadanou pozici**:

Toto je malinko složitější.

```js
> x.splice(1, 0, 8)
[1, 8, 2, 3]
```

Immutable:

```js
> [...x.slice(0, 1), 8, ...x.slice(2)]
```

Spready objektů fungují podobně jako spready polí. 

```js
> const time = { hours: 5, mins: 21 }
> { ...time, secs: 35 }
{ hours: 5, mins: 21, secs: 35 }
```

Pozor však na to, že pokud objekty obsahují stejnou vlastno, použije se vždy až poslední hodnota.

```js
> const time = { hours: 5, mins: 21 }
> { ...time, hours: 10 }
{ hours: 10, mins: 21 }
> { hours: 10, ...time }
{ hours: 5, mins: 21 }
```

Pomocí objektových spreadů můžeme snadno nahradit různé objektové mutable operace za immutable. 

Například změna nebo přidání vlasnosti.

Na místě:

```js
> time.hours = 10
> time.secs = 35
> time
{ hours: 10, mins: 21, secs: 35 }
```

Immutable:

```js
> { ...time, hours: 10, secs: 35 }
{ hours: 10, mins: 21, secs: 35 }
```


