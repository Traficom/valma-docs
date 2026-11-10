# **Kustannustiedoston tulkinta tavaraliikenteen mallissa**
Tavaraliikenteen kuljetuskustannusten kustannusfunktioiden komponentit löytyvät mallin lähtötietona json-tiedostosta. Samaan tiedostoon sisältyy sekä henkilöliikenteen- että tavaraliikenteen yksikkökustannukset. Tässä tiedostossa käydään läpi kustannustiedoston (json) sisältöä ja tiedostosta löytyviä tavaraliikennemallin kuljetuskustannusten laskentaan vaikuttavia yksikkökustannuksia/kustannuskomponentteja. 

Huomionarvoista on, että tiedoston kustannuskomponentit vastaavat muuten kappaleissa tavaraliikennemallin dokumentaatiossa esitettyjä yksikkökustannuksia, mutta hallintokulujen kerroin ei ole mukana tieliikenteen kustannuksissa, vaan se huomioidaan vasta mallijärjestelmän laskennassa.

Kustannustiedostoon sisältyvien tavararyhmien (12 tavararyhmää = estimointiryhmittely) selitteet löytyvät taulukosta 1. 


*Taulukko 1. Kustannustiedostosta löytyvät tavararyhmien (estimointiryhmittely) selitteet*
| Tavararyhmän lyhenne | Tavararyhmän selite |
|---------------|---------|
| mameka      | Maatalous, metsästys ja kalastus |
| metsat | Metsätalous |
| energy | Kivihiili, raakaöljy, maakaasu, turve, koksi, briketit |
| kaivan | Kaivannaiset, raakamineraalit sekä ei-metalliset mineraalituotteet |
| elint | Elintarvikkeet |
| tekst | Tekstiilit, kankaat ja nahat |
| puukor | Puu- ja korkkituotteet |
| papsel | Paperi, kartonki, sellu |
| oljytu | Jalostetut öljytuotteet |
| kemiat | Metallit, koneet ja laitteet |
| jate | Jätteet |

Tiedostoon sisältyvien kuljetusmuotojen ja -tyyppien mallissa käytetyt nimet ja selitteet löytyvät taulukoista 2-4.


*Taulukko 2. Kustannustiedostosta löytyvät ajoneuvoluokat tieliikenteelle*
| Ajoneuvoluokka | Nimi kustannustiedostossa |
|---------------|---------|
| Kuorma-auto, N2 (<12t)  | truck_2n |
| Kuorma-auto, KAIP (12 t - ~40t) | truck |
| Puoliperävaunuyhdist. KAPP (~40t) | semi_trailer |
| Täysperävaunuyhdist, KATP (<64t) | trailer-truck |
| HCT-rekka, HCT (<76t)  | trailer_truck_76t |


*Taulukko 3. Kustannustiedostosta löytyvät ajoneuvoluokat rautatieliikenteelle*
| Ajoneuvoluokka | Nimi kustannustiedostossa |
|---------------|---------|
| Sähköjuna | freight_train_J |
| Dieseljuna | freight_train_D |


*Taulukko 4. Kustannustiedostosta löytyvät ajoneuvoluokat alusliikenteelle*
| Ajoneuvoluokka | Nimi kustannustiedostossa |
|---------------|---------|
| Konttilaiva | container_ship |
| RoRo / RoPax | roro_vessel |
| Kuivalasti / irtolasti | general_cargo |
| Öljytankkeri | oil_tanker |
| Tuotesäiliölaiva | product_tanker |
| LNG säiliölaiva | lng_carrier |
| Kotimaan laivaliikenne | ship_W |


Kustannustiedoston parametrit muuttuvat ennustevuoden mukaan. Esimerkiksi käyttövoiman hinta muuttuu ennustettavan vuoden mukaan ja sähköautojen osuus kannassa samaten. ***Eri ennustevuosille tarvitaan näin ollen erilliset kustannustiedostot.*** 

## **Kotimaan mallin kuljetuskustannusfunktioiden yksikköarvot tiedostossa**

Yksikköarvojen/kustannuskomponenttien sisältöä on avattu tarkemmin tavraliikennemallin dokumentaatiossa luvussa 3.4. Tieliikenteen kustannuskomponentit luodaan yhdistelemällä kustannustiedostosta löytyviä yksikkökustannuksia. ***Kaikki tarvittava yhdistely tehdään automaattisesti mallijärjestelmässä (eikä käyttäjän tarvitse miettiä sitä erikseen). Kun kustannuksia muutetaan tarkasteluissa, on käyttäjän kuitenkin hyvä ymmärtää, miten laskenta toimii.***  

