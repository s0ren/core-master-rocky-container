# Deling af Linux system installinger med værtssystemet

Linux gemmer _alle_ sine systemindstillinger i konfigurationsfiler. Det fleste i tekstfiler under `/etc/`, nogle under `/var/.
Nogle filer ligger lige i `/etc/` andre i undermapper, under `/etc/`.  
Det er egentlig de enkelte applikationer der definerer sinde konfigurationsindstillinger, og dem som sammensætter distrubutionen, som i en eller anden form for kooperation, bestemmer hvad der konfigureres hvor. Derfor kan det virke mere eller mindre kaotisk. Oftes er der nogen tanker bag. Der er naturligvis også en masse bagudkompatabilitet som har betydning, så det er ikke _bare lige_ at ændre på placeringen af filerne.

Det er klart lettest at overskue hvis hele `/etc/` og `/var/` "bindes" til mappen med containder filerne, som også er den mappe man åbner i __vs code__.  
I _docker_ hedder dette et bind-volume. Hvis man starter docker containeren direkte, ser det sådan her ud:
    
    docker run -v etc:/etc ...

Der er _bare_ det problem at de "bundne" mapper er tomme på værts-siden, og det der ligger i den (eller ikke gør) overskygger for det der en gang var, i mapperne på container siden. Så alle instillingene er væk? Og linux duer ikke! :-( 

Efter en del research har jeg fundet følgende:
* Et bind volume er det altid værtens filer der overskygger
* i et navngivet volume kan docker godt populere filerne (kopiere) ind i volumet, men dette kan ikke bindes til en mappe på værten.
* filerne kan kopires fra containeren til værten med `docker cp <vært>:/etc/ ./etc`
  * Dette behøver kun at gøres lige efter build af container. Ikke efter start.
* jeg kan ikke lige se hvordan jeg får det ind i vscode-devcontainers lifecycle scripts...

Muligheder og umuligheder
* Kan man lave et multistage build med en `Dockerfile`, hvor filerne kopieres mellem stadierne?
* Kan man lave et "hook" i `devconcainer/devcontainer.json` hvor det sker 'automatisk'
* Kan jeg lave trin af commits i git hvor jeg gemmer de tilstande der rummer det initielle build, de kopierede filer, og containeren med bind-volume?
