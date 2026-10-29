---
nav_order: 3
sort: 3
---

# EMME-verkon kuvaus
EMME-verkko kuvaa valtakunnallisen liikennemallijärjestelmän liikenneverkkoa. Verkko sisältää tie- ja katuverkon, joukkoliikennelinjastot, kävely- ja pyöräliikenteen yhteydet sekä tavaraliikenteen yhteydet. Verkkoa käytetään henkilö- ja tavaraliikenteen sijoitteluissa. Verkko muodostuu solmuista, linkeistä ja joukkoliikennelinjoista.

## Liikenneverkko

### Solmut

Solmut kuvaavat liikenneverkon risteyksiä, pysäkkejä, asemia ja sijoittelualueiden sentroideja. Solmut voidaan jakaa kahteen pääryhmään:
- liikenneverkon solmut
- sijoittelualueiden sentroidit

*Taulukko x. Solmuavaruuden jako, sentroidit*

| numeroavaruus | selitys |
|---------------|---------|
| 100 - 35 999      | sentroidit, Suomen sisäiset |
| 36 000 – 36 999 | sentroidit, Tornionjokilaakso (Ruotsi) |
| 37 000 – 50 099 | VAPAA |
| 50 100 - 50 199 | ulkomaan rajapaikat ja satamat |
| 50 200 - 59 999 | ulkomaan sentroidit (Eurooppa ja muu maailma) |
| 60 000 - 60 999 | ulkomaan sentroidit (Viro, Ruotsi, Norja, Tanska, Latvia) |
| 61 000 - 99 999 | VAPAA |

*Taulukko x. Solmuavaruuden jako, muut solmut kuin sentroidit*

| numeroavaruus | selitys |
|---------------|---------|
| 100 000 - 899 999    | käytetyt solmut |
| 900 000 - 999 999 | VAPAA |




*Taulukko x. Solmujen attribuuttitiedot*

| attribuutti      |       | selitys                                                      |
|------------------|-------|--------------------------------------------------------------|
| solmuattribuutti | ui1   | väliaikainen tieto, VAPAA               |
| solmuattribuutti | ui2   | VAPAA                                |
| solmuattribuutti | ui3   | VAPAA |
| network field | #municipality | Kunnan nimi |
| network field | #park_cost_n | Liityntäpysäköinnin hinta (e/h) |
| network field | #subarea | 1 = osamallialue, 2 = osamallin puskurivyöhyke, 3 = muu Suomi |
| network field | #transit_stop_b | Bussipysäkki |
| network field | #transit_stop_e | Kaukobussipysäkki |
| network field | #transit_stop_g | Runkobussipysäkki |
| network field | #transit_stop_p | Pikaratikkapysäkki |
| network field | #transit_stop_t | Ratikkapysäkki |

#### Sentroidit
Sentroidit edustavat liikennemallin sijoittelualueita. Sijoittelualueiden liikenne kytkeytyy varsinaiseen liikenneverkkoon sentroidien ja niitä ympäröivien konnektoreiden avulla.




### Kulkumuodot

EMMEssä kulkumuodot määrittävät, millä verkon linkeillä eri liikennemuodot voivat kulkea. Kulkumuotojen kuvauksessa on eroteltu tavaraliikenteen käyttämät kulkumuodot (isot kirjaimet) ja henkilöliikenteen käyttämät kulkumuodot (pienet kirjaimet).

Valtakunnallisessa liikennemallissa autoliikenteen pääkulkumuoto on h (auto). Kaikilla aux. auto -kulkumuotoa käyttävillä linkeillä on sallittava myös pääkulkumuoto h.

Joukkoliikenteen kulkumuodot (transit) määrittävät joukkoliikennelinjojen käyttämät linkit. Joukkoliikenteen apukulkumuodoilla (aux. transit) kuvataan esimerkiksi kävelyä pysäkeille ja vaihtoyhteyksiä linjojen välillä.



*Taulukko x. Kulkumuotojen (modes) kuvaus*

