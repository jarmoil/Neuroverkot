cifar10CNN avg 40 sek per epoch
cifar10FCN avg 4 sek per epoch

GPU:lla
cifar10cnn avg 7 sek per epoch after first one
cifar10fcn avg 1 sek per epoch

# CIFAR-10 kuvaluokittelu neuroverkoilla

## Projektin tavoite
Projektin tavoitteena oli soveltaa neuroverkkotekniikoita CIFAR-10-kuvaluokitteluun sekä vertailla kahden eri arkkitehtuurin suorituskykyä:
- Täysin yhdistetty neuroverkko (Fully Connected Network, FCN)
- Konvoluutioneuroverkko (Convolutional Neural Network, CNN)

Tavoitteena oli analysoida mallien tarkkuutta, oppimista ja tehokkuutta sekä ymmärtää, miksi CNN soveltuu paremmin kuvadataan.

## Toteutus

### Data
Käytettiin CIFAR-10-datasettiä, joka sisältää 60 000 värikuvaa (32x32 pikseliä, 3 värikanavaa) ja 10 eri luokkaa.

### FCN-malli
FCN-mallissa kuvat litistettiin (flatten), jolloin spatiaalinen informaatio menetettiin.

Rakenne:
- Flatten
- Dense-kerroksia (ReLU)
- Output-kerros (softmax)

Ominaisuudet:
- Suuri määrä parametreja
- Ei hyödynnä kuvien rakennetta

### CNN-malli
CNN hyödyntää konvoluutiokerroksia, jotka tunnistavat paikallisia piirteitä (reunat, muodot).

Rakenne:
- Conv2D + ReLU
- MaxPooling
- Useita konvoluutiolohkoja
- Flatten + Dense
- Softmax output

Lisäksi käytettiin:
- Dropout (ylisovittamisen vähentämiseen)
- Batch Normalization

## Tulokset

| Malli | Testitarkkuus | Parametrien määrä | Opetusaika |
|------|--------------|------------------|------------|
| FCN  | ~50 %        | Suuri            | Nopea      |
| CNN  | ~83 %        | Kohtalainen      | Hitaampi   |

Ilman GPU:ta:
- FCN keskimäärin 4 sekuntia per epoch
- CNN keskimäärin 40 sekuntia per epoch

GPU:lla:
- FCN keskimäärin 1 sekuntia per epoch
- CNN keskimäärin 7 sekuntia ensimmäisen jälkeen (26 sek)

Tietyn epochien määrän jälkeen, testitarkkuus ei nouse kauheasti, mutta opetusaika nousee, jonka takia piti kokeilla eri epochien määrä kunnes löytyi sopiva väli jolloin opetusaika ei ole liian pitkä, mutta tarkkuus oli hyvä.
Vaikka kuinka paljon yrittää niin FCN mallilla ei mene kauheammin yli 50 % testitarkkuus. CNN on suorastaan parempi malli tällaiseen tehtävään.

## Oppimiskäyrät

- FCN: validation loss alkoi kasvaa, jonka takia ylisovittaminen
- CNN: tasaisempi oppiminen ja parempi yleistyminen

## Visualisoinnit

Projektissa tarkasteltiin:
- Esimerkkikuvia ja ennusteita
- Todennäköisyysjakaumia (softmax output)
- Väärin luokiteltuja kuvia

Havainto:
- CNN teki vähemmän virheitä ja oli varmempi ennusteissaan
- FCN sekoitti helposti samankaltaisia luokkia (esim. kissa vs. koira)

## Analyysi

### Miksi CNN toimii paremmin?
CNN suoriutuu paremmin, koska:
- Säilyttää kuvien spatiaalisen rakenteen
- Tunnistaa paikallisia piirteitä (reunat, tekstuurit)
- Käyttää vähemmän parametreja suhteessa tehokkuuteen

FCN puolestaan:
- Litistää kuvan, jonka takia menetetään rakenne
- Vaatii enemmän dataa oppiakseen tehokkaasti

### Väärin luokitellut kuvat
Virheitä tapahtui erityisesti:
- Epäselvissä kuvissa
- Luokissa, joilla on visuaalisia yhtäläisyyksiä

## Kokeilut ja parannukset

Projektissa kokeiltiin:
- Dropout, joka vähensi ylisovittamista
- Eri kerrosmääriä
- Mahdollisesti data augmentationia

## Johtopäätökset

- CNN oli selvästi parempi CIFAR-10 datan käsittelyyn
- FCN soveltuu huonommin kuvadatalle
- Mallin arkkitehtuuri vaikuttaa merkittävästi suorituskykyyn

Projektin tulokset vastasivat odotuksia:
- FCN: ~50–55 %
- CNN: ~75–85 %

## Tekoälyn käyttö

Tekoälyä käytettiin:
- Rakenteen suunnitteluun sekä mahdollisesti tiedon etsimiseen ja asioiden ymmärtämiseen.
- Raportin kirjoittamisen tukena.

Kaikki ratkaisut ymmärrettiin ja sovellettiin itse.