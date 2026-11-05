---
nav_order: 6
sort: 6
---

# Henkilöliikennemallin kalibrointi

Tämä ohje on tarkoitettu tilanteeseen, jossa pitää tehdä tarkastelukohtainen mallikalibrointi.

Kalibrointi annetaan kahdessa valinnaisessa tiedostossa, jotka asetetaan käyttöliittymän projektiasetuksissa. Sama kalibrointi koskee siten kaikkia projektin skenaarioita.

| Tiedosto | Projektiasetus | Komentoriviparametri |
|---|---|---|
| Kulkutapa- ja matkakohdevalinnan kalibrointi (.json) | Kulkutapa- ja matkakohdevalinnan kalibrointitiedosto | `--mode-dest-calibration-file` |
| Kunta-kunta-kalibrointi (.txt) | Kunta-kunta-kalibroinnin tiedosto | `--municipality-calibration-file` |

**Tee kuitenkin aina ensin tarvittavat korjaukset verkkoon ja aluejakoon!**

Huomioi seuraavat _ennen_ kalibrointia:

1. Liikenne- ja matkustajamäärien vertaaminen laskentoihin. Syy poikkeamiin voi olla verkon koodauksessa; esimerkiksi linkin kapasiteetti tai nopeus voi olla virheellinen.
2. Joukkoliikenteen tarkastelussa tulee tarkistaa erityisesti kävelyetäisyydet.
3. Aluejako voi olla liian harva, jolloin sitä tulee tarkentaa.
       - Lisää sentroideja ja konnektoreita Emmeen.
       - Tee vastaavat lisäykset syöttötietoihin (.gpkg).

## Kulkutapa- ja matkakohdevalinnan kalibrointi
   
Kulkutapa- ja matkakohdevalinnan kalibroinnissa *lisätään* vaihtoehtokohtainen komponentti hyötyfunktioon _U_.

Logit-todennäköisyys `e^U/Σe^U` toimii yleisesti niin, että valintajakauma muuttuu suhteellisesti lisäkomponentin e-potenssin mukaan. Sen takia karkea arvio lisäkomponentin tarpeen suuruudesta saadaan kaavalla `ln(todellisuus / kalibroimaton malli)`. 
> Esim. jos ruuhkatunnin joukkoliikennematkustaminen Helsingin kantakaupunkiin on todellisuudessa 30 % suurempi kuin malli sanoo, sopiva lisäkomponentti on  
> $\ln(1.3) = 0.26$.   

Lisäkomponentti kohdennetaan johonkin aluetietojen (.gpkg) alueluokitukseen. Käytettävissä ovat seuraavat luokitukset:

| Luokitus | Alueen nimi |
|---|---|
| `zone` | Ajettavan osamallin sijoittelualueen numero |
| `municipality`, `county`, `submodel`, `pt_authority`, `calibration_area` | Aluetietojen samannimisen sarakkeen arvo |

Muita luokituksia, kuten aluetietojen _aggregate_results_-sarakkeita, ei voi käyttää kalibroinnissa, ja ajo pysähtyy virheeseen, jos niitä annetaan. Jos haluat kalibroida oman alueen, kirjoita alueen nimi aluetietojen `calibration_area`-sarakkeeseen.

Kalibrointia on hyvä hieman tasoittaa alueellisesti. Esim. jos lisätään attraktiota Helsingin kantakaupunkiin, olisi hyvä hieman lisätä attraktiota Helsingin esikaupunkialueillekin. Muuten malliin saattaa tulla erikoisia rajailmiöitä. Attraktio- ja kulkutapakalibrointi ei lisää kysyntää, vaan kysyntä siirretään tasaisesti kaikista matkakohteista tai kulkutavoista. Tämä tarkoittaa, että jos kalibroitu kulkutapa tai matkakohde muodostaa suuren osan todennäköisyydestä, kalibrointi pitää iteroida saavuttaakseen toivottu lopputulos.

Käyttöliittymässä kalibroinnin lisäkomponentit syötetään Valma-projektiasetuksissa json-formaatissa kohdassa "kulkutapa- ja matkakohdevalinnan kalibrointitiedosto (.json)".

Tiedostossa on kaksi osiota, joiden molempien tulee olla mukana (osio voi olla tyhjä, `{}`):
- `mode_choice_calibration` lisää vakion kulkutavan hyötyyn niille kiertomatkoille, jotka __generoituvat__ alueelta (kotiperäisillä kiertomatkoilla alueen asukkaiden kiertomatkoille). Käytä sitä, kun alueen _kulkutapajakauma_ on pielessä.
- `destination_choice_calibration` lisää vakion alueen sijoittelualueiden hyötyyn tietyllä kulkutavalla tehtävien kiertomatkojen __matkakohteina__. Käytä sitä, kun alueen _attraktio_ on pielessä.

Jos alueen nimeä ei löydy aluetiedoista, lokiin tulee varoitus _Dummy variable … not found in …_, eikä vakiolla ole vaikutusta.

