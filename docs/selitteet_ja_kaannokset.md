---
nav_order: 5
sort: 5
---

# Selitteet ja käännökset

### Matka ja kiertomatka
Malli kuvaa liikkumista kiertomatkoina (tour) ja matkoina (trip). Kysyntämallit kuvaavat kiertomatkoja, jotka muunnetaan matkoiksi ennen liikenneverkolle sijotitelua.

* Kiertomatka (tour) kuvaa liikkumista kiertomatkan alkupisteestä yhden tai useamman matkan avulla takaisin samaan pisteeseen. Kiertomatka sisältää edestakaiset matkat ja mahdollisesti pysähdyksiä toissijaisiin matkakohteisiin. Tyypillinen kiertomatka voi olla esimerkiksi koti – kauppa –työpaikka – koti, joka muodostaa yhden kiertomatkan ja kolme matkaa. 

* Matkalla (trip) tarkoitetaan siirtymistä paikasta toiseen pihapiirin ulkopuolella. Matka voi sisältää pieniä pysähdyksiä, esimerkiksi kioskille. Jos matka kuitenkin keskeytyy pidemmäksi aikaa, tästä syntyy kaksi matkaa.

* Matka voidaan kulkea yhdellä tai usealla kulkutavalla, joista yksi on pääasiallinen kulkutapa. Mallissa kuvaataan tämän pääkulkutavan käyttöä matkoilla.

### Matkaryhmät
Alla esitetty mallin kuvaamien matkaryhmien nimet ja selitteet. Matkaryhmä määrittyy lähtöpaikan ja pääasiallisen matkakohteen perusteella.

| Koodi   | Kiertomatkan tyyppi                         |
|---------|---------------------------------------------|
| hb_work    | Kotiperäinen työmatka, jonka pääasiallinen matkakohde on työpaikka.  |
| hb_edu_basic    | Kotiperäinen koulumatka, jonka pääasiallinen matkakohde on koulu ja matkustaja on alle 15 vuotias.  |
| hb_edu_student    | Kotiperäinen opiskelumatka, jonka pääasiallinen matkakohde on opiskelupaikka ja matkustaja on yli 15 vuotias.  |
| hb_grocery | Kotiperäinen päivittäistavaroiden ostosmatka, jonka pääasiallinen matkakohde on päivittäistavarakauppa.  |
| hb_other_shop | Kotiperäinen muu ostos- tai asiointimatka, jonka pääasiallinen matkakohde on kauppakeskus, muu kauppa tai asiointipaikka. Sisältää myös sosiaali- ja terveyspalveluiden asioinnin. |
| hb_leisure | Kotiperäinen vapaa-ajan matka, jonka pääasiallinen matkakohde on ravintola, kahvila, kulttuurikohde tai muu vapaa-ajan kohde.  |
| hb_sport | Kotiperäinen urheilumatka, jonka pääasiallinen matkakohde on liikuntapaikka.  |
| hb_visit | Kotiperäinen vierailumatka, jonka pääasiallinen matkakohde on vierailupaikka ystävien, sukulaisten tai tuttavien luona.  |
| hb_escort | Kotiperäinen saattomatka, jonka pääasiallinen matkakohde on paikka henkilön noutamiseen tai jättöön kyydistä.  |
| hb_business | Kotiperäinen työasiamatka, jonka pääasiallinen matkakohde on työasiointikohde.  |
| hb_overnight | Kotiperäinen yön yli matka, joissa pivän ensimmäinen tai viimeinen matkakohde on ollut hotelli, kesämökki, kakkoskoti tai vierailupaikka. Matka on avoin kiertomatka, eli siltä ei ole palattu kotiin samana päivänä. |
| hb_abroad_other | Kotiperäinen ulkomaanmatka. |
| wb_business | Työperäinen työasiamatka, jolle on lähdetty työpaikalta ja pääasiallinen matkakohde on työasiointikohde.  |
| wb_other | Työperäinen muu matka, jolle on lähdetty työpaikalta ja pääasiallinen matkakohde on muu kuin työasiointikohde. Esimerkiksi työpäivän aikana tehtävät kauppa- tai ravintolavierailut. |
| ob_other |  Ei-kotiperäinen muu matka, jolle on lähdetty pääasiallisesta matkakohteesta. Sisältää muita vierailupaikoista tai vapaa-ajan kohteista käsin tehtäviä matkoja. |

Pääasiallinen matkakohde määritetään kiertomatkan aikana käydyistä paikoista seuraavalla prioriteeteilla:

1) Työpaikka
2) Opiskelupaikka
3) Vierailulupaikka, vapaa-ajan kohde, liikuntakohde
4) Kaupat, saattopaikat

