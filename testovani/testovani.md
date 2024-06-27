## Testování kódu a aplikací

Při programování běžně dochází k chybám. Děláme je všichni a často. Jako profesionální vývojáři a vývojářky bychom si ale měli zakládat na tom, že do produkční verze aplikace doručíme kód pokud možno bez chyb.

Testování často působí jako ztráta času. Opravdu musíme po každé změně kódu znovu celou aplikaci proklikat a vyzkoušet, zda vše v pořádku funguje? Vždyť je přeci jasné, že jsme v kódu udělali jen malou změnu a ta nemohla způsobit nic strašného. No jasně... ostřílení vývojáři by mohli vyprávět.

Manuální testování má svoje místo. Je vždy fajn, když aplikace otestuje člověk - tester, který se chová jako běžný uživatel. Nás jako vývojáře však mnohem více zajímá automatizované testování. Napíšeme si vlastní testy, které jednoduše spustíme po každé změně v kódu, případně před každým commitem do repozitáře nebo před nasazením aplikace do testovacího nebo produkčního prostředí. Pokud testy v pořádku proběhnou, můžeme si být víceméně jistí, že naše změny v kódu nerozbily aplikace na nějakém nečekaném místě.

I u těchto automatických testů nás čeká podobné dilema - psaní a vymýšlení testů zabere nějaký čas a my se musíme rozhodnout, kolik času strávíme psaním testů a kolik vlastní iplementací nových funkcí aplikace.

Důležité je pochopit, ža naše aplikace bude otestovaná tak jako tak. Když to neuděláme my, otestují ji až naši uživatelé. A každá chyba, na kterou přijde koncový uživatel, způsobuje ztrátu důvěry v aplikaci, rozčílení, možnou ztrátu času a podobně. Tomu se chceme vyhnout.

Testování se vyplatí. Dává nám jistotu, že námi napsaný kód je v pořádku a že jsme opravením jedné chyby nezpůsobili chybu druhou.

## Druhy testování

Testování lze rozdělit do několika kategorií. Odborníci na testování by určitě měli kategorií víc, nám budou pro pochopení stačit tyto 3 základní:

- **Unit testy** testují pouze jednu samostatnou část našeho kódu (unit). Typicky jde o nějakou funkci nebo metodu. Unit test může zjistit, zda funkce např. vrací očekáváné hodnoty.
- **Integrační testy** ověří, zda náš kód správně komunikuje s okolním prostředím. To může být třeba databáze, API, souborový systém nebo i další moduly v rámci naší aplikace. Integrační testy jsou obvykle komplikovanější na přípravu a nastavení, protože obvykle se v rámci nich musíme postarat o přípravu testovacího prostředí, inicializaci růtných závislostí nebo třeba simulaci odpovědí z databáze nebo API.
- **End-to-end testy (E2E)** kontroluljí aplikaci z pohledu uživatele. Nějakým způsobem simulují chování uživatele (klikání, vyplňování hodnot) a ověřují, zda se aplikace následně chová, jak by měla. End-to-end testy se obvyle pokrývají kritické cesty v aplikaci (např. dokončení objednávky v e-shopu).

My si v následujích kapitolách ukážeme, jak si vytvořit unit testy a end-to-end testovací scénáře.