> HUOM: Kalibrointivakio __korvaa__ mallissa jo olevan vakion, jolla on sama alueen nimi ja kulkutapa. Kotiperäisten matkaryhmien kulkutapamalleissa on valmiiksi vakiot joukkoliikenteen toimivaltaisten viranomaisten alueilta generoituville kiertomatkoille (aluetietojen sarake `pt_authority`):
> - `HSL`, `Tampere` ja `Turku`: joukkoliikennevakio (`transit`)
> - `Oulu`: pyöräilyvakio (`bike`), työasiointi- ja yön yli -matkoilla (hb_business, hb_overnight) kävelyvakio (`walk`). Oululla ei ole valmista joukkoliikennevakiota.
>
> Näiden alueiden ja kulkutapojen kalibrointi `pt_authority`-luokituksella korvaa siis estimoidut vakiot sen sijaan, että lisäisi niihin. Esimerkiksi Oulun joukkoliikennevakio lisätään uutena vakiona, mutta Oulun pyöräilyvakio korvaa estimoidun vakion.
>
> Osassa matkaryhmistä (hb_edu_basic, hb_grocery, hb_leisure, hb_other_shop, hb_sport, hb_visit ja hb_work) näihin vakioihin sovelletaan lisäksi matkaryhmäkohtaista skaalauskerrointa. Kun kalibrointivakio korvaa tällaisen vakion, myös annettu kalibrointivakio kerrotaan skaalauskertoimella (kertoimet ovat välillä 0,1–0,9), joten sen vaikutus on näissä matkaryhmissä annettua pienempi.

Vakiot annetaan kulkutavoittain, ja ne koskevat __kaikkia matkaryhmiä__, joiden kulkutapa- tai kohdevalintamallissa kyseinen kulkutapa on. Kalibrointia ei voi kohdistaa yksittäiseen matkaryhmään.

| Osio | Kalibroitavat kulkutavat |
|---|---|
| `mode_choice_calibration` | `car_driver`, `car_passenger`, `transit`, `bike`, `walk`, `airplane` |
| `destination_choice_calibration` | `car_driver`, `car_passenger`, `transit`, `bike`, `walk` |

Muut nimet, esimerkiksi kulkutavan ja matkaryhmän yhdistelmät kuten `car_work` tai `transit_work`, jätetään huomiotta ilman varoitusta. Kohdevalinnan kalibrointi ei vaikuta pitkien matkojen matkaryhmiin (`hb_business`, `hb_overnight`, `hb_abroad_other`).

> HUOM: Käytä osioissa eri alueluokituksia. Jos molemmissa osioissa käytetään samaa luokitusta (esimerkiksi `calibration_area`), aluetietoihin luodaan vain `destination_choice_calibration`-osion alueet, ja ajo pysähtyy virheeseen `mode_choice_calibration`-osion alueiden kohdalla.

Esimerkkitiedosto, jossa Vantaalta generoituvien kiertomatkojen henkilöautoilua (kuljettajana) lisätään ja Helsingin kantakaupunkiin ja esikaupunkialueille sekä sijoittelualueelle 202 suuntautuvien matkojen attraktiota lisätään:

```json
{
    "mode_choice_calibration": {
        "municipality": {
            "Vantaa": {
                "car_driver": 0.1
            }
        }
    },
    "destination_choice_calibration": {
        "calibration_area": {
            "Helsingin kantakaupunki": {
                "transit": 0.26
            },
            "Helsingin esikaupunkialueet": {
                "transit": 0.13
            }
        },
        "zone": {
            "202": {
                "car_driver": 0.18
            }
        }
    }
}
```

## Kunta-kunta-kalibrointi

Kunta–kunta‑kalibroinnilla voidaan räätälöidä matkojen suuntautuminen niin, että jokaiselle lähtökunnalle määritetään oma kohdekuntakohtainen kalibrointi. Kalibrointi toimii samalla logiikalla kuin edellä mainittu attraktiokalibrointi. Tällöin vain kunnasta lähtevien matkojen _suuntautuminen_ muuttuu ilman matkojen kokonaismäärän muuttumista. 

Kalibroinnin tiedoston tulee olla sarkaineroteltu tekstitiedosto (.txt). Siinä kahden ensimmäisen sarakeotsikon nimet ovat aina _generation_ ja _attraction_. Seuraavat sarakeotsikot kertovat, mihin kulkutapoihin kalibrointi kohdistuu.

Sarakkeisiin _generation_ (lähtökunta) ja _attraction_ (kohdekunta) kirjoitetaan kuntien nimet samassa muodossa kuin aluetietojen `municipality`-sarakkeessa. Kuntapareille, joita ei ole tiedostossa, ei lisätä vakiota.

Kulkutapasarakkeet nimetään kohdevalinnan kulkutapojen mukaan: `car_driver`, `car_passenger`, `transit`, `bike` ja `walk`. Kunkin sarakkeen vakiot lisätään kaikkien kyseistä kulkutapaa käyttävien matkaryhmien kohdevalinnan hyötyyn. Muut sarakkeet (esimerkiksi `car_work`) jätetään huomiotta ilman varoitusta. Käytä desimaalierottimena pistettä.

> HUOM: Mallijärjestelmän nykyisessä dev-versiossa (commit `12ba8b8`) kulkutapojen, joiden nimessä on alaviiva (`car_driver`, `car_passenger`), sarakkeilla ei ole vaikutusta, eikä tästä anneta varoitusta. Vain sarakkeet `transit`, `bike` ja `walk` otetaan huomioon.

Esimerkkinä tiedosto, jossa lähtökuntina ovat Espoo ja Kauniainen ja näiden kohdekuntina Helsinki. Kulkutavoiksi on valittu joukkoliikenne ja pyörä (sarakkeet erotetaan sarkaimilla):

| generation | attraction | transit | bike |
|---|---|---|---|
| Espoo | Helsinki | -0.1 | 0.1 |
| Kauniainen | Helsinki | 0.1 | -0.1 |

Käyttöliittymässä tekstitiedosto syötetään Valma-projektiasetuksissa txt-formaatissa kohdassa
“kunta-kunta-kalibroinnin tiedosto (.txt)”.
