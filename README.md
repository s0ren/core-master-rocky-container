# Linux Server 16xxx faget med containere

Et eksperiment for hvor meget man kan med docker containere, og stadig hodle sig rimeligt tæt på Bendt Mollerups (og Willys) Linux undervisningsmateriale.

## Baggrund

I omtalte materiale op bygges en række linux maskiner, nogen til terminal øvelser, nogen som desktop maskiner, igen andre til som servere. 
I materialet køres maskinerne som virtuelle maskiner i _vmware_.
Man kunne udemærket opbygge og afvikle det hele i en anden hypervizor. F.eks. VirtualBox eller HyberV. Nu beskriver materialet hvordan man gør med vmware, så det er det letteste.

Alligevel, tænker jeg på andre muligheder. Faget afvikles også med elever der har valgt specialet Programmering. Disse frustreres over at tænkegangen er at maskinerne har en tilstand, som forandres og forædles, gennem et utal af kommandoer, og redigering af mange configurations filer. På et tidspunkt har man lavet de rigtige ting, og så virker det.

Dette er kontra intutivt for mange programmører. Vi vil have et fixture. Projektet starter med at være rent, og urørt. Når jeg har compileret programfilerne, kan jeg udføre en bestemt funktion, og svaret vil altid være det samme. Afhængigt af om jeg har skrevet koden rigtigt, er resultatet som forventet, eller ikke.  
Hvis der er fejl, og resultet ikke er det forventede, kan man ændre noget i programteksten, _rebuilde_ projektet, og se projektet nu opfører sig som forventet.

Ved system configuration, kan det være svært at følge kæden baglæns og prøver forfra. Man kan naturligvis begynde _helt_ forfra, men det er tidskrævende og demotiverende.

Derfor vil jeg gerne have en femgangsmåde og metodik og miljø, der minder mere om et programmeringsprojekt, og lidt mindre om serverkonfigurering.

Flere af maskinerne kunne godt implementeres som containere, frem for almindlige virtuelle (eller fysiske) maskiner. 
En _Docker container_ er i princippet tilstandsløs, og smider alt sin persistense når den lukker eller genstarter. Det som _skal_ gemmes placeres i fil er i volumes, som er en slags _file share_ som er mapper der deles mellem containeren og værts-systemt. Dette giver også mulighed for at man kan bruge en mere komfortabel editor end _vi_. 

Endvidere kan man bruge versionstyringsværktøjer til at gemme, distribuere, forgrene og genbruge. Her `git` og _GitHUb_.

# Konkret 

Dette projekt tænkes som et af flere, der implementerer stadier i nævnte kompendier. 

Dette tænkes som Core Master, og tager sin første pause ved s. xx.
næste stadie, er hvor vmware maskinen, var klar til at blive klonet. Her laver jeg en ny branch, frem for at klone en maskine. Docker sørger selve maskinerne.  
Processen her afføder nogen docker images, som også kan organiseret med henblik på distrubution, men elevern skal jo have lov at lave noget af arbejdet...

Jeg laver separate _MarkDown_ filer og nogen shellscript filer for at følge flowet i kompendierne. Disse organisres i mapper under standard-brugeren, `tec`s, hjemmemappe. Se `/home/tec/exercises`

I denne branch forsøger jeg med at lægge alle linux konfiragtioner i flere commits (og branches), så alle filerne _er_ der når man checker den rigtige bransh ud.

Se [Motivation.md](Motivation.md) og [conf-in-commits-playbook.md](conf-in-commits-playbook.md).