Eli pääasialliseksi kohteeksi katsotaan ensisijaisestityöpaikka tai opiskelupaikka, jos kiertomatkan aikana on käyty näissä kohteissa. Mikäli kiertomatkalla on useampi kohden samalla prioriteetilla, on pääasiallinen kohde se paikka, jossa on vietetty eniten aikaa. 

Matkaryhmät hb_business, hb_overnight ja hb_abroad_other kuvataan koko Suomen pitkien matkojen mallissa, muut alueellisissa osamalleissa. Matkaryhmät wb_business, wb_other ja ob_other ovat toissijaisten matkakohteiden matkaryhmiä, jotka generoidaan kotiperäisistä kiertomatkoista: wb_business kotiperäisistä työmatkoista (hb_work), wb_other työ-, koulu- ja opiskelumatkoista (hb_work, hb_edu_basic, hb_edu_student) ja ob_other vapaa-ajan, urheilu- ja vierailumatkoista (hb_leisure, hb_sport, hb_visit).

### Aikajaksot
Malli kuvaa matkavalintoja ja liikennettä vuoden keskimääräisenä päivänä. Poikkeuksena joukkoliikenteen tarjonta kuvaa arkipäivän vuorotarjontaa ja palvelutasoa. Mallin tulosten laajentaminen vuositasolle tapahtuu kertoimella 365.

| Nimi          | Vastine suomeksi                   | Määritelmä |
|---------------|------------------------------------|-------------------|
| AHT          | Aamuhuipputunti | Kellonajat 07:10-08:10 |
| AH          | Aamuhuippu | Kellonajat 06:00-09:00 |
| IHT          | Iltahuipputunti | Kellonajat 16:10-17:10 |
| IH          | Iltahuippu | Kellonajat 15:00-18:00 |
| PT          | Päivätunti | Keskimääräinen päivätunti, joka on joukkoliikenteelle klo 09-15 ja muille kulkutavoille klo 09-15 ja klo 18-22. |
| IT          | Iltatunti  | Käytössä vain joukkoliikenteelle. Kellonajat klo 18-22. |
| VRK   | Vuorokausi | Koko vuorokausi |

Alueellisissa osamalleissa sijoittelut tehdään tuntiajanjaksoille (AHT, PT, IHT ja joukkoliikenteelle IT). Pitkien matkojen malli ja tavaraliikenteen malli sijoittelevat koko vuorokauden (VRK) kysynnän. Tuntitulokset laajennetaan vuorokausitasolle sijoitteluluokittaisilla kiinteillä kertoimilla.

### Kulkutavat liikenneverkolla
Alla on esitetty liikenneverkolle sijoiteltavien kulkutapojen nimet ja yksiköt. 

| Nimi          | Vastine suomeksi                   | Sijoitteluyksikkö |
|---------------|------------------------------------|-------------------|
| car          | Henkilöauto | Ajoneuvoa / [vrk/aht/iht/pt] |
| van          | Pakettiauto | Ajoneuvoa / [vrk/aht/iht/pt] |
| bike          | Pyörät | Henkilöä / [vrk/aht/iht/pt] |
| transit   | Joukkoliikenne | Henkilöä / [vrk/aht/iht/pt] |
| walk           | Kävely | Henkilöä / [vrk/aht/iht/pt] |
| airplane           | Lentokone | Henkilöä / [vrk/aht/iht/pt] |
| truck           | Kuorma-auto | Ajoneuvoa / [vrk/aht/iht/pt] |
| semi_trailer           | Puoliperävaunuyhdistelmä | Ajoneuvoa / [vrk/aht/iht/pt] |
| trailer_truck           | Täysperävaunuyhdistelmä | Ajoneuvoa / [vrk/aht/iht/pt] |

Henkilöautoliikenne (car) sijoitellaan kolmessa käyttövoimittaisessa luokassa: polttomoottoriautot (`icev`), täyssähköautot (`bev`) ja lataushybridit (`phev`). Luokkien osuudet annetaan kustannustietojen kohdassa `car_shares` (ks. [Malliajon lähtötiedot](malliajon_lahtotiedot.md)). Joukkoliikenteen (transit) luokka sisältää liityntä- ja poistumismatkat.

### Kulkutavat kysyntämallissa
Alla on esitetty kysyntämallin kuvaamien kulkutapojen nimet ja yksiköt. 

