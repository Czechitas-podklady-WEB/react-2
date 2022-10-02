## Časovače

K problémum se zastaralými hodnotami v React dochází vždy, když funkce vytvořené v těle komponenty pužíváme mimo JSX. V takovím případě nemá React nad našimi funckemi kontrolu a nemůže vyměňovat staré funkce za nové. To nastává v případě

1. událostí, které obsluhujeme mimo React jako `document/keyUp`, `window/offline` apod.,
1. časovačů jako `setTimeout` a `setInterval`. 

U časovačů je situace jiná, než u událostí, protože za běhu časovače není už možné vyměnit funkci, kterou časovač vykonává. Postup s ruční výměnou funkce nám je tady k ničemu.  
