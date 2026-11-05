---
nav_order: 5
sort: 5
---

# Malliajojen tulokset

Tulosten tallennuspolku määritellään käyttöliittymän projektiasetuksissa kohdassa projektikansio. Ohjeet projektiasetuksiin löydät [täältä](mallijarjestelman_kaytto.md).
VALMA-skenaarioajojen eli malliajojen tulokset tallentuvat projektikansion alikansioon, jonka nimi vastaa ajetun skenaarion nimeä. Tulokset ovat tekstitiedostoja sekä matriiseja (.omx). Lisäksi verkkotulokset tallentuvat GeoPackage-tiedostoon, ja sijoittelutulokset jäävät Emme-pankkiin, jossa niitä voi analysoida EMMEn työkaluilla.

Skenaarion tuloskansioon tallentuvat myös
- ajon lokitiedosto `<skenaarion nimi>.log`, jossa ovat ajon asetukset, eteneminen, kunkin iteraation kulkutapaosuudet ja konvergenssi sekä varoitukset ja virheet
- ajon kaikki parametrit tiedostossa `runtime_params.json`, jonka avulla ajon voi toistaa komentoriviltä.

Henkilöliikenteen mallin tuloskansion rakenne:

```
<projektikansio>
└── <skenaarion nimi>
    ├── <skenaarion nimi>.log
    ├── runtime_params.json
    ├── aggregated_results
    │   └── <osamalli>
    │       ├── *.txt
    │       └── Matrices
    │           └── logsum_<matkaryhmä>_vrk.omx
    ├── link_results
    │   └── assignment_results_<osamalli>.gpkg
    ├── demand_matrices
    │   └── <osamalli>
    │       ├── demand_<ajanjakso>.omx
    │       ├── demand_vrk.omx
    │       └── long_dist_demand_vrk.omx
    └── los_matrices
        └── <osamalli>
            ├── beeline_.omx
            └── <tyyppi>_<ajanjakso>.omx
```

Tavaraliikenteen malli kirjoittaa tulostaulukkonsa suoraan skenaarion tuloskansioon ja kysyntämatriisinsa kansioon `demand_matrices\koko_suomi` (ks. kohta _Tulosmatriisit_).

## Malliajon validointi

Malliajoissa käytetään suurta määrää erilaisia lähtötietoja, joten virheet ajoissa ovat tyypillisiä. Suositamme siksi tekemään malliajoille seuraavan validointirutiinin. Tärkein validointi on malliajon tulosten tulkinta, mutta rutiinin avulla voidaan varmistua että malliajossa ei ole ollut suuria virheitä.

### Vastukset
Malliajon tulostiedostoihin tulostuu mallista tiedosto "los_validation.txt", jossa on esitetty matka-ajat ja kustannukset valituille yhteysväleille. Näitä tietoja voi verrata nykytilanteen ajoon, jonka vastaava tiedosto on saatavilla Sharefilesta.
* Tulos ei eri skenaarioita kuvaavissa ajoissa ole välttämättä täysin sama kuin nykytilanteessa, mutta muutoksen tulee olla looginen suhteessa nykytilaan. Mikäli ratahanke nopeuttaa matka-aikaa, ei poikkeaman tulisi olla positiivinen.

### Kulkutapajakauma
Malliajon tulostiedostoihin tulostuu "purpose_mode_shares.txt", jossa on esitetty kulkutapaosuudet matkaryhmittäin. Lisäksi koko mallin kulkutapaosuudet kirjoitetaan jokaisen iteraation jälkeen lokiin (rivit _"Mode shares (… iteration)"_). Vertaa niitä nykytilan ajon vastaaviin tietoihin, jotka ovat saatavilla Sharefilesta.
* Tulos ei eri skenaarioita kuvaavissa ajoissa ole välttämättä täysin sama kuin nykytilanteessa, mutta muutoksen tulee olla looginen suhteessa nykytilaan. Mikäli joukkoliikenteen palvelutaso paranee, ei poikkeaman tulisi olla negatiivinen.

### Konvergenssi ja loki
Tarkista, että ajo on konvergoitunut (tiedosto "demand_convergence.txt" ja lokin varoitus _"Model has not converged"_), ja lue lokin varoitukset. Konvergoitumattoman ajon tuloksia ei tule käyttää tarkistamatta.

## Tulostiedostot