| Nimi          | Vastine suomeksi                   | Sijoitteluyksikkö |
|---------------|------------------------------------|-------------------|
| car_driver          | Henkilöauto kuljettajana. | Sijoitellaan liikenneverkolle. |
| car_passenger          | Henkilöauto matkustajana  | Ei sijoitella liikenneverkolle. |
| bike          | Pyöräily | Sijoitellaan liikenneverkolle. |
| transit   | Joukkoliikenne | Sijoitellaan liikenneverkolle. |
| walk           | Kävely | Sijoitellaan liikenneverkolle (loppusijoittelussa). |
| airplane           | Lentokone | Sijoitellaan liikenneverkolle. |
| transit_car_access | Pitkän matkan joukkoliikenne, liityntä autolla (liityntäpysäköinti) | Sijoitellaan liikenneverkolle. |
| transit_taxi_access | Pitkän matkan joukkoliikenne, liityntä taksilla | Sijoitellaan liikenneverkolle. |
| transit_taxi_egress | Pitkän matkan joukkoliikenne, poistuminen taksilla | Sijoitellaan liikenneverkolle. |
| airplane_car_access | Lentoliikenne, liityntä autolla | Sijoitellaan liikenneverkolle. |
| airplane_car_egress | Lentoliikenne, poistuminen autolla | Sijoitellaan liikenneverkolle. |
| airplane_taxi_access | Lentoliikenne, liityntä taksilla | Yhdistetään luokkaan airplane_car_access ennen sijoittelua. |

Kysyntämallissa ei ole pitkän matkan joukkoliikenteen autolla poistumisen kulkutapaa. Sijoittelussa käytettävä luokka `transit_car_egress` muodostetaan transponoimalla kulkutavan `transit_car_access` kysyntä.

Kaikki kulkutavat eivät ole käytettävissä kaikissa matkaryhmissä. Esimerkiksi pitkien matkojen matkaryhmissä ei ole pyöräilyä, eikä perusopetuksen koulumatkoissa (hb_edu_basic) ole henkilöautoa kuljettajana. Ulkomaanmatkoilla (hb_abroad_other) kulkutapoina ovat vain joukkoliikenne ja lentoliikenne. Autolla tai taksilla liittyminen pitkän matkan joukkoliikenteeseen ja lentoliikenteeseen on mahdollista vain pitkien matkojen mallissa.

### Käsitteet

Dokumentaatiossa ja mallin käytössä käytettyjä käsitteitä. Suluissa on englanninkielinen vastine.

