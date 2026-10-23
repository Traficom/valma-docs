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
| network field | #subarea | 1 = osamallialue, 2 = osamallin bufferialue, 3 = bufferialueen ulkopuolinen alue |
| network field | #transit_stop_b | Bussipysäkki |
| network field | #transit_stop_e | Kaukobussipysäkki |
| network field | #transit_stop_g | Runkobussipysäkki |
| network field | #transit_stop_p | Pikaratikkapysäkki |
| network field | #transit_stop_t | Ratikkapysäkki |

#### Sentroidit
Sentroidit edustavat liikennemallin sijoittelualueita. Sijoittelualueiden liikenne kytkeytyy varsinaiseen liikenneverkkoon sentroidien ja niitä ympäröivien konnektoreiden avulla.




### Kulkumuodot
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
| `h` | Päämoodi |



### Linkit

*Taulukko x. Linkkien ominaisuudet*

| kenttä          | kuvaus                                                 |
|-----------------|--------------------------------------------------------------|
| type            | ks. taulukko x                                              |
| length          | linkin pituus                                                             |
| lanes           | kaistamäärä |
| modes           | kulkumuodot (taulukko x)                                                    |
| vdf             | sijoittelufunktion nro                                       |
| ul1 | linkin yhden kaistan kapasiteetti |
| ul2             | linkin vapaa nopeus                                          |
| ul3             | VAPAA  |
| @ferry_wait_time |                          |
| @toll_cost_vrk      |     |
| @freight_gate      |     |
| #car_time_aht      |     |
| #car_time_iht      |     |
| #car_time_it      |     |
| #car_time_pt      |     |
| #car_time_vrk      |     |
| #dr_leveys      |     |
| #dr_linkkityyp      |     |
| #dr_nopeusrajoitus      |     |
| #dr_toiminn_lk      |     |
| #extra_cost      |     |
| #hinta_vrk      |     |
| #road_number      |     |
| #road_part_nr_max      |     |
| #road_part_nr_min      |     |
| #street_name      |     |
| #traffic_light      |     |

#### Syöttölinkit
Syöttölinkeillä (linkkityyppi 99) sentroidit yhdistetään ympäröivään verkkoon. Jokaisesta sentroidista on olemassa yksi autoliikenteen ja yksi kävely- ja pyöräliikenteen syöttölinkki lähimpiin solmuihin. Autoliikenteen syöttölinkkiä ei saa yhdistää moottoritiehen, ramppeihin, liikenneympyröihin tai kaksiajorataisiin katuihin/teihin.