| **Kulkumuoto** | **Kuvaus** | **Tyyppi** 
|---|---|---|
| `h` | Pääkulkumuoto | auto |
| `c` | Henkilöauto | aux. auto |
| `v` | Pakettiauto | aux. auto |
| `k` | Kuorma-auto | aux. auto |
| `y` | Perävaunullinen kuorma-auto | aux. auto |
| `r` | Lähijuna | transit |
| `j` | Kaukojuna | transit |
| `t` | Raitiovaunu | transit |
| `p` | Pikaraitiovaunu | transit |
| `m` | Metro | transit |
| `b` | Linja-auto | transit |
| `g` | Runkobussi | transit |
| `e` | Pitkän matkan linja-auto | transit |
| `l` | Lentoliikenne | transit |
| `w` | Lautta | transit |
| `d` | Pitkän matkan lautta | transit |
| `a` | Kävely | aux. transit |
| `f` | Pyöräily | aux. transit |
| `u` | Liityntäpysäköinti | aux. transit |
| `D` | Dieseljuna | transit |
| `J` | Sähköjuna | transit |
| `W` | Kotimaan vesiliikenne | transit |
| `C` | Konttialus | transit |
| `G` | Yleinen rahtialus | transit |
| `L` | LNG-tankkeri | transit |
| `O` | Öljytankkeri | transit |
| `P` | Tuotetankkeri | transit |
| `R` | Ro-ro-alus | transit |
| `T` | Raakapuu syöttöliikenne | aux. transit |
| `F` | Tavaraliikenne syöttöliikenne| aux. transit |



### Linkit

*Taulukko x. Linkkien ominaisuudet*

| kenttä          | kuvaus                                                 |
|-----------------|--------------------------------------------------------------|
| id              | link identifier |
| i               | I-node of link |
| j               | J-node of link |
| type            | ks. taulukko x                                              |
| length          | linkin pituus                                                             |
| lanes           | kaistamäärä |
| modes           | kulkumuodot (taulukko x)                                                    |
| vdf             | sijoittelufunktion nro                                       |
| ul1 | linkin yhden kaistan kapasiteetti (ajon./h/kaista) |
| ul2             | linkin vapaa nopeus (km/h)                                         |
| ul3             | VAPAA  |
| @ferry_wait_time |  Lauttojen odotusaika                        |
| @toll_cost_vrk      | Tienkäyttömaksu VRK-ajanjaksolla |
| @freight_gate      |  Positiivinen (lähde) tai negatiivinen (kohde) sentroidin tunniste tavaraliikenteen kulun analysointia varten  |
| #buslane            | Tosi, jos linkillä on joukkoliikennekaista |
| #car_time_aht      | Ennalta määritetty auton matka-aika (AHT)    |
| #car_time_iht      |  Ennalta määritetty auton matka-aika (IHT)   |
| #car_time_it      |  Ennalta määritetty auton matka-aika (IT)   |
| #car_time_pt      | Ennalta määritetty auton matka-aika (PT)    |
| #car_time_vrk      |  Ennalta määritetty auton matka-aika (VRK)   |
| #dr_leveys      | Linkin leveys (Digiroad) |
| #dr_linkkityyp      | Linkin tyyppi (Digiroad) |
| #dr_nopeusrajoitus      | Linkin nopeusrajoitus (Digiroad) |
| #dr_toiminn_lk      | Linkin toiminnallinen luokka (Digiroad) |
| #extra_cost      | Ennalta määritetty lisäkustannus    |
| #hinta_vrk      | Hinta VRK-ajanjaksolla |
| #road_number      |  Tien numero valtion omistamilla teillä   |
| #road_part_nr_max      |  Suurin tienosan numero linkillä   |
| #road_part_nr_min      | Pienin tienosan numero linkillä    |
| #street_name      | Kadun nimi suomeksi    |
| #traffic_light      | Tosi, jos linkki on lähellä liikennevaloa    |



*Taulukko 9. Linkkityypit (link type)*

| linkkityyppi (link type) | selitys                                                                      |
|--------------------------|------------------------------------------------------------------------------|
| 2       | ratikka                                                                                       |
| 3       | metro                                                                                         |
| 4       | juna                                                                                         |
| 7       | lento                                                                    |
| 99      | syöttölinkki                                                                                  | |
| 101–141 | jalankulku, pyöräily, autot, bussit                               |
| 144 | autolautta                         |


