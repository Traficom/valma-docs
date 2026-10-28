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

*Taulukko x. Solmujen attribuuttitiedot*

| attribuutti      |       | selitys                                                      |
|------------------|-------|--------------------------------------------------------------|
| solmuattribuutti | ui1   | 1 = important                                    |
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

Pääkulkumuodon (auto) h on oltava linkillä sallittu.

*Taulukko x. Kulkumuotojen (modes) kuvaus*

| **Kulkumuoto** | **Kuvaus** |
|---|---|
| `c` | Henkilöauto |
| `v` | Pakettiauto |
| `k` | Kuorma-auto |
| `y` | Perävaunullinen kuorma-auto |
| `r` | Lähijuna |
| `j` | Kaukojuna |
| `t` | Raitiovaunu |
| `p` | Pikaraitiovaunu |
| `m` | Metro |
| `b` | Linja-auto |
| `g` | Runkobussi |
| `e` | Pitkän matkan linja-auto |
| `a` | Kävely |
| `f` | Pyöräily |
| `l` | Lentoliikenne |
| `w` | Lautta |
| `d` | Pitkän matkan lautta |
| `D` | Dieseljuna |
| `J` | Sähköjuna |
| `W` | Kotimaan vesiliikenne |
| `C` | Konttialus |
| `G` | Yleinen rahtialus |
| `L` | LNG-tankkeri |
| `O` | Öljytankkeri |
| `P` | Tuotetankkeri |
| `R` | Ro-ro-alus |
| `T` | Raakapuu syöttöliikenne |
| `F` | Tavaraliikenne syöttöliikenne|
| `u` | Liityntäpysäköinti |
| `h` | Pääkulkumuoto |



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
| ul1 | linkin yhden kaistan kapasiteetti |
| ul2             | linkin vapaa nopeus                                          |
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

Joukkoliikennekaistat on laskettu mukaan kaistamäärään ja näistä on tieto omassa attribuutissa. Joukkoliikennekaistat huomioidaan mallijärjestelmässä viivytysfunktioissa.

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
| Linkkityyppi | Kuvaus | Viivytysfunktio (vdf) | Kaistakapasiteetti (ul1) (ajon./h/kaista) | Vapaa nopeus (ul2) (km/h) | Nopeusrajoitus (km/h) |
|---:|---|:---:|---:|---:|---:|
| 101 | moottoritie | 1 | 2100 | 113 | 120 |
| 102 | moottoritie | 1 | 2100 | 113 | 120 |
| 103 | moottoritie, kaistoja ≥3 | 1 | 1900 | 113 | 120 |
| 104 | moottoritie | 1 | 2000 | 97 | 100 |
| 105 | moottoritie, kaistoja ≥3 | 1 | 1800 | 97 | 100 |
| 106 | moottoritie | 1 | 2000 | 81 | 80 |
| 107 | moottoritie, kaistoja ≥3 | 1 | 1800 | 81 | 80 |
| 108 | valtatie | 2 | 1900 | 97 | 100 |
| 109 | kantatie, seututie, yhdystie | 2 | 1700 | 97 | 100 |
| 110 | valtatie | 2 | 1900 | 90 | 90 |
| 111 | kantatie, seututie, yhdystie | 2 | 1700 | 90 | 90 |
| 112 | valtatie | 2 | 1850 | 81 | 80 |
| 113 | kantatie, seututie | 2 | 1650 | 81 | 80 |
| 114 | valtatie | 2 | 1600 | 73 | 70 |
| 115 | kantatie, seututie, yhdystie | 2 | 1500 | 73 | 70 |
| 116 | valtatie | 2 | 1600 | 63 | 60 |
| 117 | kantatie, seututie | 2 | 1400 | 63 | 60 |
| 118 | liityntäkatu tai tärkeä yksityistie | 3 | 1400 | 97 | 100 |
| 119 | liityntäkatu tai tärkeä yksityistie | 3 | 1400 | 90 | 90 |
| 120 | liityntäkatu tai tärkeä yksityistie | 3 | 1350 | 81 | 80 |
| 121 | yhdystie | 3 | 1200 | 58 | 60-80 |
| 122 | liityntäkatu tai tärkeä yksityistie | 3 | 1100 | 73 | 70 |
| 123 | useampikaistaiset pääkadut, valot | 3 | 1250 | 54 | 60 |
| 124 | kantatie, seututie, yhdystie, liityntäkatu tai tärkeä yksityistie | 3 | 1100 | 63 | 60-80 |
| 125 | seudullinen pääkatu | 4 | 1150 | 48 | 50 |
| 126 | pääkatu tai alueellinen kokoojakatu | 4 | 1050 | 48 | 50 |
| 127 | yhdystie tai kokoojakatu | 4 | 1000 | 44 | 50 |
| 128 | pääkatu | 4 | 1000 | 41 | 30-40 |
| 129 | pääkatu tai kokoojakatu | 4 | 900 | 41 | 40 |
| 130 | kokoojakatu | 5 | 900 | 48 | 50 |
| 131 | keskustan pääkatu, valot | 5 | 900 | 41 | 50 |
| 132 | keskustan pääkatu, valot | 5 | 900 | 36 | 40 |
| 133 | keskustan kokoojakatu | 5 | 750 | 36 | 40 |
| 134 | tonttikatu | 5 | 600 | 36 | 40 |
| 135 | pääkatu | 5 | 700 | 30 | 30 |
| 136 | pääkatu | 5 | 600 | 25 | 30 |
| 137 | pääkatu tai kokoojakatu | 5 | 550 | 20 | 30 |
| 138 | tonttikatu | 5 | 500 | 18 | 30 |
| 139 | pääkatu tai kokoojakatu | 5 | 700 | 20 | 20 |
| 140 | paikalliskatu | 5 | 600 | 15 | 20 |
| 141 | paikalliskatu | 5 | 500 | 12 | 20 |
| 144 | lautta | 11 | 500 | 20 |

