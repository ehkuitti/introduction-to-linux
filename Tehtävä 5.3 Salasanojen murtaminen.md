A)

1. Aluksi luomme halutut käyttäjät terminaalilla: 

![Adduser](https://user-images.githubusercontent.com/72074501/119223306-4613db80-bb01-11eb-973a-154a8c696380.PNG)

2. Avaamme Johnnyn root-oikeuksilla (terminaaliin sudo johnny ja salasana). Avaamme ohjevideon mukaisesti salasanatiedoston /etc/shadow. Tiedostosta löytyvät juuri luodut
käyttäjät sekä niiden hashit:

![Johnny](https://user-images.githubusercontent.com/72074501/119229397-92badf00-bb20-11eb-9061-9be40467f11e.PNG)

Siellähän ne näkyvät. Taulukosta myös selviää, että formaatti on crypt. Siispä meidän pitää mennä Optionssiin ja vaihtaa sieltä Current  hash formattiin myös crypt:

![Options](https://user-images.githubusercontent.com/72074501/119229527-1aa0e900-bb21-11eb-9ca5-3775ec0d34bc.PNG)

Nyt voimme palata Passwordssiin. Tämän jälkeen klikkaamme luotujen käyttäjien rivien kohdalta hash-saraketta hiiren oikealla näppäimellä ja valitsemme vaihtoehdon Include in attack. Tämän jälkeen painamme ohjelman yläosasta Start new attack, jolloin salasanojen murtaminen alkaa. 

![Johnny](https://user-images.githubusercontent.com/72074501/119229562-4c19b480-bb21-11eb-80aa-09f35b36e5c5.PNG)
Kuva: Attack käynnissä. 

Virtuaalikoneeni (itse asennettu levykuvasta, annettu AMD FX-8350 prosessorilta 4 ydintä ja 6 gigaa ramia, SSD) sai heikon salasanan murrettua alle todella nopeasti, alle minuutissa. Keskitason salasanan, jossa oli iso alkukirjain ja yhteensä 4 kirjainta se ratkaisi noin puolessa tunnissa. Vahvaa salasanaa en saanut edes murrettua samassa illassa. Olen hieman yllättynyt, kuinka paljon turvallisemmaksi kirjainten kirjainkoon muuttelu sekä erikoismerkkien lisääminen salasanasta tekee. Vaikken siis päässytkään toivottuun 3/3 lopputulokseen, opin myös samalla paljon tärkeää tietoa salasanaturvallisuudesta.

![Vahva](https://user-images.githubusercontent.com/72074501/119232935-8a1dd500-bb2f-11eb-9866-5612883c520e.PNG)

B) 

1. Kopioimme Canvasista pyydetyn hashin CrackStationiin, laitamme rastin ruutuun "en ole robotti" ja lopulta aloitamme murron. Menee noin 5 sekuntia ja saamme jo tulokset:

![CrackStationi](https://user-images.githubusercontent.com/72074501/119230135-92701300-bb23-11eb-82c4-d3f50eacb555.PNG)

2. Aivan aluksi asennamme Geditin komennolla _sudo apt install gedit_. Tämä siksi, että tarvitsemme tekstieditorin, johon kopioida Canvasissa annetut MD5-hashit. Kun tämä on tehty, avaamme Geditin kirjoittamalla terminaaliin komennon _gedit_. Tämän jälkeen hashit liitetään tiedostoon. Tallennamme tiedoston työpöydälle nimellä testmd5.txt...

![Gedit](https://user-images.githubusercontent.com/72074501/119233344-37451d00-bb31-11eb-89a9-e244b576162d.PNG)

... ja suljemme geditin. 

Olen tallentanut kaiken tarvittavan eetu-käyttäjäni työpöydälle. Seuraavaksi avataan terminal. Käytämme John The Ripper ohjelmaa salasanan murtamiseen, joten ajamme seuraavan komennon: 

sudo john -w=/home/eetu/Desktop/finnish-unknown.txt --format=raw-md5 "/home/eetu/Desktop/testmd5.txt"

, jossa

- sudo tarkoittaa root-oikeuksia
- john viittaa itse ohjelmaan
- -w valitsimella paikannamme sanalistan
- --format=raw-md5:llä kerromme, että sen formaatti on md5
- testmd5.txt on tiedosto, työpöydällä

Kuluu alle minuutti ja ohjelma on valmis. Saamme seuraavat tulokset: 

![Joni](https://user-images.githubusercontent.com/72074501/119233595-893a7280-bb32-11eb-8cc3-1480c9f98fc7.PNG)