#### Syöttölinkit
Syöttölinkeillä (linkkityyppi 99) sentroidit yhdistetään ympäröivään verkkoon. Jokaisesta sentroidista on olemassa yksi autoliikenteen ja yksi kävely- ja pyöräliikenteen syöttölinkki lähimpiin solmuihin. Autoliikenteen syöttölinkkiä ei saa yhdistää moottoritiehen, ramppeihin, liikenneympyröihin tai kaksiajorataisiin katuihin/teihin.


*Taulukko x. Sijoittelufunktioiden jako väylätyyppeihin*

| Linkkityyppi | Kuvaus | Toiminnallinen luokka | Nopeusrajoitus (km/h) | Tien leveys | Viivytysfunktio (vdf) | Kaistakapasiteetti (ul1) (ajon./h/kaista) | Vapaa nopeus (ul2) (km/h) |
|---|---|---|---|---|---|---|---|
| 101 | moottoritie | 1 | 120 | | 1 | 2100 | 113 |
| 103 | moottoritie, kaistoja ≥3 | 1| 120 | | 1 | 1900 | 113 |
| 104 | moottoritie |1 | 100 | | 1 | 2000 | 97 |
| 105 | moottoritie, kaistoja ≥3 | 1| 100 | | 1 | 1800 | 97 |
| 106 | moottoritie | 1| 80 | | 1 | 2000 | 81 |
| 107 | moottoritie, kaistoja ≥3 |1 | 80 | | 1 | 1800 | 81 |
| 116 | ramppi |1-4 | 60–120 | | 2 | 1600 | 63 |
| 125 | ramppi |1-4 | 50 | | 4 | 1150 | 48 |
| 128 | ramppi |1-4 | 20–40 | | 4 | 1000 | 41 |
| 108 | valtatie | 1 | 100 | | 2 | 1900 | 97 |
| 110 | valtatie | 1 | 90 | | 2 | 1900 | 90 |
| 112 | valtatie | 1 | 80 | | 2 | 1850 | 81 |
| 114 | valtatie | 1 | 70 | | 2 | 1600 | 73 |
| 116 | valtatie | 1 | 60 | | 2 | 1600 | 63 |
| 109 | kantatie, seututie, yhdystie | 2-4 | 100 | | 2 | 1700 | 97 |
| 111 | kantatie, seututie, yhdystie | 2-4 | 90 | | 2 | 1700 | 90 |
| 113 | kantatie, seututie, yhdystie | 2-3 | 80 | ≥6m | 2 | 1650 | 81 |
| 114 | kantatie, seututie, yhdystie | 4 | 80 | ≥6m | 2 | 1600 | 73 |
| 115 | kantatie, seututie, yhdystie | 2-3 | 80 | <6m | 2 | 1500 | 73 |
| 117 | kantatie, seututie, yhdystie | 4 | 80 | <6m | 2 | 1400 | 63 |
| 115 | kantatie, seututie, yhdystie | 2-4 | 70 | | 2 | 1500 | 73 |
| 117 | kantatie, seututie, yhdystie | 2-3 | 60 | ≥6m | 2 | 1400 | 63 |
| 121 | kantatie, seututie, yhdystie | 4 | 60 | ≥6m | 3 | 1200 | 58 |
| 124 | kantatie, seututie, yhdystie | 2-4 | 60 | <6m | 3 | 1100 | 63 |
| 122 | yksityistie | 5 | 100 | | 3 | 1100 | 73 |
| 122 | yksityistie | 5 | 90 | | 3 | 1100 | 73 |
| 122 | yksityistie | 5 | 80 | ≥6m | 3 | 1100 | 73 |
| 124 | yksityistie | 5 | 80 | <6m | 3 | 1100 | 63 |
| 124 | yksityistie | 5 | 70 | | 3 | 1100 | 63 |
| 124 | yksityistie | 5 | 60 | ≥6m | 3 | 1100 | 63 |
| 126 | yksityistie | 5 | 60 | <6m | 4 | 1050 | 48 |
| 125 | valtatie | 1 | 50 | | 4 | 1150 | 48 |
| 128 | valtatie | 1 | 40 | | 4 | 1000 | 41 |
| 135 | valtatie | 1 | 30 | | 5 | 700 | 30 |
| 139 | valtatie | 1 | 20 | | 5 | 700 | 20 |
| 126 | kantatie, seututie, yhdystie |2-3 | 50 | | 4 | 1050 | 48 |
| 127 | kantatie, seututie, yhdystie |4 | 50 | | 4 | 1000 | 44 |
| 129 | kantatie, seututie, yhdystie |2-3 | 40 | | 4 | 900 | 41 |
| 133 | kantatie, seututie, yhdystie |4 | 40 | | 5 | 750 | 36 |
| 136 | kantatie, seututie, yhdystie |2-3 | 30 | | 5 | 600 | 25 |
| 137 | kantatie, seututie, yhdystie |4 | 30 | | 5 | 550 | 20 |
| 140 | kantatie, seututie, yhdystie |2-4 | 20 | | 5 | 600 | 15 |
| 133 | yksityistie |5 | 50 | | 5 | 750 | 36 |
| 134 | yksityistie |5 | 40 | | 5 | 600 | 36 |
| 138 | yksityistie |5 | 30 | | 5 | 500 | 18 |
| 141 | yksityistie |5 | 20 | | 5 | 500 | 12 |