### **Tiekuljetusten kustannukset (kotimaa)**

#### **Tiekuljetusten terminaalikustannus**
Löytyy json-tiedoston polusta:

"freight" -> *tavararyhmä* -> "truck" -> "param" -> "terminal_cost" 

Kustannuksen yksikkö on €/t.

#### **Tiekuljetusten kilometriperusteinen liikennöintikustannus**

Löytyy json tiedoston avaimesta:

"vehicle_km_cost" 

Avaimesta löytyy niin tavaraliikenteen yksikkökustannusten lisäksi henkilöliikenteenteen mallissa käytettäviä kustannuksia. Tavaraliikenteen malliin tällä hetkellä tarvittavat kustannuskomponentit löytyvät ajoneuvoluokista "truck" (polttomoottori KAIP), "truck_ev" (sähköinen KAIP), "semi_trailer" (poltto-moottori KAPP), "semi_trailer_ev" (sähköinen KAPP), "trailer_truck"(polttomoottori KATP) ja "trailer_truck_ev"(sähköinen KATP) . Muita "vehicle_km_cost" avaimesta löytyviä parametreja/ajoneuvoluokkia ei käytetä tavaraliikenteen mallissa tällä hetkellä. Ne liittyvät henkilöliikenteen malliin.

Kilometrikustannus painottuu jokaisen ajoneuvoluokan osalta luokan sähköistymisen mukaan. Ajoneuvoluokan käyttövoimittainen jakautuminen suhteessa koko tavaraliikenteen ajoneuvokantaan löytyy polusta: 

"freight" -> *tavararyhmä* -> "truck" -> "fleet" -> *ajoneuvoluokka* 

Avaimesta löytyvä "domestic_distribution"-parametri kuvaa ajoneuvoluokan liikennöinnin osuutta kaikesta kotimaan liikennöinnistä tonnikilometreinä mitattuna. "foreign_distribution" puolestaan tarkoittaa ajoneuvoluokan osuutta kaikesta ulkomaan tavaraliikenteen liikennöinnistä tonnikilometreissä mitattuna. Domestic_distribution - parametri on ajoneuvokantamallin tulos, joka toimii syötteenä tavaraliikennemallin kustannuslaskentaan. Foreign_distribution - parametri pysyy kiinteänä ennusteissa (kuljetustilastoista laskettu), mutta ryhmien sisäistä käyttövoimien osuutta varioidaan kotimaan jakauman mukaisesti.  

Jos haluaa laskea esim. KAIP (truck)- ryhmän kotimaan kilometrikustannuksen, muodostetaan se laskelmalla "truck_ev" (sähkö KAIP) - ja "truck" (polttomoottori KAIP) - ajoneuvoluokan kilometrikustannuksen keskiarvo painotettuna kunkin luokan domestic_distribution osuudella. Niissä tavaralajeissa, joissa ajoneuvokantamallista kysyntää kohdistuu myös N2-luokan ajoneuvoille, tulee KAIP (truck), ryhmän laskennan painotuksessa huomioida myös nämä ryhmät: "truck_2n" ja "truck_2n_ev". Mikäli kaikki KAIP-suorite on allokoitu N3-luokan (truck) ajoneuvoille, ei N2-luokan ajoneuvojen hintatietoja löydy.  Samaan tapaan KATP kustannuslaskennassa tulee huomioida "trailer_truck" - luokkien lisäksi "trailer_truck_76" - ryhmien sähköpainotukset. Painotettu keskiarvo kuvaa ryhmän kustannusta (€/km) mallin mukaisessa käyttövoimajakaumassa.

Liikennöintikustannus kerrotaan vielä tavararyhmäkohtaisella (1+) tyhänäajon kertoimella, joka löytyy polusta:

"freight" -> *tavaryhmä* -> "truck" -> "empty_share"

Tämän jälkeen kustannus jaetaan vielä tavararyhmäkohtaisella keskikuormituksella, joka löytyy polusta:

"freight" -> *tavararyhmä* -> "truck" -> "param" -> "avg_load"

Näin saadaan kustannus, joka on muodossa €/t/km. Myöhemmin se kerrotaan matkan pituudella (automatkan pituus liikenneverkolta laskettuna) ja saadaan kustannus muodossa €/t.

#### **-	Tiekuljetusten aikaperusteinen liikennöintikustannus**

