# Konfigurationes filer i commits

I denne branch forsøger jeg med at sørge for at filerne i `./etc/` og `./var/` er populeret (kopieret ind i) inden bind-volume'et åbnes.

Se [Motivation.md](Motivation.md) og [README.md](README.md).

Problemet er at når jeg laver et bind-volume overskygges indholdet på containeren af hvad der er i mappen på værts maskinen.  
men det hele ligger jo omrindeligt i den linux vi har installeret i containeren, men ikke på værtsmaskinen (som kan være windows).

Vi kan ikke lige kopiere det når containeren er startet, for da kan linux ikke fungere uden sine indstillinger.

Men hvis vi laver containeren først, kopierer indholdet af contanerens `/etc/`(og `/var/`) over til projektets mappe på værtsmaskinen, og derefter starter containeren, _med_ bind-volumet, så kører det hele måske:

* docker build ...
* docker copy ...
* docker run ...

jeg prøver

    docker build -t core-master-rocky .devcontainer/

i shell

    rm -f image_id container_id 
    docker build --iidfile image_id -t core-master-rocky .devcontainer/
    image_id=$(cut -c 8-19 image_id)

    docker create --cidfile container_id $image_id

    container_id=$(cat container_id)
    docker cp $container_id:/etc ./etc
    docker cp $container_id:/var ./var