- __Aggregointi__ (aggregation) tarkoittaa tietojen yhdistämistä suuremmiksi yksiköiksi, esimerkiksi syöttöalueista sijoittelualueiksi tai alueista kunnittain.
- __Aliskenaario__ (sub-scenario) on VALMA-skenaarion muunnelma, jolla on oma hintadata ja joka käyttää pääskenaarion kysyntämatriiseja.
- __Diskreetti valintamalli__ (discrete choice model) on tilastollinen valintojen malli, jossa yksilö valitsee yhden vaihtoehdon useista erillisistä vaihtoehdoista, esimerkiksi kulkutavan.
- __EMME__ eli OpenPaths EMME on Bentley Systemsin liikennesuunnitteluohjelmisto, jota VALMA käyttää verkkoihin ja sijoitteluun.
- __Emme-pankki__ (EMME databank) on Emme-projektin tietokanta. VALMAssa osamalleilla on omat pankkinsa, tai alueelliset osamallit voivat käyttää yhteistä pankkia.
- __Emme-skenaario__ (EMME scenario) on Emme-pankkiin tallennettu verkko. Ei pidä sekoittaa VALMA-skenaarioon.
- __Ennusteskenaario__ (forecast scenario) on tulevaa tilannetta kuvaava lähtötietojen yhdistelmä. Ennusteessa mallia käytetään samoilla parametreilla kuin estimoinnissa, mutta eri lähtötiedoilla.
- __Estimointi__ (estimation) tarkoittaa malliparametrien määrittämistä niin, että malli toistaa mahdollisimman hyvin tutkimusaineistossa havaitun käyttäytymisen.
- __Hankevaihtoehto__ (project alternative) on vaihtoehto, joka sisältää arvioitavan hankkeen.
- __Hyötyfunktio__ (utility function) kuvaa matemaattisesti vaihtoehdon houkuttelevuutta.
- __Iteraatio__ (iteration) on yksi kysyntälaskennan ja sijoittelun kierros.
- __Konnektori__ eli syöttölinkki (connector) on linkki, joka yhdistää sentroidin muuhun verkkoon.
- __Konvergenssi__ (convergence) tarkoittaa, että kysyntä ei enää muutu merkittävästi iteraatioiden välillä.
- __Lähtödata__ (base data) ovat lähtökysyntämatriisit, joita käytetään iteroinnin lähtökohtana.
- __Lähtökysyntä__ (base demand) on ensimmäisessä sijoittelussa käytetty kysyntä. Kun mallia käytetään oikein, tulokset eivät riipu lähtökysynnästä, mutta sopiva lähtökysyntä lyhentää ajoaikaa.
- __Linkki__ (link) on kahden verkon solmun välinen yhteys, esimerkiksi tieosuus.
- __Logit-malli__ (logit model) on tilastollinen malli, joka kuvaa vaihtoehdon valintatodennäköisyyttä kaikkien vaihtoehtojen hyötyjen funktiona.
- __Logsum__ on vaihtoehtojen eksponentoitujen hyötyjen summan logaritmi. Se yhdistää kaikkien vaihtoehtojen hyödyn yhdeksi luvuksi, ja sitä käytetään saavutettavuuden mittarina.
- __Malli__ (model) on matemaattinen kuvaus järjestelmästä, tässä Suomen liikkumisesta ja kuljetuksista.
- __Mallijärjestelmä__ (model system) on useiden mallien yhdistelmä, joka kuvaa monimutkaista kokonaisuutta.
- __OMX__ (Open Matrix) on VALMAssa matriiseille käytetty tiedostomuoto.
- __Osamalli__ (sub-model) on yksi VALMAn maantieteellisistä osista (`koko_suomi`, `uusimaa`, `lounais_suomi`, `ita_suomi`, `pohjois_suomi`), joilla kullakin on oma aluejakonsa ja verkkonsa.
- __Palvelutaso__ (level of service, LOS) kuvaa alueiden välisiä matka-aikoja, kustannuksia ja etäisyyksiä.
- __Parametri__ (parameter) on mallin muuttujan kerroin, joka määritetään estimoinnissa.
- __Pesitetty logit-malli__ (nested logit) on logit-mallin muunnelma, jossa toisiinsa korreloivat vaihtoehdot ryhmitellään samaan haaraan.
- __Pitkien matkojen malli__ (long-distance model) on henkilöliikenteen mallin osa, joka kattaa työasiamatkat, yön yli -matkat ja ulkomaanmatkat koko Suomessa.
- __Saavutettavuus__ (accessibility) kuvaa, kuinka helposti kohteet ovat saavutettavissa. VALMAssa saavutettavuutta mitataan yleensä logsumeilla.
- __Sentroidi__ (centroid) on sijoittelualuetta edustava solmu. Matkat alkavat ja päättyvät sentroideihin.
- __Sijoittelu__ (assignment) eli reitinvalinta on mallin vaihe, jossa kysyntä sijoitellaan verkolle. VALMA käyttää sijoitteluun OpenPaths EMMEä.
- __Sijoittelualue__ (zone) on mallin perusalueyksikkö. Jokaista sijoittelualuetta edustaa verkossa yksi sentroidi.
- __Sijoitteluluokka__ (assignment class) on yhdessä sijoiteltava kysynnän ryhmä, esimerkiksi polttomoottoriautot (`icev`) tai joukkoliikenne (`transit`).
- __Skenaario__ (scenario) on käyttöliittymässä malliajo: verkon, aluetietojen, hintadatan ja ajoasetusten yhdistelmä, joka tuottaa yhden tulosjoukon.
- __Solmu__ (node) on verkon piste, esimerkiksi risteys tai pysäkki.
- __Syöttöalue__ (input zone) on aluetietotiedoston alue. Syöttöalueet aggregoidaan kunkin osamallin sijoittelualueiksi tiedoston kohdistussarakkeiden avulla.
- __Tavaraliikenteen malli__ (freight model) on VALMAn osa, joka mallintaa tavarankuljetuksia hyödykeryhmittäin.
- __Toissijainen matkakohde__ (secondary destination) on kiertomatkan lisäpysähdys, esimerkiksi työpaikalta tehty työasiamatka.
- __Validointi__ (validation) tarkoittaa mallin tulosten vertaamista riippumattomaan havaintoaineistoon sen varmistamiseksi, että malli antaa oikeita tuloksia nykytilanteessa. Validoinnissa käytettyä aineistoa ei saa olla käytetty estimoinnissa.
- __Vastus__ (impedance) kuvaa matkan haittoja matkustajalle, kuten etäisyyttä, matka-aikaa ja kustannusta. Alueiden väliset vastukset tallennetaan palvelutasomatriiseihin.
- __Vertailuvaihtoehto__ (reference alternative) on vaihtoehto ilman hanketta, ja sitä käytetään vertailun pohjana.
- __Viivytysfunktio__ (volume-delay function) kuvaa, miten linkin matka-aika kasvaa liikennemäärän kasvaessa.
- __Yleistetty matkakustannus__ (generalised cost) yhdistää matkan matka-ajan, kustannuksen ja muut tekijät yhdeksi arvoksi.
