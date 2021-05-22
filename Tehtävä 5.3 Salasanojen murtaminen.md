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

Aikaa kuluu noin viitisen minuuttia ja lopulta kaikki kolme salasanaa on onnistuttu murtamaan. 

B) 

1. Kopioimme Canvasista pyydetyn hashin CrackStationiin, laitamme rastin ruutuun "en ole robotti" ja lopulta aloitamme murron. Menee noin 5 sekuntia ja saamme jo tulokset:

![CrackStationi](https://user-images.githubusercontent.com/72074501/119230135-92701300-bb23-11eb-82c4-d3f50eacb555.PNG)

2. 