Löytyy json tiedoston avaimesta:

"vehicle_hour_cost"

Avaimesta löytyvistä ajoneuvoluokkien parametreista käytetään samoja ajoneuvoluokkia kuin kilometriperusteisten liikennöintikustannusten yhteydessä (ks. yllä).

Aikaperusteiset kustannukset painottuvat samalla tavalla sähköön ja poltto-moottoriliikennöintiin "domestic_distribution"- parametrin (kotimaan mallissa) mukaan kuin kilometrikustannus ja ne kerrotaan samaan tapaan tyhänäajon kertoimella kuin kilometriperusteiset kustannukset (ks. yllä). 
€/t/min-muotoinen kustannus saadaan jakamalla tuntikustannus tavararyhmittäisellä keskikuormituksella samalla tavalla kuin kilometrikustannuksen laskennan yhteydessä (ks. yllä). *Aikakustannukset on raportoitu minuuteissa, koska sijoitteluohjelma (EMME) toimii minuuttipohjaisesti.*  

### **Rautaiekuljetusten kustannukset (kotimaa)**

#### **Rautaiekuljetusten terminaalikustannus**

Löytyy json-tiedoston polusta:

"freight" -> *tavararyhmä* -> "freight_train" -> "num_terminals"_*junatyyppi*

Terminaalikustannus eroaa junatyyppien välillä. "num_terminals_J" tarkoittaa sähköjunan terminaalikustannusta ja "num_terminals_D" tarkoittaa dieseljunan terminaalikustannusta. Lyhenteet J ja D tulevat taulukosta 3. Kustannukset eriteltynä muodossa €/t.

#### **Rautatiekuljetusten kilometriperusteinen liikennöintikustannus**

Löytyy json-tiedoston polusta:

"freight" -> *tavararyhmä* -> "freight_train" -> "dist_"*junatyyppi*

Kilometrikustannus eroaa junatyyppien välillä. "dist_J" tarkoittaa sähköjunan kilometrikustannusta ja "dist_D" tarkoittaa dieseljunan kilometrikustannusta. Lyhenteet J ja D tulevat taulukosta 3. Kustannukset eriteltynä muodossa €/t/km. Myöhemmin se kerrotaan matkan pituudella (junamatkan pituus liikenneverkolta laskettuna) ja saadaan kustannus muodossa €/t.

#### **Rautatiekuljetusten aikaperusteinen liikennöintikustannus**

Löytyy json-tiedoston polusta:

"freight" -> *tavararyhmä* -> "freight_train" -> "time_"*junatyyppi*

Kilometrikustannus eroaa junatyyppien välillä. "time_J" tarkoittaa sähköjunan aikakustannusta ja "time_D" tarkoittaa dieseljunan aikakustannusta. Lyhenteet J ja D tulevat taulukosta 3. Kustannukset eriteltynä muodossa €/t/min. Myöhemmin se kerrotaan matka-ajalla (junamatkan aika liikenneverkolta laskettuna) ja saadaan kustannus muodossa €/t.

### **Aluskuljetusten kustannukset (kotimaa)**

Kotimaan alusliikenteessä on valittavana vain yksi alustyyppi (W) tavararyhmäkohtaisesti taulukon 4 mukaisesti. Jokaiselle tavararyhmälle on määritetty edustava laivatyyppi - syväys kombinaatio, jolla tavararyhmää kotimaan liikenteessä kuljetetaan. Taulukko kotimaan laivaliikenteessä edustavasta laivatyyppisyväys kombinaatiosta tavararyhmittäin löytyy alta.


*Taulukko 5. Kotimaan laivaliikenteessä edustava laivatyyppi-syväys kombinaatio tavararyhmittäin.*
| Tavararyhmä | Alustyyppi | Syväys |
|---------------|---------|---------|
| mameka | Kuivalasti / irtolasti | 4 m |
| metsat | Kuivalasti / irtolasti | 4 m |
| energy | Kuivalasti / irtolasti | 4 m |
| kaivan | Kuivalasti / irtolasti | 4 m |
| elint | RoRo / RoPax | 4 m |
| tekst | RoRo / RoPax | 4 m |
| puukor | Kuivalasti / irtolasti | 4 m |
| papsel | Kuivalasti / irtolasti | 4 m |
| oljytu | Tuotesäiliölaiva | 5 m |
| kemiat | Kuivalasti / irtolasti | 4 m |
| metkot | RoRo / RoPax | 4 m |
| jate | Kuivalasti / irtolasti | 4 m |