### Tie- ja katuverkon koodausperiaatteet

Aluesyötöt yhdistetään lähimpään solmuun, joka on saavutettavissa ajoneuvoilla. Solmusta täytyy lähteä linkki, joka on tyyppiä "Yksiajorataisen tien osa". Toisin sanoen autoliikenteen syöttölinkkiä ei yhdistetä moottoritiehen, ramppeihin, liikenneympyriin tai kaksiajorataisiin katuihin/teihin.
Jokaisesta centroidista tehdään lisäksi yksi kävelylinkkisyöttö vastakkaiseen suunnan lähimpään solmuun. Tämän solmun täytyy olla aluetta kuvaavan polygonin sisällä.

Jokaisen malliajon yhteydessä linkkien ul1 (kapasiteetti), ul2 (vapaa nopeus) ja vdf (viivytysfunktio) -arvot ylikirjoitetaan linkkityypin perusteella, joten niitä ei tarvitse määritellä erikseen linkeille. 

Eritasoliittymien erkanemis- ja liittymiskaistoja ei lähtökohtaisesti ole huomioitu kaistamäärissä. Jos liittymis- ja erkanemiskaistat ulottuvat toisiinsa asti kattaen kahden eritasoliittymän välisen matkan kokonaan, ne on otettu huomioon kaistamäärässä.

Tasoliittymien kääntymiskaistoja ei ole lähtökohtaisesti huomioitu, vaan kaistamäärä on kuvattu pääsuunnan liittymän läpi kulkevien kaistojen määrän perusteella. Tilanteessa, jossa kääntymiskaista ulottuu yli viereisen liittymän siten, että kääntymiskaistan vuoksi seuraavassa liittymässä on useampi läpi kulkeva kaista, kääntymiskaista on huomioitu myös liittymien välisellä osuudella. 

Joukkoliikennekaistat on laskettu mukaan kaistamäärään ja näistä on tieto omassa attribuutissa. Joukkoliikennekaistat huomioidaan mallijärjestelmässä viivytysfunktioissa.

## Joukkoliikenne

### Joukkoliikenteen ajoneuvotyypit

*Taulukko x. Joukkoliikenteen ajoneuvotyypit, niitä vastaavat kulkumuodot ja kuvaus.

| Ajoneuvotyyppi (vehicle) | Kuvaus | Kulkumuoto (mode) |
|---|---|---|
| 1 | Linja-auto | `b` |
| 2 | Raitiovaunu | `t` |
| 3 | Juna | `j` |
| 4 | Metro | `m` |
| 5 | Lautta | `w` |
| 6 | Lentokone | `l` |
| 7 | Pikaraitiovaunu | `p` |
| 8 | Pitkän matkan linja-auto | `e` |
| 9 | Lähijuna | `r` |
| 10 | Runkobussi | `g` |
| 11 | VR:n lähijuna | `j` |
| 12 | Kiskobussi | `j` |
| 13 | Pitkän matkan yölautta | `d` |
| 14 | Pitkän matkan päivälautta | `d` |
| 20 | Kotimaan vesialus | `W` |
| 23 | Konttialus | `C` |
| 24 | Yleinen rahtialus | `G` |
| 25 | LNG-tankkeri | `L` |
| 26 | Öljytankkeri | `O` |
| 27 | Tuotetankkeri | `P` |
| 28 | Ro-ro-alus | `R` |
| 30 | Tavarajuna, diesel | `D` |
| 31 | Tavarajuna, sähkö | `J` |