*Taulukko x. Sijoittelufunktioiden jako väylätyyppeihin*
| linkkityyp | toiminn_lk | kaistojen_lkm | nopeusrajoitus | type | VDF | ul1 | ul2 |
|---:|---:|---:|---:|---:|---:|---:|---:|
| 1 | | 1,2 | 120 | 101 | 1 | 2100 | 113 |
| 1 | | 3,4,5 | 120 | 103 | 1 | 1900 | 113 |
| 1 | | 1,2 | 100 | 104 | 1 | 2000 | 97 |
| 1 | | 3,4,5 | 100 | 105 | 1 | 1800 | 97 |
| 1 | | 1,2 | 80 | 106 | 1 | 2000 | 81 |
| 1 | | 3,4,5 | 80 | 107 | 1 | 1800 | 81 |
| 6 | | | 120 | 102 | 1 | 2000 | 113 |
| | 1 | | 100 | 108 | 2 | 1900 | 97 |
| | 1 | | 90 | 110 | 2 | 1900 | 90 |
| | 1 | | 80 | 112 | 2 | 1850 | 81 |
| | 1 | | 70 | 114 | 2 | 1600 | 73 |
| | 1 | | 60 | 116 | 2 | 1600 | 63 |
| | 2,3,4 | | 100 | 109 | 3 | 1700 | 97 |
| | 2,3,4 | | 90 | 111 | 3 | 1700 | 90 |
| | 2,3,4 | | 80 | 113 | 3 | 1650 | 81 |
| | 2,3,4 | | 70 | 115 | 3 | 1400 | 68 |
| | 2,3,4 | | 60 | 117 | 3 | 1400 | 63 |
| | 5 | | 100 | 118 | 5 | 700 | 50 |
| | 5 | | 90 | 119 | 5 | 700 | 50 |
| | 5 | | 80 | 120 | 5 | 600 | 40 |
| Varaus: useampikaistaiset pääkadut, valot | | | 70 | 121 | 3 | 1450 | 61 |
| | 5 | | 70 | 122 | 5 | 800 | 60 |
| Varaus: useampikaistaiset pääkadut, valot | | | 60 | 123 | 3 | 1250 | 54 |
| | 5 | | 60 | 124 | 5 | 800 | 50 |
| | 1 | | 50 | 125 | 4 | 900 | 50 |
| | 1 | | 40 | 128 | 4 | 900 | 41 |
| | 1 | | 30 | 135 | 5 | 700 | 30 |
| | 1 | | 20 | 139 | 5 | 700 | 20 |
| | 2,3,4 | | 50 | 126 | 4 | 1050 | 54 |
| Varaus: esik. pääkadut, valot | | | 50 | 127 | 4 | 1000 | 44 |
| | 2,3,4 | | 40 | 129 | 4 | 900 | 38 |
| Varaus: keskustan pääkadut, valot | | | 50 | 131 | 4 | 900 | 41 |
| Varaus: keskustan pääkadut, valot | | | 40 | 132 | 4 | 800 | 36 |
| Varaus: keskustan kokoojat | | | 40 | 133 | 5 | 750 | 36 |
| | 2,3,4 | | 30 | 136 | 5 | 600 | 30 |
| Varaus: keskustan, pienet kadut | | | 30 | 138 | 5 | 500 | 23 |
| | 2,3,4 | | 20 | 140 | 5 | 500 | 20 |
| | 5 | | 50 | 130 | 5 | 800 | 40 |
| | 5 | | 40 | 134 | 5 | 600 | 30 |
| | 5 | | 30 | 137 | 5 | 500 | 30 |
| | 5 | | 20 | 141 | 5 | 500 | 20 |

### Tie- ja katuverkon koodausperiaatteet
## Joukkoliikenne
### Joukkoliikenteen ajoneuvotyypit
### Joukkoliikennelinjojen pysähtymiskäyttäytyminen
### Joukkoliikennelinjastot
## Tavaraliikenne

##### Sentroidien numerointi kunnittain

