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

#### Sentroidit
Sentroidit edustavat liikennemallin sijoittelualueita. Sijoittelualueiden liikenne kytkeytyy varsinaiseen liikenneverkkoon sentroidien ja niitä ympäröivien konnektoreiden avulla.

### Kulkumuodot
*Taulukko 7. Kulkumuotojen (modes) kuvaus*

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