### Joukkoliikennelinjojen pysähtymiskäyttäytyminen
Joukkoliikennelinjoilla on linja-attribuutti `#keep_stops`, jolla määritetään, miten linjan pysähtymiskäyttäytyminen määräytyy.

- **`#keep_stops = 1`:** Linja säilyttää alkuperäisen pysähtymiskäyttäytymisensä. Pysähtyminen määräytyy noodien kulkumuotokohtaisten attribuuttien `#transit_stop_b`, `#transit_stop_e`, `#transit_stop_g`, `#transit_stop_p` ja `#transit_stop_t` perusteella.
- **`#keep_stops = 0`:** Linja pysähtyy niillä pysäkeillä, jotka on määritetty pysäkkisegmenteille (attribuutit noali ja noboa).

Attribuutti `#keep_stops` koskee vain seuraavia kulkumuotoja: `b` (bussi), `e` (kaukobussi), `g` (runkobussi), `p` (pikaratikka) ja `t` (ratikka).

### Joukkoliikennelinjastot

Samalla joukkoliikennelinjalla ei pystytä kuvaamaan eri hintafunktioita yksinkertaisesti EMME-mallissa. Tämä on ongelma seudullisilla junilla, joita voi käyttää paikallisen toimivaltaisen viranomaisen lipuilla (HSL, NYSSE), mutta alueen ulkopuolella tarvitaan VR:n lippu. Tästä johtuen HSL:n ja NYSSE:n alueelle päättyvät R, T, Z, M ja D-junat on lisätty malliin tuplana: Toisella linjalla nousut/poistumiset on kielletty HSL/NYSSE-alueella siten, että linjaa voi käyttää vain seuturajat ylittävään matkaan. Toinen linja on katkaistu seudun sisälle, jolloin sitä käytetään vain seudun sisäisiin matkoihin. Näille linjoille on eri hintafunktiot. Tässä on hyödynnetty custom transit lines –ominaisuutta. 

*Taulukko x. Joukkoliikennelinjan perusattribuutit*

| attribuutti | kuvaus |
|---|---|
| `line` | Linjan yksilöivä tunnus. |
| `mode` | Linjan kulkumuoto, esim. `b`, `e`, `g`, `p` tai `t`. |
| `vehicle` | Ajoneuvotyyppi |
| `description` | Linjan kuvaus |
| `ut1` | Joukkoliikennelinjan hinta-id |
| `ut2` | VAPAA |
| `ut3` | VAPAA |
| `#agency_name` | Operaattorin nimi |
| `#departures_per_day` | Vuorojen määrä per vrk |
| `#hdw_aht` | Vuoroväli aamuhuipputunnissa (klo 6-9) |
| `#hdw_iht` | Vuoroväli iltahuipputunnissa (klo 15-18) |
| `#hdw_it` | Vuoroväli iltatunnissa (klo 18-21) |
| `#hdw_pt` | Vuoroväli päivätunnissa (klo 9-15) |
| `#hdw_vrk` | Vuorokauden keskimääräinen vuoroväli |
| `#keep_stops` | 1 = Linja säilyttää alkuperäisen pysähtymiskäyttäytymisensä. |
| `#route_short_name` | Route short name (GTFS) |
| `#trip_short_name` | Trip short name (GTFS) |

*Taulukko x. Joukkoliikennesegmenttien perusattribuutit*