#### **Aluskuljetusten terminaalikustannus**

Löytyy json-tiedoston polusta:

"freight" -> *tavararyhmä* -> "ship" -> "num_terminals_W"

Kustannukset eriteltynä muodossa €/t.

#### **Aluskuljetusten kilometriperusteinen liikennöintikustannus**

Löytyy json-tiedoston polusta:

"freight" -> *tavararyhmä* -> "ship" -> "dist_W"

Kustannukset eriteltynä muodossa €/t/km. Myöhemmin se kerrotaan matkan pituudella (laivamatkan pituus liikenneverkolta laskettuna) ja saadaan kustannus muodossa €/t.

#### **Aluskuljetusten aikaperusteinen liikennöintikustannus**

Löytyy json-tiedoston polusta:

"freight" -> *tavararyhmä* -> "ship" -> "time_W"

Kustannukset eriteltynä muodossa €/t/min. Myöhemmin se kerrotaan matka-ajalla (laivamatkan aika liikenneverkolta laskettuna) ja saadaan kustannus muodossa €/t.

## **Ulkomaan mallin kuljetuskustannusfunktioiden yksikköarvot tiedostossa**

Ulkomaan mallin kustannuksia lasketaan vain ulkomailla ajettavan osuuden osalta. Kotimaan osuudessa kuljetustapavalinnat jakaantuvat kunkin alueparin välillä kotimaan mallin kyseisen hyödykeryhmän kuljetustapajaon mukaisesti. 

### **Tiekuljetusten kustannukset (ulkomaa)**

#### **Tiekuljetusten terminaalikustannus**

Käyttää samaa terminaalikustannusta kuin kotimaan liikennöinnissä (ks. yllä)

#### **Tiekuljetusten kilometriperusteinen liikennöintikustannus**

Muodostuu täysin samalla tavalla kuin kotimainen kilometriperusteinen liiken-nöintikustannus, mutta jakaantuminen eri käyttövoimiin menee "foreign_distribution"-parametrin mukaan. "foreign_distribution"-parametri löytyy samasta json-polusta kuin "domestic_distribution" (ks. kotimaan liikenteen vastaava kappale yllä).

#### **Tiekuljetusten aikaperusteinen liikennöintikustannus**

Muodostuu täysin samalla tavalla kuin kotimainen aikaperusteinen liikennöintikustannus, mutta jakaantuminen eri käyttövoimiin menee "foreign_distribution"-parametrin mu-kaan. "foreign_distribution"-parametri löytyy samasta json-polusta kuin "do-mestic_distribution" (ks. kotimaan liikenteen vastaava kappale yllä).

### **Rautatiekuljetusten kustannukset (ulkomaa)**

Kaikki rautatiekuljetusten kustannukset muodostuvat samalla tavalla ulkomaan mallissa kuin kotimaassa. Katso kotimaan vastaava kappale.

### **Aluskuljetusten kustannukset (ulkomaa)**

Ulkomaanliikenteessä kaikki tavararyhmälle määritetyt laivatyypit ja syväykset ovat mahdollisia. Kustannus-json sisältää ainoastaan ne tavararyhmä-laivatyyppi-syväys kombinaatiot, jotka mielletään mahdollisiksi kuljetusvaihtoehdoiksi. 

#### **Aluskuljetusten terminaalikustannus**

Löytyy json-tiedoston polusta:

"freight" -> *tavararyhmä* -> "foreign_ship" -> *alustyyppi* -> *syväys* -> "terminal_cost"

Kustannukset eriteltynä muodossa €/t.

#### **Aluskuljetusten kilometriperusteinen liikennöintikustannus**

Löytyy json-tiedoston polusta:

"freight" -> *tavararyhmä* -> "foreign_ship" -> *alustyyppi* -> *syväys* -> "dist"

Kustannukset eriteltynä muodossa €/t/km. Myöhemmin se kerrotaan matkan pituudella (laivamatkan pituus liikenneverkolta laskettuna) ja saadaan kustan-nus muodossa €/t.

#### **Aluskuljetusten aikaperusteinen liikennöintikustannus**

Löytyy json-tiedoston polusta:

"freight" -> *tavararyhmä* -> "foreign_ship" -> *alustyyppi* -> *syväys*  "time"

Kustannukset eriteltynä muodossa €/t/min. Myöhemmin se kerrotaan matka-ajalla (laivamatkan aika liikenneverkolta laskettuna) ja saadaan kustannus muodossa €/t.






