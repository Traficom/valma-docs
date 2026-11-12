---
nav_order: 2
sort: 2
---

# Mallijärjestelmän käyttö

Tässä ohjeessa kerrotaan, mistä löydät materiaalit malliajoihin ja miten suoritat ajoja VALMA-käyttöliittymällä.

## Valmistelu

1. Lataa malliajon tiedot [Sharefilestä](https://traficom.sharefile.eu/home/shared) VALMA-lahtotiedot kansiosta.
   Pyydä pääsyoikeutta [Traficomilta](https://traficom.fi/fi/liikennejarjestelma/liikenteen-analyysit-ja-ennusteet/valtakunnallinen-liikennemallijarjestelma-valma).
   Tarkempia tietoja näistä löytyy [Lähtötietojen kuvauksesta](malliajon_lahtotiedot.md)
   - Baseline_data: lähtökysyntämatriisit (zip.) alueellisiin osamalliajoihin.
   - Cost_data: liikenteen hintadata, jossa on ennustevuoden hintataso.
     (Tähän tiedostoon käyttäjä voi myös lisätä yleisiä korotuskertoimia.)
   - Emme_network: tarkasteluvuotesi EMME-verkot.
   - Zone_data: aluetiedot, jossa on ennustevuoden henkilöliikenteen aluedata-aineisto.
   
2. Lähtökysyntämatriisit:
   - Alueellisten osamallien lähtökysyntämatriisien zip. -kansiot tulee purkaa.
     Sinun tulee myöhemmässä vaiheessa viitata kansioon, jossa on demand_matrices-niminen kansio.
     Luo siis kansio, joka sisältää demand_matrices-kansion. Pura lähtökysyntämatriisit demand_matrices-kansioon osamallikohtaisiin alikansioihin:
     ```
     <lähtödatan kansio>
     └── demand_matrices
         ├── business_and_overnight
         │   └── ext_foreign_passenger_vrk.omx
         ├── uusimaa
         │   ├── demand_aht.omx
         │   ├── demand_pt.omx
         │   ├── demand_iht.omx
         │   ├── demand_it.omx
         │   └── long_dist_demand_vrk.omx
         ├── lounais_suomi
         │   └── …
         └── …
     ```
     Osamallien kansioissa on vastaavan alueen matriisitiedostot, jotka ovat formaatissa .omx:
     - `demand_<ajanjakso>.omx`: osamallin lähtökysyntä ajanjaksoittain (aht, pt, iht ja it)
       sijoitteluluokittain (`icev`, `bev`, `phev`, `van`, `bike`, `transit`, `airplane`, `truck`, `semi_trailer`, `trailer_truck`).
       Iltatunnin (it) tiedosto sisältää vain joukkoliikenteen luokat.
       Matriiseja käytetään ensimmäisessä sijoitteluiteraatiossa sekä pelkän loppusijoittelun ajoissa.
     - `long_dist_demand_vrk.omx`: osamallin pitkien matkojen henkilöauto- ja joukkoliikennekysyntä vuorokaudessa.
       Käytetään, kun pitkien matkojen kysyntä otetaan projektin lähtödatasta.
   - Lähtökysyntä ei käytännössä vaikuta lopputuloksiin, mutta mitä lähempänä se on lopullista kysyntää, sitä nopeammin malli konvergoituu.
   - Matriisitiedostoista saa puuttua verkon sijoittelualueita (ne täytetään nollilla), mutta niissä ei saa olla alueita, joita verkossa ei ole.
     Aluenumeroiden tulee olla tiedostoissa nousevassa järjestyksessä.
   - Koko Suomen ajoihin (työasiointi- ja yön yli -matkojen malli sekä tallennetun nopeuden sijoittelu) ei tarvita alueellisten osamallien lähtökysyntämatriiseja.
     Lähtödatan kansiossa tulee kuitenkin aina olla demand_matrices-kansio, muuten ajo pysähtyy virheeseen _Baseline matrix directory … does not exist_.
     Työasiointi- ja yön yli matkojen malli käyttää lisäksi tiedostoa `business_and_overnight\ext_foreign_passenger_vrk.omx`,
     jossa on ulkomaille suuntautuva ja ulkomailta saapuva henkilöliikenteen vuorokausikysyntä.
     Jos tiedosto puuttuu, ulkomaanmatkat jäävät pois pitkien matkojen mallista ilman virheilmoitusta.

3. Luo resurssinhallintaasi projektikansio, jonne VALMA-ajo tallentaa käyttöliittymän projektin asetukset, EMME-projektin ja mallitulokset.
   Projektikansiossa ei tarvitse olla sisältöä.
   
## VALMA-projekti

1. Avaa käyttöliittymä, luo uusi VALMA-projekti ja määrittele sen asetukset:
   - Nimeä projektisi.
   - Valitse projektikansioksi resurssinhallintaasi tallentamasi kansio. Tämän ei tarvitse olla samanniminen kuin projekti.
   - Tarkista kohta Emme Python v311. Siinä tulee olla EMMEn Python-tulkin polku, yleensä `%EMMEPATH%\Python311\python.exe`.
     Painike _Hae Python automaattisesti_ etsii tulkin oletussijainnista.
   - Viittaa lataamasi mallijärjestelmän Scripts -kansioon kohdassa valma model system,
     tai lataa mallijärjestelmä painikkeella _Lataa eri versio internetistä_ (ks. [Asennus](asennus.md)).
   - Viittaa kansioon, joka sisältää demand_matrices-kansion kohdassa lähtödatan sisältävä kansio.
   - Aseta tarvittaessa kulkutapa- ja suuntautumismallien kalibrointiparametrit (.json) tai kunta-kunta-kalibroinnin tiedosto (.txt).
     Tiedostojen käytöstä voit lukea lisää [täältä](henkiloliikennemallin_kalibrointi.md).
   - Tallenna asetukset.

   Olemassa olevan projektin asetuksia voi käyttää uuden projektin pohjana valinnalla _Valitse toinen projekti pohjaksi_.
   Osa projektiasetuksista (projektikansio, Python-polku, mallijärjestelmän polku ja lähtödatan sisältävä kansio) voidaan yliajaa
   yksittäiselle skenaariolle skenaarion kohdassa _Skenaariokohtaiset yliajot_.
   Kalibrointitiedostot ovat projektiasetuksia, joten ne koskevat kaikkia projektin skenaarioita.

   Kun olet luonut uuden VALMA-projektin, projektikansioon syntyy myös uusi Emme-projekti `<projektikansio>\<projektin nimi>\<projektin nimi>.emp`.

3. Luo seuraavaksi vähintään yksi Emme-pankki valitsemalla _Luo Emmepankki_. Valitse osamalli ja skenaarioiden lukumäärä.
   Osamallin valinta vaikuttaa tässä vaiheessa vain Emme-pankin otsikkoon ja kokoon.
   > HUOM:
   > - Voit tarvittaessa luoda Emme-projektiin useita erilaisia pankkeja valitsemalla _Luo Emmepankki_ uudestaan.
   >   Käyttöliittymä antaa pankin otsikoksi osamallin tunnuksen: _koko_suomi_, _alueelliset_osamallit_ (Alueelliset osamallit yhdessä),
   >   _koko_suomi_kunta_ (Koko Suomi kuntajaossa) sekä alueellisten osamallien mukaisesti _ita_suomi_, _uusimaa_, _pohjois_suomi_ tai _lounais_suomi_.
   > - Emmen käyttöliittymässä voit tarvittaessa kytkeä muitakin pankkeja projektiin.
   >   Huolehdi siinä tapauksessa siitä, että Emme-pankin otsikko on jonkin alueellisen osamallin mukainen tai _koko_suomi_ tai _alueelliset_osamallit_.
   > - "Tallenna ajanjaksot erillisiin Emme-skenaarioihin" -valinta vaikuttaa ekstra-attribuuttien tilatarpeeseen.
   >   Emme-skenaariot tarvitsevat vähemmän ekstra-attribuuttitilaa jos on tarkoitus tallentaa ajanjaksot erillisiin skenaarioihin.
   >   Silloin pitää kuitenkin muistaa luoda tarpeeksi skenaarioita (alueellisissa osamalleissa verkkoskenaarion lisäksi viisi Emme-skenaariota, ks. kohta 4).
   >   Jos on tarkoitus tehdä vain pitkien matkojen ennuste, täppä on mahdollinen laittaa päälle säästäkseen levytilaa vaikka malliajossa
   >   olisi tarkoitus käyttää vain yhtä Emme-skenaariota (vrk-sijoitteluihin).
   - Emme-pankin luominen avaa sen EMME-käyttöliittymään.

5. Tuo Emme-skenaarioksi lataamasi verkko tai verkot Emme-pankkiin Emmen Modeller Import Scenario työkalun avulla.
   Kopioi tarvittaessa skenaario Modellerin Copy Scenario työkalun avulla ja tee tarvittavat verkkomuutokset.
   Jos aiot tallentaa ajanjaksot erillisiin Emme-skenaarioihin, alueellisten osamallien verkkoskenaarion perään pitää jättää viisi vapaata skenaarionumeroa.
   Malli kopioi verkkoskenaarion uusiin skenaarioihin ja tallentaa tulokset niihin seuraavasti:

   | Skenaarionumero | Sisältö |
   |---|---|
   | _n_ | Lähtötietona annettu verkkoskenaario |
   | _n_ + 1 | Koko vuorokauden (vrk) tulokset |
   | _n_ + 2 … _n_ + 5 | Ajanjaksojen aht, pt, iht ja it tulokset |

   Pitkien matkojen mallin ajossa (vain vrk-ajanjakso) käytetään numeroita _n_ + 1 ja _n_ + 2.
   Samannumeroiset olemassa olevat skenaariot ylikirjoitetaan, joten varmista myös, että pankkiin mahtuu tarvittava määrä skenaarioita.
   Verkon sisällön vaatimukset on kuvattu sivulla [EMME-verkon kuvaus](emme_verkko.md).
   > HUOM: Pidä Emme-skenaarion otsikko lyhyenä. Malli lisää otsikkoon ajanjakson tunnuksen luodessaan skenaarioita, ja EMME sallii enintään 60 merkkiä.
   > Yli 56 merkin otsikot hylätään lähtötietojen tarkistuksessa.

## Emme-projektin ja -pankin tiedot

VALMA ajaa sijoittelunsa Emme-projektissa. Emme-projekti (`.emp`-tiedosto) sisältää yhden tai useamman Emme-pankin (emmebank),
ja jokainen pankki sisältää yhden tai useamman Emme-skenaarion.
Kukin verkkovaihtoehto (esimerkiksi ennustevuosi tai hankevaihtoehto) tallennetaan omaksi Emme-skenaariokseen osamallin pankkiin.
Usein on käytännöllistä luoda yksi Emme-projekti tarkastelua kohden ja koota siihen kaikki tarkastelun skenaariot (esimerkiksi nykytila ja vaihtoehdot).

Käyttöliittymän _Luo Emmepankki_ -toiminto luo uuden pankin kansioon `<projektikansio>\<projektin nimi>\<osamalli>\emmebank`. Pankki
- saa otsikokseen osamallin tunnuksen (esimerkiksi `uusimaa`)
- käyttää UTF-8-merkistöä
- käyttää koordinaattiyksikköä 0,001, eli solmujen koordinaatit ovat metreinä ja linkkien pituudet kilometreinä
- sisältää yhden tyhjän Emme-skenaarion.

Jos projektissa on vain yksi pankki, sitä käytetään sen otsikosta riippumatta. Älä nimeä kuitenkaan käyttöliittymän luomia pankkeja uudelleen.

Pankin mitat asetetaan automaattisesti valitun osamallin mukaan:

*Taulukko x. Emme-pankin mitat*

| Mitta | Alueelliset osamallit | koko_suomi | koko_suomi_kunta |
|---|---|---|---|
| Sentroidit | 3 400 | 10 000 | 320 |
| Tavalliset solmut | 55 000 | 120 000 | 50 000 |
| Linkit | 150 000 | 350 000 | 130 000 |
| Joukkoliikennelinjat | 3 300 | 8 000 | 8 000 |
| Joukkoliikennesegmentit | 320 000 | 700 000 | 500 000 |

Lisäksi kaikissa pankeissa on tilaa 9 999 täydelle matriisille, 99 funktiolle, 40 joukkoliikenteen ajoneuvotyypille ja 5 000 operaattorille.
Ekstra-attribuuteille varattava tila lasketaan verkon koon, sijoitteluluokkien määrän sekä sen perusteella, tallennetaanko ajanjaksot erillisiin skenaarioihin.
Ennen jokaista malliajoa lähtötietojen tarkistus varmistaa, että pankissa on riittävästi tilaa mallin luomille ekstra-attribuuteille.
Jos tilaa ei ole, ajo pysähtyy virheeseen _"At least N words required for extra attributes"_.

### Emme-pankin lisääminen käsin

Emme-pankin voi luoda tai importoida myös EMME Desktop -sovelluksessa:
1. Avaa projektin Emme-projekti `<projektikansio>\<projektin nimi>\<projektin nimi>.emp`.
3. Lisää pankki käytettävälle osamallille vähintään edellä esitetyillä mitoilla. Anna pankin otsikoksi osamallin tunnus.
   Emme-pankin sijainti voi olla mikä tahansa, kunhan Emme-projekti on `<projektikansio>\<projektin nimi>\<projektin nimi>.emp`.
5. Aseta koordinaattiyksikön pituudeksi 0,001.

### Mallin luomat EMME-tiedot

Malli luo jokaisen ajon alussa tarvitsemansa matriisit, viivytys- ja joukkoliikenteen matka-aikafunktiot sekä ekstra-attribuutit.
Pankissa jo olevat samannumeroiset funktiot ylikirjoitetaan.
Poikkeuksena ovat linkkien ekstra-attribuutit `@ferry_wait_time` ja `@freight_gate`, joiden tulee olla verkossa valmiina (ks. [EMME-verkon kuvaus](emme_verkko.md)).

> HUOM: Jos matriisien tallennusta Emme-pankkiin ei ole valittu (ks. kohta _Lisävalinnat_ alempana),
> henkilöliikenteen malliajon lopussa __pankista poistetaan kaikki matriisit__, myös ne, joita malli ei ole luonut.
> Älä säilytä omia matriisejasi pankissa, jota käytetään VALMA-ajoihin.

## VALMA-skenaariot

1. Luo VALMA-skenaario käyttöliittymässä.
   Voit luoda henkilöliikenteen skenaarion (_Uusi henkilöliikenteen skenaario_) tai tavaraliikenteen skenaarion (_Uusi tavaraliikenteen skenaario_).
   Skenaarion nimessä tulee olla vähintään kolme merkkiä, eikä projektissa saa olla toista samannimistä skenaariota.
   > HUOM: Käyttöliittymän vanhemmilla versioilla luodut erilliset pitkien matkojen skenaariot (tyyppi `long_distance`) eivät näy käyttöliittymässä, kun projekti avataan.
   > Niiden tiedostot jäävät projektikansioon, mutta skenaariot on luotava uudelleen henkilöliikenteen skenaarioina.

### Henkilöliikenteen skenaario

Yksi henkilöliikenteen skenaario voi kattaa sekä työasiointi- ja yön yli -matkojen mallin (aina koko Suomen verkolla) että alueelliset osamalliajot.
Kukin skenaario vastaa yhtä verkkojen, aluetietojen ja hintadatan yhdistelmää.

- Viittaa lataamaasi aluetietoon (.gpkg) kohdassa Aluetiedot.
- Viittaa lataamaasi hintadataan (.json) kohdassa Liikenteen hintadata.
- Valitse iteraatioiden enimmäismäärä (oletus 15, sallittu 1–99) tai pelkkä loppusijoittelu (_Aja vain loppusijoittelu_).
  Iteraatioiden enimmäismääräs koskee skenaarion osamalliajoja.
  Työasionti - ja yön yli -matkojen sekä koko Suomen ajoissa iteraatioiden määrä on aina 1.
  - Jos ajat vain loppusijoittelun, kysyntämatriisit tulevat lähtödatasta.
    Jos haluat, että kysyntämatriisit tulevat projektikohtaisten pohjamatriisien sijaan jo tehdystä Valma-skenaariokohtaisesta kysyntäennusteesta,
    luo sille skenaariolle uusi aliskenaario.
- Tavaraliikenteen (kuorma-autojen) kysyntäennuste otetaan kohdassa _Tavaraliikenteen kysyntäennuste_ joko projektin lähtödatasta (_Ota projektin lähtödatasta_)
  tai malliajon tuloskansiosta (_Ota malliajon tuloskansiosta_).
  Kansiossa tulee olla vuorokauden kysyntätiedosto `demand_vrk.omx`, jossa ovat luokat `truck`, `semi_trailer` ja `trailer_truck`.
  > HUOM: Tavaraliikenteen malli tallentaa kuorma-autojen kysynnän nimellä `freight_demand_vrk.omx`,
  > mutta henkilöliikenteen malli lukee annetusta kansiosta tiedoston `demand_vrk.omx`.
  > Jos käytät tavaraliikenteen malliajon tulosta, kopioi tiedosto erilliseen kansioon nimellä `demand_vrk.omx` ja viittaa siihen kansioon.
- Valitse pitkien matkojen (työasiointi-, yön yli- ja ulkomaanmatkat) kysynnän lähde kohdassa _Työasionti - ja yön yli -matkojen ennuste_:

  | Valinta | Komentorivin arvo | Kuvaus |
  |---|---|---|
  | _Ota projektin lähtödatasta_ (oletus) | `base` | Työasionti - ja yön yli -matkojen kysyntä luetaan lähtödatan tiedostosta `long_dist_demand_vrk.omx`. Käytä, kun tarkasteltu kohde ei olennaisesti muuta pitkiä, harvoin tehtyjä matkoja. |
  | _Ota malliajon tuloskansiosta_ | kansion polku | Työasionti - ja yön yli -matkojen kysyntä luetaan aiemman malliajon tuloksista. Viittaa kansioon `projektikansio\skenaarion_nimi\demand_matrices\business_and_overnight`, jossa on tiedosto `demand_vrk.omx`. Voit luoda kansion valmiiksi ja viitata siihen, vaikka ajo ei olisi vielä suoritettu. |
  | _Aja_ ja _Emme-skenaario (koko suomi)_ | `calc` | Työasionti - ja yön yli -matkojen malli ajetaan annetussa koko Suomen Emme-skenaariossa, ja skenaarion alueelliset osamallit käyttävät sen tulosta. |

  Työasionti - ja yön yli -matkojen mallin ajossa henkilöautot sijoitellaan koko vuorokaudelle vapaan nopeuden matka-ajoilla.
  Joukkoliikennesijoittelussa käytetään koko vuorokauden keskimääräisiä vuorovälejä.
  Jos Emme-projektissa on useita Emme-pankkeja, mallijärjestelmä käyttää pankkia, jonka otsikko on "koko_suomi".
  Jos työasionti - ja yön yli -matkojen kysyntä otetaan aiemmasta malliajosta, varmista, että ajossa on käytetty samaa malliversiota ja yhteensopivia lähtötietoja.
- Valitse ajettavat osamallit valintaruuduilla (_Itä Suomi_, _Lounais Suomi_, _Pohjois Suomi_, _Uusimaa_)
  ja anna kullekin sen verkon sisältävän Emme-skenaarion numero (_Emme skenaario_).
  Jos Emme-projektissa on useita emmepankkeja, mallijärjestelmä yrittää löytää osamallin mukaan nimetyn Emme-pankin tai Emme-pankin nimeltään "alueelliset_osamallit".
  Jos valitulle osamallille ei ole annettu Emme-skenaarion numeroa, käyttöliittymä antaa virheen _Tarkista valittujen mallien --first-scenario-id_.
- Koko Suomen koontiajo ajetaan käyttöliittymästä aina tallennetun nopeuden sijoittelulla (koko Suomen ruuhkasijoittelu voisi viedä aikaa jopa viikon).
  Koko Suomen koontiajo on tarpeellinen vain, jos tarkastelukohde ulottuu useampaan osamalliin.
  Jos skenaariossa on ajettavia osamalleja, niiden linkkimatka-ajat siirtyvät automaattisesti koko Suomen ajoon.
  Lisää tietoja tästä kohdassa [Tallennetun nopeuden sijoittelu](#tallennetun-nopeuden-sijoittelu-koko-suomen-koontiajo).

Kun skenaario ajetaan, käyttöliittymä ajaa sen osat peräkkäin erillisinä malliajoina tässä järjestyksessä:
1. Työasionti - ja yön yli -matkojen malli, jos _Aja_ on valittu
2. valitut alueelliset osamallit (Itä-Suomi, Lounais-Suomi, Pohjois-Suomi, Uusimaa)
3. koko Suomen tallennetun nopeuden sijoittelu, jos se on valittu.

Kaikki osat kirjoittavat tuloksensa samaan skenaarion tuloskansioon osamallin mukaan nimettyihin alikansioihin.

#### Tallennetun nopeuden sijoittelu (koko Suomen koontiajo)

- Tallennetun nopeuden sijoittelussa autoliikenne sijoitellaan kaikki-tai-ei-mitään-menetelmällä verkolle tallennetuilla matka-ajoilla, ja ajossa on aina yksi iteraatio.
- Matka-ajat luetaan linkkien network field -attribuuteista `#car_time_aht`, `#car_time_pt`, `#car_time_iht`, `#car_time_it` ja `#car_time_vrk`.
- Alueellisten osamallien ajot tallentavat ruuhkautuneet auton linkkimatka-ajat tuloskansioon tiedostoihin `netfield_links_<osamalli>.txt`
  (vain osamallin oman alueen linkit, ks. [EMME-verkon kuvaus](emme_verkko.md), attribuutti `#subarea`).
  Tallennetun nopeuden sijoittelu tuo ennen sijoittelua verkolle kaikki skenaarion tuloskansiosta löytyvät `netfield_links`-tiedostot.
- Koko Suomen tallennetun nopeuden sijoittelu voidaan tehdä kahdella tavalla riippuen, onko sinulla kaikki osamallit jo ajettavissa vai ei.
   - Jos olet ajamassa saman skenaarion kaikki alueelliset osamallit, malli tuottaa linkkimatka-ajat ja siirtää ne automaattisesti koko Suomen verkolle.
     Vasta tämän jälkeen se suorittaa koko Suomen malliajon tallennetun nopeuden sijoittelulla.
   - Jos et aja kaikkia alueellisia osamalleja (koska tarkastelukohde ei vaikuta ajonopeuksiin valtakunnallisesti), linkkimatka-ajat pitää tuoda muualta ennen ajoa.
     Malliajossa tulee virheilmoitus jos linkkimatka-ajat puuttuvat tallennetun nopeuden sijoittelussa.
- Skenaarion _Lisävalinnat_-kohdan valinta _Tallennetun nopeuden sijoittelu_ koskee alueellisia osamalleja: kun se on valittu,
  myös alueelliset osamallit sijoitellaan tallennetuilla matka-ajoilla.
  Tämä mahdollistaa vaikutusten nopean arvioinnin; perusmalliajon jälkeen voidaan nopeasti arvioida vaikutuksia esim. pienistä muutoksista joukkoliikennetarjonnassa.

### Tavaraliikenteen skenaario

- Viittaa kohdassa "Liikenneverkon sisältävä Emme-skenaario" luomaasi Emme-skenaarioon.
- Viittaa lataamaasi aluekohtaiseen lähtötietoon (.gpkg) kohdassa Aluetiedot, jossa on ennustevuoden tavaraliikenteen generaatio- ja attraktiodata.
- Viittaa lataamaasi hintadataan (.json) kohdassa liikenteen hintadata.
- Viittaa lataamaasi vienti- ja tuontidataan (.omx) kohdassa vienti- ja tuontidata.
  Vienti- ja tuontidata on OMX-tiedosto (.omx), joka sisältää hyödykkeittäiset tuonti- ja vientimäärät.
  Tavaraliikenteen malli käyttää sitä ulkomaankaupan reitinvalinnassa. Tiedosto on pakollinen.
- Tavaraliikenne käyttää automaattisesti koko Suomen osamallia.
  Malli käyttää koko Suomen verkkoa ja aluejakoa riippumatta skenaarion osamallivalinnasta.
  Jos Emme-projektissa on useita Emme-pankkeja, tavaraliikenteen malli käyttää pankkia, jonka otsikko on "koko_suomi".

Tavaraliikenteen malli ajetaan yhdellä kierroksella:
1. Tyhjän tavaraliikenneverkon sijoittelu vastusten laskemiseksi.
2. Ulkomaankaupan reitinvalinta (satama tai raja-asema) jokaiselle tuonti- ja vientihyödykkeelle.
3. Kotimaan kysyntä ja kuljetustavan valinta jokaiselle hyödykkeelle.
4. Tiekuljetusten tonnien muuntaminen ajoneuvoiksi.
5. Ajoneuvojen ja tonnien loppusijoittelu.

Tuloksena syntyvä kuorma-autojen vuorokausikysyntä tallentuu tiedostoon `projektikansio\skenaarion_nimi\demand_matrices\koko_suomi\freight_demand_vrk.omx`.

### Aliskenaariot

Skenaariolle voi luoda aliskenaarioita (_Luo aliskenaario_).
Aliskenaariolla on oma nimi, osamalli, Emme-skenaarion numero ja hintadata (.json).
Aliskenaario ajetaan aina pelkkänä loppusijoitteluna,
ja sen kysyntämatriisit otetaan pääskenaarion tuloskansiosta (`projektikansio\pääskenaarion_nimi\demand_matrices\<osamalli>`).
Pääskenaario on siis ajettava ensin. Aliskenaarioilla voi esimerkiksi testata kustannus- tai verkkomuutoksia laskematta kysyntää uudelleen.

### Lisävalinnat

Skenaarion lisävalinnoilla ja niitä vastaavilla komentoriviparametreilla vaikutetaan malliajon kulkuun:

| Valinta käyttöliittymässä | Komentoriviparametri | Kuvaus |
|---|---|---|
| Aja vain loppusijoittelu | `-o`, `--end-assignment-only` | Sijoittelee lähtökysyntämatriisit laskematta kysyntää. Hyödyllinen verkon nopeaan tarkistamiseen. |
| – | `-c`, `--car-end-assignment-only` | Kuten edellä, mutta vain autoliikenteen kysyntä sijoitellaan. |
| Tallennetun nopeuden sijoittelu | `-x`, `--stored-speed-assignment [kansiot]` | Ks. kohta [Tallennetun nopeuden sijoittelu](#tallennetun-nopeuden-sijoittelu-koko-suomen-koontiajo) edellä. Komentorivillä voi antaa tuloskansiot, joiden `netfield_links`-tiedostoista matka-ajat tuodaan; muuten käytetään skenaarion omaa tuloskansiota. Pakottaa yhden iteraation. |
| Tallenna ajanjaksot erillisiin Emme-skenaarioihin | `-s`, `--separate-emme-scenarios` | Tallentaa kunkin ajanjakson tulokset erillisiin Emme-skenaarioihin. |
| Tallenna ajanjaksojen matriisit Emme-projektin Database-kansioon | `-e`, `--save-emme-matrices` | Tallentaa kaikkien ajanjaksojen kysyntä- ja vastusmatriisit Emme-pankkiin alkaen kohdassa _Matriisit tallennetaan numeroille_ annetusta numerosta (`--first-matrix-id`). Muuten kaikki matriisit poistetaan pankista ajon lopussa. |
| Poista sijoittelun strategiatiedostot malliajon jälkeen (oletuksena valittu) | `-d`, `--del-strat-files` | Poistaa joukkoliikennesijoittelun strategiatiedostot (`STRAT_s*`, `STRATS_s*`) Emme-pankin kansiosta ajon jälkeen. Tiedostot ovat suuria, mutta niitä tarvitaan joukkoliikenteen reittianalyyseihin EMMEssä. |
| – | `--delete-extra-matrices` | Säilyttää vain kysyntälaskennassa tarvittavat matriisit, mikä säästää muistia ja levytilaa. |
| – | `-m`, `--do-not-use-emme` | Käyttää mock-sijoittelua, joka lukee valmiiksi lasketut vastusmatriisit. Vain testaukseen. |

### Iteraatiot ja konvergenssi

Kysyntälaskentaa ja sijoittelua iteroidaan, kunnes kysyntä on vakiintunut.
Jokaisen iteraation jälkeen malli vertaa aamuhuipputunnin (aht) polttomoottorihenkilöautojen (sijoitteluluokka `icev`) kysyntämatriisia edelliseen iteraatioon:
- __suurin muutos__ (`--max-gap`, oletus 1,0): suurin muutos yksittäisessä lähtö–määräpaikkasolussa
- __suhteellinen muutos__ (`--rel-gap`, oletus 0,01): matriisin kokonaiskysynnän suhteellinen muutos.

Kun molemmat alittavat raja-arvonsa, malli ajaa vielä yhden viimeisen iteraation.
Jos iteraatioiden enimmäismäärä (`--iterations`, oletus 15) saavutetaan ensin, malli pysähtyy ja kirjoittaa lokiin varoituksen _"Model has not converged"_.

Viimeinen iteraatio on erityinen: toissijaiset matkakohteet lasketaan kaikille kulkutavoille, sijoittelut ajetaan tiukemmilla lopetusehdoilla ja kaikki tulokset kirjoitetaan.

Kunkin iteraation konvergenssitunnusluvut kirjoitetaan tiedostoon `demand_convergence.txt`, ja ne näkyvät käyttöliittymässä ajon aikana.

> HUOM: Konvergoitumattoman ajon tuloksia ei tule käyttää tarkistamatta. Kasvata iteraatioiden enimmäismäärää tai tarkista lähtötiedot.

### Skenaarioiden ajaminen

1. Valitse ajettavat skenaariot skenaarioluettelosta.
2. Käynnistä ajo.
3. Käyttöliittymä tarkistaa ensin kaikkien valittujen skenaarioiden lähtötiedot ja verkot (`validate_inputfiles.py`).
   Jos virhe löytyy, ajoa ei käynnistetä ja virhe näytetään lokissa.
5. Skenaariot ajetaan peräkkäin. Ajon eteneminen, kunkin iteraation kulkutapaosuudet ja mahdolliset varoitukset näkyvät ajon lokissa.

Ajon voi keskeyttää, jolloin vielä aloittamattomat skenaariot ohitetaan.
Ajoajat riippuvat osamallista, iteraatioiden määrästä ja tietokoneesta.
Kysyntälaskenta käyttää kaikkia käytettävissä olevia prosessoriytimiä.

Jokainen ajo kirjoittaa skenaarion tuloskansioon lokitiedoston `<skenaarion nimi>.log`.
Henkilöliikenteen ajot (`valma_travel.py`) ja autonomistusmallin ajot (`valma_cars.py`) kirjoittavat lisäksi ajon parametrit tiedostoon `runtime_params.json`.
Tavaraliikenteen malli ei kirjoita tätä tiedostoa.

`runtime_params.json` on samassa muodossa kuin komentorivillä käytettävä asetustiedosto, joten henkilöliikenteen ajon voi toistaa täsmälleen samanlaisena.

## Ajaminen komentoriviltä

Mallijärjestelmää voi ajaa ilman käyttöliittymää. Avaa komentokehote mallijärjestelmän `Scripts`-kansiossa ja aja

```
python valma_travel.py --help
```

nähdäksesi kaikki parametrit. Parametrit annetaan jommallakummalla tavalla:
- __Komentoriviparametreina.__ Parametrit, joita ei anneta komentorivillä, luetaan `Scripts`-kansion tiedostosta `dev-config.json`.
- __JSON-tiedostona__ parametrilla `--json <tiedosto>`.
  Tällöin __kaikki__ parametrit luetaan JSON-tiedostosta: tiedostosta puuttuvat parametrit saavat tyhjän arvon ja valinnat (flags) ovat pois päältä,
  vaikka ne olisi annettu komentorivillä tai tiedostossa `dev-config.json`.
  Älä siis yhdistä `--json`-parametria muihin komentoriviparametreihin, vaan anna JSON-tiedostossa kaikki ajon tarvitsemat parametrit.

JSON-tiedostoissa parametrien nimet kirjoitetaan isoilla kirjaimilla alaviivoin (esim. `SCENARIO_NAME`), ja valinnat (flags) luetellaan kohdassa `OPTIONAL_FLAGS`
(esim. `"OPTIONAL_FLAGS": ["SEPARATE_EMME_SCENARIOS", "DEL_STRAT_FILES"]`).
Valinnan nimi on komentorivivalinnan pitkä muoto isoin kirjaimin ja alaviivoin.
Poikkeuksena valinta `--save-emme-matrices` kirjoitetaan JSON-tiedostoon muodossa `SAVE_MATRICES`.

Esimerkki alueellisen osamallin ajon asetustiedostosta:

```json
{
    "LEM_VERSION": "v0.0.1",
    "LOG_LEVEL": "INFO",
    "LOG_FORMAT": "TEXT",
    "SCENARIO_NAME": "2030_v1_uusimaa",
    "RESULT_DATA_FOLDER": "C:\\valma\\results",
    "SUBMODEL": "uusimaa",
    "EMME_PROJECT_FILE": "C:\\valma\\emme\\my_project\\my_project.emp",
    "FIRST_SCENARIO_ID": 10,
    "FIRST_MATRIX_ID": 100,
    "BASE_DATA_FOLDER": "C:\\valma\\base_data",
    "ZONE_DATA_FILE": "C:\\valma\\input\\zonedata_2030.gpkg",
    "COST_DATA_FILE": "C:\\valma\\input\\costdata_2030.json",
    "LONG_DIST_DEMAND_FORECAST": "C:\\valma\\results\\2030_v1_ld\\demand_matrices\\koko_suomi",
    "ITERATIONS": 15,
    "MAX_GAP": 1.0,
    "REL_GAP": 0.01,
    "OPTIONAL_FLAGS": ["DELETE_EXTRA_MATRICES"]
}
```

Ajo käynnistetään komennolla:

```
python valma_travel.py --json C:\valma\config\2030_v1_uusimaa.json
```


### Tyypillinen kaksivaiheinen henkilöliikenteen ajo

Tee kummallekin vaiheelle oma, täydellinen JSON-tiedosto edellä olevan esimerkin mukaisesti.
Ensimmäisessä tiedostossa (`2030_ld.json`) ovat muun muassa `"SCENARIO_NAME": "2030_ld"`, `"SUBMODEL": "koko_suomi"`, `"FIRST_SCENARIO_ID": 1` ja `"LONG_DIST_DEMAND_FORECAST": "calc"`.
Toisessa tiedostossa (`2030_uusimaa.json`) ovat `"SCENARIO_NAME": "2030_uusimaa"`, `"SUBMODEL": "uusimaa"`, `"FIRST_SCENARIO_ID": 10` ja `"LONG_DIST_DEMAND_FORECAST": "C:\\valma\\results\\2030_ld\\demand_matrices\\koko_suomi"`.

```
rem 1. Koko Suomen pitkien matkojen malli
python valma_travel.py --json C:\valma\config\2030_ld.json

rem 2. Alueellinen osamalli, joka käyttää pitkien matkojen tulosta
python valma_travel.py --json C:\valma\config\2030_uusimaa.json
```

Saman voi tehdä myös pelkillä komentoriviparametreilla ilman `--json`-parametria, jolloin kaikki tarvittavat parametrit (esim. `--emme-project-file`, `--base-data-folder`, `--zone-data-file`, `--cost-data-file` ja `--result-data-folder`) annetaan komentorivillä.

### Tavaraliikenteen malli

```
python valma_freight.py --scenario-name 2030_freight --emme-project-file <.emp> ^
    --first-scenario-id 1 --zone-data-file <tavaraliikenteen aluetiedot .gpkg> ^
    --cost-data-file <hintadata .json> --trade-demand-file <vienti- ja tuontidata .omx> ^
    --result-data-folder <tuloskansio>
```

Parametrilla `--specify-commodity-names` voi tallentaa valittujen hyödykkeiden kysyntämatriisit ja verkkokuormitukset (esim. `--specify-commodity-names metsat puukor`).

### Autonomistusmalli

`valma_cars.py` laskee aluetiedoille autonomistuksen todennäköisyydet kotitaloussegmenteittäin ajamatta muuta mallia:

```
python valma_cars.py --scenario-name 2030_cars --submodel uusimaa --zone-data-file <.gpkg>
```

### Lähtötietojen tarkistus

Saman tarkistuksen, jonka käyttöliittymä tekee ennen jokaista ajoa, voi ajaa erikseen:

```
python validate_inputfiles.py --scenario-name 2030_uusimaa --submodel uusimaa ^
    --base-data-folder <lähtödatan kansio> --emme-project-files <.emp> --first-scenario-ids 10 --zone-data-files <.gpkg> ^
    --cost-data-files <.json> --long-dist-demand-forecast base --freight-matrix-paths none
```

Useita skenaarioita voi tarkistaa kerralla antamalla jokaiselle parametrille useita arvoja.

## Vianetsintä

| Virheilmoitus | Todennäköinen syy |
|---|---|
| _Baseline matrices' directory '…' does not exist._ | Lähtötietojen tarkistus: lähtödatan sisältävä kansio on väärä, tai siinä ei ole demand_matrices-kansiota ja sen alla osamallin kansiota. |
| _Baseline matrix directory '…' does not exist._ | Malliajon alussa: lähtödatan sisältävä kansio on väärä, tai siinä ei ole demand_matrices-kansiota (myös koko Suomen ajoissa). |
| _.emp project file not found_ | Emme-projektin polku on väärä. |
| _Project … has no scenario N_ (tarkistuksessa) / _EMME project has no scenario N_ (ajon aikana) | Emme-skenaarion numeroa ei ole osamallin pankissa. |
| _Scenario name: … too long, time period extension might exceed Emme's 60 characters limit._ | Emme-skenaarion otsikko on yli 56 merkkiä pitkä. |
| _At least N words required for extra attributes_ | Emme-pankissa ei ole tarpeeksi tilaa ekstra-attribuuteille. |
| _Network field … missing from scenario_ | Pakollista network field -attribuuttia ei ole tuotu verkkoon (ks. [EMME-verkon kuvaus](emme_verkko.md)). |
| _Attribute @ferry_wait_time missing from scenario N_ / _Attribute @freight_gate missing from scenario N_ | Pakollista linkkien ekstra-attribuuttia ei ole verkossa. |
| _No modes defined for link …_ | Linkillä ei ole yhtään kulkumuotoa. |
| _Zone numbers not in strictly ascending order in file …_ | Matriisitiedoston aluenumerot eivät ole nousevassa järjestyksessä. |
| _Zone number N from mapping … not found in network_ / _Zone number N not found in mapping_ | Aluetietojen osamallisarakkeen aluenumerot eivät vastaa verkon sentroideja. |
| _… for zone N is negative_ / _… is larger than one_ / _… is not a number_ | Aluetiedoissa on virheellinen arvo. |
| _Multiple layers found in file_ | Aluetietojen GeoPackage-tiedostossa saa olla vain yksi taso. |
| _No transit fares for operator id N_ | Joukkoliikennelinjan hintatunnukselle (ut1) ei löydy hintatietoja. |
| _Headway missing for line …_ | Joukkoliikennelinjalta puuttuu vuoroväli jollakin ajanjaksolla. |
| _Model has not converged_ | Iteraatioiden enimmäismäärä saavutettiin ennen konvergenssia. |