| attribuutti | kuvaus |
|---|---|
| `line` | Joukkoliikennelinja |
| `i` | Segmentin I-solmu |
| `j` | Segmentin J-solmu |
| `dwt` | Pysähdyksen kesto |
| `noali` | Ei poistumista I-solmusta |
| `noboa` | Ei nousemista I-solmusta |
| `ttf` | Joukkoliikenteen matka-aikafunktio (määrittyy malliajon aikana automaattisesti) |
| `us1` | Matka-aika pysäkkien välillä (min) |
| `us2` | VAPAA |
| `us3` | VAPAA |


## Tavaraliikenne
Tavara- ja henkilöliikenteen verkot ovat pääosin yhteisiä ja ne on tehty mallissa samaan verkkokuvaukseen/skenaarioon. Prosessilla on mahdollista tuottaa myös pelkästään henkilöliikennettä koskeva kuvaus. Tavaraliikenteen kuvaus hyödyntää muutamia täydentäviä tietolähteitä raiteista ja vesiväylistä ja tietyt terminaalit/lastauspaikat ovat vaatineet erityiskäsittelyä verkossa. 

Rautatie- ja vesiväylien sijoittelu- ja vastuslaskennan periaatteena on EMME:n joukkoliikennepohjainen sijoittelu. Jokaista vesiväylä- ja raidelinkkiä kohden on tehty "joukkoliikennelinja", jolla kuljetukset tapahtuvat. 

Rautatieverkolle on liitetty tieto, kulkeeko siinä tavaraliikennettä vai ei. Lisäksi on tiedot raiteiden sähköistyksestä sekä tavaraliikenteen keskimääräisestä kuljetusnopeudesta. Tieto rataosien sähköistyksestä pohjautuu Väyläviraston Rautateiden verkkoselostukseen 2026. Tavaraliikenteen keskimääräinen kuljetusnopeus perustuu todellisiin kuljetustietoihin. Kuljetukset kuvataan kahdella kulkumuodolla, dieseljunalla ja sähköllä kulkevalla junalla. Liikennepaikoille on merkitty käsin tieto, käytetäänkö paikkaa raakapuun, muun tavaran vai molempien lastaukseen. Liikennepaikkatieto pohjautuu rataverkkoselostukseen. Näille paikoille on tehty linkit, joissa kuorma-auton liittyminen asemaan on mahdollista. Muiden kuin valtion omistuksessa olevat rataverkon osat (teollisuusraiteet) ja niillä sijaitsevat liikennepaikat kuvattu verkkoon erikseen suurimpien teollisuuslaitosten osalta.

Satamat yhdistyvät aina vesiväyliin ja niiden osalta, joihin on merkitty tieto yhdistymisestä raiteisiin, on luotu lähimpään rautatiesolmuun yhdistävä linkki.

Verkolle on muodostettu myös @freight_gate attribuutti, joka kertoo satamiin ja raiteisiin johtavan kuorma-autolinkin lähimmän aluesyötön id:n. Tämä attribuutti palvelee kuorma-autolla tehtävien osamatkojen tallennusta matriisimuotoiseksi sijoittelun yhteydessä. Attribuuttia käytetään EMME:n traversal matrix työkalussa.

Digiroadin ajoneuvon suurin sallittu pituus ja suurin sallittu massa -kenttiä on hyödynnetty raskaan liikenteen rajoitusten kuvaamisessa. Jos linkillä ajoneuvon suurin sallittu pituus on vähintään 22 metriä tai massarajoitus 42 000 kg, on sen käyttö kielletty yhdistelmäajoneuvoilta. Jos ajoneuvon suurin sallittu pituus on 6 metriä tai massarajoitus 8000 kg, on linkeillä lisäksi kielletty kuorma-autot.

Tiekuljetukset voivat käyttää pääosin kaikkea tieverkkoa. Suurten kaupunkien keskusta-alueille on kuitenkin kuvattu raskaiden ajoneuvojen rajoituksia. Kattavaa tietoa rajoituksista ei ole. Rajoituksia voidaan jatkossa kuvata myös muille, nyt rajoittamattomille alueille tai yksittäisille tienkohdille. Rajoitukset on kuvattu siten, että rajoitusalueen läpi ei pääse ajamaan, mutta jokaiselle osa-alueelle pääsee yhtä reittiä myös eri ajoneuvoluokkien raskailla ajoneuvoilla.

