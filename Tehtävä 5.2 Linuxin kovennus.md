A) 

Asensin Kali Linuxin itse alusta levykuvalla virtuaalikoneeseen, sillä sain tämän johdosta merkittävästi parempaa suorituskykyä. Tämän takia komentorivissä lukee eetu@kali, mutta
Kali on muuten täysin sama. Kaikki käyttämämme komennot vaativat root-tason oikeuksia, sillä teemme merkittäviä muutoksia itse järjestelmään.

1. Aivan aluksi asennamme UFW-palomuurin kirjoittamalla:
 
![Kali install ufw](https://user-images.githubusercontent.com/72074501/119134972-7fd3dc00-ba46-11eb-90ec-a3ee7dce1e7f.PNG)

UFW latautuu ja asentuu. Asennuksen aikana UFW:lle luodaan automaattisesti muutama konfiguraatiotiodosto, joita UFW hyödyntää erilaisten tietojen käsittelyssä.

Tämän jälkeen asennamme vielä GUWF:n, joka on UFW:n GUI:lla (graafinen käyttöliittymä) varustettu versio:

![Kali install gufw](https://user-images.githubusercontent.com/72074501/119135320-ebb64480-ba46-11eb-9393-7eb58277a575.PNG)

Nyt kun kaikki on asennettu, voimme käynnistää palomuurin komentoriviltä seuraavan komennon avulla: 

![Kali enable ufw](https://user-images.githubusercontent.com/72074501/119135495-2c15c280-ba47-11eb-90c3-530b81be067d.PNG)

2. Seuraavaksi selvitämme, mitä sääntöjä palomuurissa on käytössä oletuksena. Tämä tapahtuu seuraavasti:

![Kali ufw status](https://user-images.githubusercontent.com/72074501/119135906-ad6d5500-ba47-11eb-8335-a68164214691.PNG)

Koska status tulostaa vain sanan active eikä muuta, tarkoittaa tämä sitä, että oletuksena palomuurissa ei ole mitään sääntöjä tehtynä. 

3. Nyt lisäämme palomuurin säänöt, jotka sallivat http- ja https-yhteydet:

![Kali ufw allow](https://user-images.githubusercontent.com/72074501/119136268-210f6200-ba48-11eb-91e3-443aca604e44.PNG)

4. Seuraavaksi haluamme estää FTP-yhteydet sillä rajoituksella, että se koskee vain saapuvia yhteyksiä. Tämä on helppoa tehdä gufwissa. Avaamme gufwin kirjoittamalla terminaaliin gufw. Järjestelmä tunnistaa komennon vaativan root-tason oikeuksia, joten esiin ponnahtaa graafinen ikkuna, jossa tähtä ilmoitetaan erikseen. Annamme salasanan ja painamme enteriä, jolloin järjestelmä sallii meidän avata gufwin. 

![Gufw](https://user-images.githubusercontent.com/72074501/119157758-2d061e80-ba5e-11eb-9cb0-9e04b0722227.PNG)

Kun ohjelma on avattu, klikkaamme välilehteä Rules (säännöt) ja sitten alareunasta plussaa (+). 

![Rulez](https://user-images.githubusercontent.com/72074501/119158652-1dd3a080-ba5f-11eb-937d-745318a5cbc6.PNG)

Ikkuna aukeaa ja löydämme itsemme Preconfigured-välilehden alta. Tämä on hyvä. Sitten valitsemme Policyksi (käytäntö) Deny eli estä. Tämän jälkeen valitsemme suunnaksi (direction) In ja kategoriaksi network, alakategoriaan (subcategory) ei tarvitse koskea. Tämän jälkeen kun selaamme Sovelluslistaa (application) voimme löytää sieltä FTP:n. Lopuksi klikkaamme alhaalta add. 

![Add rule](https://user-images.githubusercontent.com/72074501/119158497-f086f280-ba5e-11eb-8e93-b3da85902979.PNG)

Kun nyt suljemme lisäysikkunan, voimme huomata, että FTP on ilmestynyt listalle. 

![Rulesi](https://user-images.githubusercontent.com/72074501/119158816-4a87b800-ba5f-11eb-92da-70bb7597a71c.PNG)

5. Ulospäin lähtevän liikenteen kieltäminen gufw:lle on myös todella helppoa. Rulesista painamme taas alhaalta plussaa. Nyt kuitenkin valitsemme Preconfiguredin (esimääritetty) sijaan yksinkertaisen menettelytavan (simple). 

![Simple](https://user-images.githubusercontent.com/72074501/119159877-60e24380-ba60-11eb-8366-c4244fd963e2.PNG)

Nyt tarvitaan jotain nimeä. Laitan nimeksi "Estä portti 25 lähtevä", sillä se selittää suoraan mitä se tekee. Sitten laitan vielä käytänteeksi (policy) kiellon (deny) ja suunnaksi out. Protokollaan ei tarvitse koskea, vaan se voidaan jättää oletukseen Both (= koskee sekä UDP:tä että TCP:tä). Lopuksi kirjoitamme portin riville ihan vain luvun 25 ja painamme Add. Mikäli kaikki menee hyvin, tämäkin sääntö ilmestyy sääntölistaan...

![Säännöt](https://user-images.githubusercontent.com/72074501/119160126-9c7d0d80-ba60-11eb-845f-f0d072f76b50.PNG)

... ja siellähän se on! 

6. Seuraavaksi luvassa on hieman monimutkaisempi osuus, sillä IP-osoitteen kieltäminen vaatii nimittäin erityismäärityksiä. Painamme taas plussaa lisätäksemme uuden säännön. Tällä kertaa joudumme valitsemaan vaihtoehdon Advanced (edistynyt), koska se on ainoa, joka sallii säännön koskevan tarkkaan tiettyä IP:tä. Menemme nyt siis edistyneiden käyttäjien puolelle ja löydämme sieltä hieman enemmän asetuksia: 

![Edistynyt](https://user-images.githubusercontent.com/72074501/119160745-3d6bc880-ba61-11eb-8472-0a7a104eb240.PNG)

Nyt onkin valittava hieman enemmän asetuksia. Annetaan nimeksi alkuun looginen "Estä 15.15.15.51 kokonaan". Tämän jälkeen muutamme asetukset seuraavanlaisiksi:

- Policy: Deny
- Direction: Both
- Inferace: All interfaces //Tämä tarkoittaa sitä, että asetus koskee kaikkia tietokoneen verkkoonyhdistämistapoja eli samat säännöt koskevat esim. ethernettiä ja WiFiä. 
- Log: Do not log // Jos haluaisimme, voisimme pitää lokia yhteysyrityksistä tähän porttiin. Päätän jättää ne päälle. 
- Protocol: Both // Koskee TCP:tä ja UDP:tä. 
- From: Tähän tulee haluttu osoite 15.15.15.51 eli estämme saapuvat yhteydet sieltä. 
- To: Tähän tulee myös 15.15.15.51 eli estämme samalla säännöllä myös sinne lähtevät yhteydet. 

Nyt voimme painaa Add alhaalta. 

![Add](https://user-images.githubusercontent.com/72074501/119164450-1e6f3580-ba65-11eb-9a6b-7800f5b91353.PNG)

Ja tämäkin ilmestyy listalle.

![Listanen](https://user-images.githubusercontent.com/72074501/119164790-70b05680-ba65-11eb-8e3e-419c2874f570.PNG)

B)

Aivan aluksi asennamme ClamAV:n seuraavasti: 

![clamav](https://user-images.githubusercontent.com/72074501/119165380-19f74c80-ba66-11eb-89c0-f5ce8d809f08.PNG)

Nyt ClamAV on valmiina käytettäväksi. Paketista löytyy clamscan toiminto, jota voi ajaa komentorivillä seuraavasti: 

![clam](https://user-images.githubusercontent.com/72074501/119166037-d51fe580-ba66-11eb-9bd1-5d5355bb390a.PNG)

sudo tarkoittaa taas root-oikeuksia eli annamme ohjelmalle täydet oikeudet toimia järjestelmässä. Tämän jälkeen kirjoitamme clamscan, mikä on ohjelman mukana tuleva scannauskomento. Käytämme valitsinta -r listaamaan scannatut tiedostot ja asetamme kohteeksi tiedostojärjestelmän juuren "/". Enterillä ja salasanan annolla scannaus alkaa. 

![One eternity later](https://user-images.githubusercontent.com/72074501/119166402-3e075d80-ba67-11eb-9b8b-9c5ff7bb5a19.jpg)

Scannauksessa meni pitkään, sillä se kävi läpi koko tiedostojärjestelmän. Nyt kuitenkin se on valmis ja tullut lopputulokseen: ei viruksia. 