Seuraavassa esitetty malliajon tuottamien tulostiedostojen sisältö. Kaikki tulostaulukot ovat sarkaineroteltuja tekstitiedostoja, jotka voi avata Excelissä tai lukea millä tahansa data-analyysityökalulla. Ellei toisin mainita, henkilöliikenteen arvot ovat keskimääräiseltä vuorokaudelta (tavaraliikenteen tulostaulukoiden yksiköt on kuvattu niiden omassa taulukossa), kysyntä on kiertomatkoina ja aluekohtaiset tulokset ovat osamallin sijoittelualueittain. Henkilöliikenteen mallin tulostaulukot tallentuvat osamallikohtaisiin alikansioihin.

| Tiedoston nimi                               | Kuvaus | Tarkempi kuvaus | Yksikkö |
|----------------------------------------------|--------|-----------------|-----------------|
| accessibility.txt | Logsum-saavutettavuus. | Kysyntämallista laskettu aluekohtainen logsum-saavutettavuus (1), joka lasketaan matkaryhmittäin ja kulkutavoittain. Esitetään välimatka-asteikolla, joten suhdelukujen käyttö ei mahdollista. | Yksikötön |
| aggregated_demand_[county/municipality/..].txt | Alueelta alueelle kysyntä | Kiertomatkojen kysyntä alueelta alueelle kulkutavoittain ja matkaryhmittäin. Sisältää vain kiertomatkat lähtöpaikasta pääasialliseen matkakohteeseen, eli ei vastaa suoraan liikenneverkolle tulevaa liikennettä. Uusia alueita voi määrittää Zonedatan kautta. | Kiertomatkaa / vrk |
| car_ownership | Kotitalouden autonomistus | hh_lic, cars koostuu kotitaloudesta (hh), jossa voi olla 1 tai 2 aikuista, ajokortillisista henkilöistä (lic), joita voi olla 1 tai 2 sekä kotitalouden autoista, joita voi olla 0, 1 tai 2+.| Prosenttiosuus desimaalina 0-1 |
| zone_attraction_by_mode/purpose.txt | Alueen attraktoimat kiertomatkat  | Aluetasolla esitetty attraktio, eli saapuvien kiertomatkojen lukumäärä vuorokaudessa. | Kiertomatkaa / vrk |
| zone_attraction_dist_by_mode/purpose.txt | Alueen attraktoimien kiertomatkojen keskipituus | Aluetasolla esitetty attraktoitujen matkojen keskipituus laskettuna linnuntie-etäisyydestä. Ei nykyisellään käyttökelpoinen suoritelaskuissa. | km / kiertomatka |
| zone_generation_by_mode/purpose.txt | Alueen generoimat kiertomatkat  | Aluetasolla esitetty generaatio, eli lähtevien kiertomatkojen lukumäärä vuorokaudessa.  | Kiertomatkaa / vrk |
| zone_generation_dist_by_mode/purpose.txt | Alueen generoimien kiertomatkojen keskipituus | kts. zone_attraction_dist_by_mode/purpose.tx | km / kiertomatka |
| zonedata_input.txt | Malliajossa käyterttyjen aluetietojen sisältö | Tulostus malliajosta käytetyistä aluetiedoista, joka sisältää Zonedatan muuttujat ja lisäksi malliajossa lasketut välitulokset kotitalouksien koostumuksesta. | Vaihtuva |
| demand_convergence.txt | Konvergenssitunnusluvut | Kunkin iteraation konvergenssitunnusluvut (max_gap, rel_gap). Ks. [Mallijärjestelmän käyttö](mallijarjestelman_kaytto.md). | Yksikötön |
| link_lengths.txt | Linkkipituudet | Linkkien kokonaispituus tietyypeittäin ja ratatyypeittäin osamallin alueella. | km |
| los_validation.txt | Palvelutason tarkistus | Matka-aika, kustannus ja etäisyys valituilla yhteysväleillä (esim. Helsinki–Jyväskylä, Helsinki–Tukholma, Tampere–Turku). Tiedoston unit-sarake kertoo kunkin arvon yksikön. Ks. kohta _Vastukset_ edellä. | h / € / km |
| netfield_links_[osamalli].txt | Auton linkkimatka-ajat | Ruuhkautuneet auton matka-ajat linkeittäin ja ajanjaksoittain. Voidaan tuoda tallennetun nopeuden sijoitteluun. | min |
| purpose_mode_shares.txt | Kulkutapaosuudet matkaryhmittäin | Generoitujen kiertomatkojen kulkutapaosuudet matkaryhmittäin. | Osuus desimaalina 0-1 |
| result_summary.txt | Tulosten yhteenveto | Sijoiteltu kokonaiskysyntä ajanjaksoittain ja sijoitteluluokittain. | Vaihtuva |
| tour_lengths.txt | Kiertomatkojen pituusjakauma | Kiertomatkojen määrä matkaryhmittäin, kulkutavoittain ja pituusluokittain (pituusluokat 0–3 km:stä yli 800 km:iin). | Kiertomatkaa / vrk |
| transit_kms.txt | Joukkoliikenteen suoritteet | Joukkoliikenteen ajoneuvokilometrit ja -tunnit vuorokaudessa ajoneuvotyypeittäin. | km / vrk, h / vrk |
| vehicle_kilometers_by_mode.txt | Suoritteet sijoitteluluokittain | Ajoneuvo- tai henkilökilometrit vuorokaudessa sijoitteluluokittain osamallin alueella. | km / vrk |
| vehicle_kilometers_by_road_class.txt | Suoritteet tietyypeittäin | Ajoneuvokilometrit vuorokaudessa sijoitteluluokittain ja tietyypeittäin (ks. taulukko _Tietyypit_ alla) osamallin alueella. | km / vrk |
| within_zone_tours.txt | Alueen sisäiset kiertomatkat | Sijoittelualueen sisäiset kiertomatkat kulkutavoittain. | Kiertomatkaa / vrk |
| zone_car_ownership.txt | Autonomistus alueittain | Autojen määrä sekä 0, 1 ja 2 auton kotitalouksien osuudet sijoittelualueittain. | Autoa, osuus desimaalina 0-1 |

 _(1) Miller, E. (2020), “Measuring Accessibility: Methods and Issues”, International Transport. Forum Discussion Papers, No. 2020/25, OECD Publishing, Paris._