| Kunta | Kunnan ensimmäinen sentroidinumero |
|---|---:|
| Helsinki | 100 |
| Espoo | 1100 |
| Vantaa | 1600 |
| Hyvinkää | 2000 |
| Lohja | 2100 |
| Järvenpää | 2200 |
| Nurmijärvi | 2300 |
| Kirkkonummi | 2400 |
| Tuusula | 2500 |
| Kerava | 2600 |
| Vihti | 2700 |
| Sipoo | 2800 |
| Mäntsälä | 2900 |
| Kauniainen | 3000 |
| Karkkila | 3100 |
| Siuntio | 3200 |
| Pornainen | 3300 |
| Loviisa | 3400 |
| Lapinjärvi | 3500 |
| Porvoo | 3600 |
| Askola | 3700 |
| Pukkila | 3800 |
| Myrskylä | 3900 |
| Raasepori | 4000 |
| Hanko | 4100 |
| Inkoo | 4200 |
| Janakkala | 4300 |
| Riihimäki | 4400 |
| Hausjärvi | 4500 |
| Loppi | 4600 |
| Orimattila | 4700 |
| Kärkölä | 4800 |
| Maarianhamina | 4900 |
| Jomala | 5000 |
| Finström | 5100 |
| Lemland | 5200 |
| Saltvik | 5300 |
| Hammarland | 5400 |
| Sund | 5500 |
| Eckerö | 5600 |
| Geta | 5700 |
| Lumparland | 5800 |
| Föglö | 5900 |
| Vårdö | 6000 |
| Brändö | 6100 |
| Kumlinge | 6200 |
| Kökar | 6300 |
| Sottunga | 6400 |
| Forssa | 6500 |
| Tammela | 6600 |
| Jokioinen | 6700 |
| Ypäjä | 6800 |
| Humppila | 6900 |
| Hämeenlinna | 7000 |
| Hattula | 7200 |
| Valkeakoski | 7300 |
| Akaa | 7400 |
| Urjala | 7500 |
| Sastamala | 7600 |
| Punkalaidun | 7700 |
| Ikaalinen | 7800 |
| Parkano | 7900 |
| Kihniö | 8000 |
| Tampere | 8100 |
| Nokia | 8500 |
| Ylöjärvi | 8600 |
| Kangasala | 8700 |
| Lempäälä | 8800 |
| Pirkkala | 8900 |
| Hämeenkyrö | 9000 |
| Orivesi | 9100 |
| Pälkäne | 9200 |
| Vesilahti | 9300 |
| Kuhmoinen | 9400 |
| Mänttä-Vilppula | 9500 |
| Virrat | 9600 |
| Ruovesi | 9700 |
| Juupajoki | 9800 |
| Kankaanpää | 9900 |
| Karvia | 10000 |
| Jämijärvi | 10100 |
| Siikainen | 10200 |
| Pori | 10300 |
| Ulvila | 10500 |
| Huittinen | 10600 |
| Kokemäki | 10700 |
| Harjavalta | 10800 |
| Nakkila | 10900 |
| Merikarvia | 11000 |
| Pomarkku | 11100 |
| Rauma | 11200 |
| Eura | 11300 |
| Eurajoki | 11400 |
| Säkylä | 11500 |
| Loimaa | 11600 |
| Pöytyä | 11700 |
| Aura | 11800 |
| Koski Tl | 11900 |
| Marttila | 12000 |
| Oripää | 12100 |
| Salo | 12200 |
| Somero | 12400 |
| Turku | 12500 |
| Kaarina | 12900 |
| Raisio | 13000 |
| Lieto | 13100 |
| Naantali | 13200 |
| Paimio | 13300 |
| Masku | 13400 |
| Mynämäki | 13500 |
| Rusko | 13600 |
| Nousiainen | 13700 |
| Sauvo | 13800 |
| Parainen | 13900 |
| Kemiönsaari | 14000 |
| Uusikaupunki | 14100 |
| Laitila | 14200 |
| Vehmaa | 14300 |
| Pyhäranta | 14400 |
| Taivassalo | 14500 |
| Kustavi | 14600 |
| Imatra | 14700 |
| Ruokolahti | 14800 |
| Parikkala | 14900 |
| Rautjärvi | 15000 |
| Lappeenranta | 15100 |
| Taipalsaari | 15300 |
| Luumäki | 15400 |
| Savitaipale | 15500 |
| Lemi | 15600 |
| Mikkeli | 15700 |
| Mäntyharju | 15900 |
| Kangasniemi | 16000 |
| Puumala | 16100 |
| Hirvensalmi | 16200 |
| Pertunmaa | 16300 |
| Pieksämäki | 16400 |
| Juva | 16500 |
| Savonlinna | 16600 |
| Rantasalmi | 16700 |
| Sulkava | 16800 |
| Enonkoski | 16900 |
| Joutsa | 17000 |
| Luhanka | 17100 |
| Jyväskylä | 17200 |
| Laukaa | 17500 |
| Muurame | 17600 |
| Hankasalmi | 17700 |
| Petäjävesi | 17800 |
| Uurainen | 17900 |
| Toivakka | 18000 |
| Jämsä | 18100 |
| Keuruu | 18200 |
| Multia | 18300 |
| Saarijärvi | 18400 |
| Viitasaari | 18500 |
| Pihtipudas | 18600 |
| Karstula | 18700 |
| Kinnula | 18800 |
| Kannonkoski | 18900 |
| Kyyjärvi | 19000 |
| Kivijärvi | 19100 |
| Äänekoski | 19200 |
| Konnevesi | 19300 |
| Kotka | 19400 |
| Hamina | 19500 |
| Pyhtää | 19600 |
| Virolahti | 19700 |
| Miehikkälä | 19800 |
| Kouvola | 19900 |
| Joensuu | 20100 |
| Kontiolahti | 20300 |
| Liperi | 20400 |
| Outokumpu | 20500 |
| Ilomantsi | 20600 |
| Juuka | 20700 |
| Polvijärvi | 20800 |
| Heinävesi | 20900 |
| Kitee | 21000 |
| Tohmajärvi | 21100 |
| Rääkkylä | 21200 |
| Lieksa | 21300 |
| Nurmes | 21400 |
| Kaavi | 21500 |
| Tuusniemi | 21600 |
| Rautavaara | 21700 |
| Kuopio | 21800 |
| Siilinjärvi | 22100 |
| Suonenjoki | 22200 |
| Rautalampi | 22300 |
| Vesanto | 22400 |
| Tervo | 22500 |
| Varkaus | 22600 |
| Leppävirta | 22700 |
| Joroinen | 22800 |
| Iisalmi | 22900 |
| Lapinlahti | 23000 |
| Kiuruvesi | 23100 |
| Pielavesi | 23200 |
| Sonkajärvi | 23300 |
| Vieremä | 23400 |
| Keitele | 23500 |
| Lahti | 23600 |
| Hollola | 23900 |
| Heinola | 24000 |
| Asikkala | 24100 |
| Iitti | 24200 |
| Sysmä | 24300 |
| Padasjoki | 24400 |
| Hartola | 24500 |
| Alajärvi | 24600 |
| Lappajärvi | 24700 |
| Vimpeli | 24800 |
| Evijärvi | 24900 |
| Alavus | 25000 |
| Ähtäri | 25100 |
| Kuortane | 25200 |
| Soini | 25300 |
| Seinäjoki | 25400 |
| Kurikka | 25600 |
| Kauhava | 25700 |
| Lapua | 25800 |
| Ilmajoki | 25900 |
| Isokyrö | 26000 |
| Kauhajoki | 26100 |
| Teuva | 26200 |
| Isojoki | 26300 |
| Karijoki | 26400 |
| Kajaani | 26500 |
| Sotkamo | 26600 |
| Paltamo | 26700 |
| Ristijärvi | 26800 |
| Kuhmo | 26900 |
| Suomussalmi | 27000 |
| Puolanka | 27100 |
| Hyrynsalmi | 27200 |
| Kaustinen | 27300 |
| Veteli | 27400 |
| Toholampi | 27500 |
| Perho | 27600 |
| Halsua | 27700 |
| Lestijärvi | 27800 |
| Kokkola | 27900 |
| Kannus | 28000 |
| Kemijärvi | 28100 |
| Salla | 28200 |
| Posio | 28300 |
| Savukoski | 28400 |
| Pelkosenniemi | 28500 |
| Tornio | 28600 |
| Kemi | 28700 |
| Keminmaa | 28800 |
| Simo | 28900 |
| Tervola | 29000 |
| Sodankylä | 29100 |
| Inari | 29200 |
| Utsjoki | 29300 |
| Rovaniemi | 29400 |
| Ranua | 29600 |
| Ylitornio | 29700 |
| Pello | 29800 |
| Kittilä | 29900 |
| Kolari | 30000 |
| Muonio | 30100 |
| Enontekiö | 30200 |
| Pietarsaari | 30300 |
| Pedersören kunta | 30400 |
| Uusikaarlepyy | 30500 |
| Kruunupyy | 30600 |
| Luoto | 30700 |
| Närpiö | 30800 |
| Kristiinankau-punki | 30900 |
| Kaskinen | 31000 |
| Vaasa | 31100 |
| Mustasaari | 31300 |
| Laihia | 31400 |
| Vöyri | 31500 |
| Maalahti | 31600 |
| Korsnäs | 31700 |
| Haapavesi | 31800 |
| Siikalatva | 31900 |
| Pyhäntä | 32000 |
| Kuusamo | 32100 |
| Taivalkoski | 32200 |
| Nivala | 32300 |
| Haapajärvi | 32400 |
| Pyhäjärvi | 32500 |
| Reisjärvi | 32600 |
| Kärsämäki | 32700 |
| Oulu | 32800 |
| Kempele | 33200 |
| Liminka | 33300 |
| Muhos | 33400 |
| Tyrnävä | 33500 |
| Lumijoki | 33600 |
| Hailuoto | 33700 |
| Ii | 33800 |
| Pudasjärvi | 33900 |
| Vaala | 34000 |
| Utajärvi | 34100 |
| Raahe | 34200 |
| Siikajoki | 34300 |
| Pyhäjoki | 34400 |
| Ylivieska | 34500 |
| Kalajoki | 34600 |
| Oulainen | 34700 |
| Sievi | 34800 |
| Alavieska | 34900 |
| Merijärvi | 35000 |
