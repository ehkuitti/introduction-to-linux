a)

1. 

a) export PS1="\u\A "
b) export PS1="\h\s\v "
c) export PS1="\[\e[31m\]Hei \u, mitä tehdään tänään =]?\[\e[m\] "

2. 

a) alias backup="zip -r backup.zip /home/eetu"
b) alias poista="rm -i Tiedosto1.txt"
c) alias juureen="cd /"
d) alias päivitä="sudo apt update"
e) alias täyspäivitys="sudo apt update -y && sudo apt upgrade -y && sudo apt autoremove -y && sudo apt autoclean -y"

b) 

Koodit tallennetaan .sh-päätteiseen tiedostoon ja ajetaan terminalilla kirjoittamalla chmod 777 esimerkki.sh ja sitten ./esimerkki.sh (olettaen, että tiedosto on samassa kansiossa kuin mitä terminalilla ollaan tarkastelemassa). 

a) #!/bin/bash

echo Heippa! Kerro nimesi

read varname

echo Kerro vielä ikäsi. 

read varage

if [[ $varage -gt "50" ]]
	then
		echo Terve $varname , olet yli 50v!
else
	echo Olet nuorempi kuin 50v!
	
fi

b) #!/bin/bash

echo Hei! Anna käyttäjätunnus

read varname

echo Anna salasana 

read varpw

if [[ $varname == "opiskelija" && $varpw == "demo" ]]
	then
		echo Oikein, tervetuloa!
else
	echo Syötit väärän tunnuksen tai salasanan.
	
fi

c) 

#!/bin/bash

echo Suoritetaanko ylläpitotoimet? Kirjoita y jos kyllä ja n jos ei

read varans

if [[ $varans == "y" ]]
	then
		sudo apt update && sudo apt upgrade && sudo apt autoremove -y && sudo apt autoclean -y && sudo updatedb && tar -czvf archive.tar.gz /home/eetu && cd /home/eetu && mkdir backups && cp archive.tar.gz /home/eetu/backups && echo Valmista tuli!
else
	echo Ylläpitotoimia ei suoritettu.
	
fi

d) #!/bin/bash

echo Tervetuloa arvauspeliin! Yritä arvata oikea numero kirjoittamalla jokin numero!

read varnum

n=7

if [[ $varnum == "$n" ]]
	then
		echo Numerosi meni oikein, onnittelut!
elif [[ $varnum -gt "7" ]]
	then 
		echo Numerosi on liian suuri!
else
		echo Numerosi on liian pieni!
		
fi