Aluetasolle aggregoidut tulokset (aggregated_demand) esitetään aluetietojen alueluokituksittain: `municipality`, `county`, `submodel`, `calibration_area` ja `pt_authority` sekä mahdolliset aluetietoihin lisätyt `aggregate_results_<nimi>`-sarakkeet.

*Taulukko x. Tietyypit tulostiedostoissa*

| Koodi | Tietyyppi |
|---|---|
| 1 | Moottoritie |
| 2 | Valtatie / monikaistainen tie |
| 3 | Monikaistainen pääväylä |
| 4 | Pääväylä (yksikaistainen) |
| 5 | Kokooja- ja tonttikatu |
| 11 | Lautta |
| 99 | Syöttölinkki |
| 0 | Linkki ilman autoliikennettä |

__Tavaraliikenteen mallin tulostiedostot:__

| Tiedoston nimi | Kuvaus | Yksikkö |
|---|---|---|
| freight_purpose_summary.txt | Tonnit ja tonnikilometrit hyödykkeittäin ja kuljetustavoittain | t / vuosi, tkm / vuosi |
| freight_zone_summary.txt | Tonnit alueittain, hyödykkeittäin ja kuljetustavoittain | t / vuosi |
| freight_cluster_border_summary.txt | Ulkomaankauppa hyödykkeittäin, ulkomaan klustereittain ja Suomen satamittain tai raja-asemittain | t / vuosi |
| freight_leg2_summary.txt | Ulkomaankauppa hyödykkeittäin, kuljetustavoittain, Suomen satamittain tai raja-asemittain ja ulkomaan satamittain tai raja-asemittain (kuljetuksen kansainvälinen osuus) | t / vuosi |
| freight_domestic_leg_summary.txt | Ulkomaankaupan kuljetusten kotimaan osuudet | t / vuosi, tkm / vuosi |
| freight_vehicle_summary.txt | Ajoneuvojen määrä ja ajoneuvokilometrit kuorma-autotyypeittäin | ajoneuvoa / vrk, ajoneuvo-km / vrk |

__Autonomistusmallin tulostiedostot:__

| Tiedoston nimi | Kuvaus |
|---|---|
| zone_car_ownership_by_segment.txt | Autonomistuksen todennäköisyydet alueittain, kotitaloustyypeittäin ja segmenteittäin |

## Tulosmatriisit

Matriisitiedostot ovat omx. -muodossa. Kysyntämatriisit löytyvät skenaarion tuloskansion kansiosta `demand_matrices\<osamalli>` ja vastusmatriisit (palvelutasomatriisit) kansiosta `los_matrices\<osamalli>`.