### Tie- ja katuverkon koodausperiaatteet

Valma-ajon yhteydessä linkkien ul1 (vapaa nopeus), ul2 (kapasiteetti) ja vdf (viivytysfunktio) -arvot ylikirjoitetaan linkkityypin perusteella, joten niitä ei tarvitse määritellä erikseen linkeille.

## Joukkoliikenne
### Joukkoliikenteen ajoneuvotyypit
### Joukkoliikennelinjojen pysähtymiskäyttäytyminen
Joukkoliikennelinjoilla on linja-attribuutti `#keep_stops`, jolla määritetään, miten linjan pysähtymiskäyttäytyminen määräytyy.

- **`#keep_stops = 1`:** Linja säilyttää alkuperäisen pysähtymiskäyttäytymisensä. Pysähtyminen määräytyy noodien kulkumuotokohtaisten attribuuttien `#transit_stop_b`, `#transit_stop_e`, `#transit_stop_g`, `#transit_stop_p` ja `#transit_stop_t` perusteella.
- **`#keep_stops = 0`:** Linja pysähtyy niillä pysäkeillä, jotka on määritetty pysäkkisegmenteille.

Attribuutti `#keep_stops` koskee vain seuraavia kulkumuotoja: `b` (bussi), `e` (kaukobussi), `g` (runkobussi), `p` (pikaratikka) ja `t` (ratikka).

### Joukkoliikennelinjastot

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
| `id` | Joukkoliikennesegmentin tunniste |
| `line` | Joukkoliikennelinja |
| `i` | Segmentin I-solmu |
| `j` | Segmentin J-solmu |
| `loop_index` | Segmentin indeksi saman linkin segmenttien joukossa reitillä |
| `dwt` | Pysähdyksen kesto |
| `noali` | Ei poistumista I-solmusta |
| `noboa` | Ei nousemista I-solmusta |
| `dwfac` | Pysähdyksen kestoa kuvaava kerroin |
| `ttf` | Joukkoliikenteen matka-aikafunktio |
| `us1` | GTFS-matka-aika pysäkkien välillä |
| `us2` | VAPAA |
| `us3` | VAPAA |


## Tavaraliikenne