[OMX-muotoisia](https://github.com/osPlanning/omx/wiki) matriiseja voi lukea EMMEllä, Pythonilla (`openmatrix`), R:llä ja monilla muilla työkaluilla. Jokainen tiedosto sisältää yhden matriisin sijoitteluluokkaa tai kulkutapaa kohden sekä aluenumerot.

__Matriisit:__

| Tiedoston nimi (jossa xxx on tunnin koodi) | Selite | Tarkempi kuvaus |
|--------------------------------------------|--------|-----------------|
| beeline_.omx | Linnuntie-etäisyys | Sentroidien välinen linnuntie-etäisyys (km). |
| cost_xxx.omx   | Matkakustannus | Matkan kustannus, esim. auton käyttökustannus tai joukkoliikenteen lippuhinta (€). |
| demand_xxx.omx | Kysyntä | Sijoiteltu kysyntä ajanjaksolla sijoitteluluokittain (ajoneuvoa tai henkilöä tunnissa). |
| demand_vrk.omx | Vuorokauden kysyntä | Alueellisissa osamalleissa vuorokauden kysyntä kulkutavoittain molemmat suunnat mukaan lukien; pitkien matkojen mallissa vuorokauden kysyntä sijoitteluluokittain (matkaa / vrk). |
| long_dist_demand_vrk.omx | Pitkien matkojen kysyntä | Alueellisessa ajossa käytetty pitkien matkojen kysyntä osamallin sijoittelualueille aggregoituna (matkaa / vrk). |
| dist_xxx.omx | Matkan pituus | Matkan pituus (km). |
| inv_time_xxx.omx   | Ajoneuvossa vietetty aika | Joukkoliikenteen ajoneuvossa vietetty aika (min). |
| park_cost_xxx.omx   | Pysäköintikustannus | Pysäköintikustannus liityntäpysäköinnissä ja autolla liityttäessä (€). |
| time_xxx.omx   | Matka-aika | Matka-aika; joukkoliikenteellä koettu matka-aika (min). |
| toll_cost_xxx.omx   | Tienkäyttömaksu | Tienkäyttömaksujen kustannus (€). |
| train_users_xxx.omx | Junan käyttö | Junan käyttö joukkoliikennereitillä. |
| logsum_[matkaryhmä]_vrk.omx | Liityntävalinnan logsum | Pitkien matkojen matkaryhmien liityntätavan valinnan logsum-arvot pääkulkutavoittain. Tallentuu kansioon `aggregated_results\<osamalli>\Matrices`. |

__Tavaraliikenteen matriisit__ (kansiossa `demand_matrices\koko_suomi`):

| Tiedoston nimi | Selite | Tarkempi kuvaus |
|---|---|---|
| freight_demand_vrk.omx | Kuorma-autojen kysyntä | Kuorma-autojen vuorokausikysyntä sijoitteluluokittain (`truck`, `semi_trailer`, `trailer_truck`). |
| freight_tons_vrk.omx | Tonnit | Kuljetetut tonnit kuljetustavoittain. |
| freight_demand_tons_vrk.omx | Hyödykekohtaiset tonnit | Tonnit hyödykkeittäin ja kuljetustavoittain; vain parametrilla `--specify-commodity-names` valituille hyödykkeille. |

## Verkkotulokset

Tiedosto `link_results\assignment_results_<osamalli>.gpkg` sisältää skenaarion verkon kaikkine attribuutteineen ajon jälkeen ETRS-TM35FIN-koordinaatistossa. Tiedostossa on tasot
- solmuille
- linkeille
- joukkoliikennesegmenteille
- joukkoliikennelinjoille.

Attribuutteihin sisältyvät kunkin sijoitteluluokan liikennemäärät ajanjaksoittain ja vuorokauden summana network field -attribuutteina (esim. `#icev_aht_volume` ja `#icev_vrk_volume`; auto- ja taksiliityntäluokilla `#<luokka>_<ajanjakso>_transit_leg_volume`), auton matka-ajat sekä joukkoliikenteen matkustajamäärät, nousut ja vaihdot. Tiedoston voi avata suoraan QGISissä tai muussa paikkatieto-ohjelmassa, joten liikennemääräkarttoja voi piirtää ilman EMMEä.

Samat tulokset tallentuvat Emme-skenaarioon (tai erillisiin skenaarioihin, jos ajanjaksojen tallennus erillisiin Emme-skenaarioihin on valittu). Koko vuorokauden tulokset lasketaan tuntituloksista sijoitteluluokittaisilla kiinteillä laajennuskertoimilla.

## Tulosten käsittely ja tulkinta

- Vertaa skenaarioita vain, jos ne on ajettu __samalla malliversiolla__, samalla lähtödatalla ja samoilla kalibrointitiedostoilla.
- Tarkista, että jokainen ajo on konvergoitunut, ja lue lokin varoitukset.
- Vertaa ennusteskenaariota mieluummin vertailuskenaarioon kuin havaintoaineistoon; skenaarioiden väliset erot ovat yleensä luotettavampia kuin absoluuttiset arvot.
- Tarkista tulokset tarkastelualueella yksityiskohtaisesti: linkkien liikennemäärät, matka-ajat ja joukkoliikenteen kuormitukset voivat paljastaa verkon koodausvirheitä.
