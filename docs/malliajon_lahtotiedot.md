---
nav_order: 4
sort: 4
---

# Aluetiedot (Zonedata)
Malli käyttää lähtötietona Zonedata geopackage-tiedostoa, jossa on esitetty maankäytön kuvaus. Aluetiedot koostuvat pakollisista ja vapaaehtoisista sarakkeista.

Pakollisia tietoja ovat mallin käyttämät alueiden hallinnolliset luokitukset ja maankäyttöä kuvaavat tunnusluvut, jotka toimivat kysyntämallien muuttujina. Väestön määrä kertoo matkojen kokonaismääristä, kun taas eri toimialojen työpaikkojen lukumäärä ja koulujen oppilaspaikkojen määrät ohjaavat matkojen suuntautumista.

Vapaaehtoisia aluetietoja ovat "aggregate_results" etuliitteellä esitetyt alueluokitukset. Näitä käytetään vain valmiiden mallitulosten ryhmittelyyn ja ne ovat vapaasti käyttäjän määritettävissä. Lisäämällä aluetietoihin sarakkeen "aggregate_results" etuliitteellä voi käyttäjä saada valmiiksi lasketut matkamäärät tälle samalle jaolle.

Kaikki tällä sivulla luetellut sarakkeet ovat pakollisia lukuun ottamatta "aggregate_results"-sarakkeita sekä niiden osamallien kohdistussarakkeita, joita ei ajeta. Muut tiedostossa olevat sarakkeet jätetään huomiotta. Traficom tuottaa perusaluetiedot Traficomin Bitbucketissa olevalla skriptillä `prepare-zone-data.R`, joka muuntaa raakadatan mallijärjestelmän muotoon.

## Tiedoston rakenne ja syöttöalueiden kohdistus

Aluetietotiedostossa tulee olla __tasan yksi taso__ (layer). Jokainen rivi on yksi _syöttöalue_. Malli ei käytä geometriaa, mutta sen avulla tietoja on helppo tarkastella ja muokata paikkatieto-ohjelmissa.

Tiedot voidaan antaa osamallien sijoittelualueita tarkemmalla jaolla. Jokaisella rivillä on yksilöllinen `input_zone_id`, ja tiedostossa on jokaiselle osamallille kohdistussarake (`koko_suomi`, `uusimaa`, `lounais_suomi`, `ita_suomi`, `pohjois_suomi`), joka kertoo, mihin sijoittelualueeseen (Emme-sentroidiin) syöttöalue kuuluu kyseisessä osamallissa. Malliajon aikana syöttöalueet aggregoidaan ajettavan osamallin sijoittelualueiksi (ks. kohta _Aggregointi_). Jokaisen verkon sijoittelualueen tulee saada tietoja, ja jokaisen kohdistussarakkeen aluenumeron tulee löytyä verkosta.

Malli pysähtyy virheeseen, jos
- `input_zone_id`-sarakkeessa on tyhjiä tai päällekkäisiä arvoja
- arvo puuttuu, ei ole luku tai on negatiivinen
- osuus on suurempi kuin yksi (toleranssi 0,02)
- kohdistussarakkeen aluenumerot eivät vastaa verkon sentroideja.

Malli antaa varoituksen, jos tiedostoa ei ole järjestetty `input_zone_id`-sarakkeen mukaan.

## Alueluokitukset

| Kenttä | Kuvaus |
|---|---|
| __input_zone_id__ | Alueen yksilöllinen tunniste. Tiedosto tulee järjestää tämän sarakkeen mukaan. |
| __municipality__ | Alueen kunnan nimi. Käyttäjän ei tule muuttaa tätä saraketta. Käytetään koulu- ja saattomatkojen kotikunnan sisäisiä ja ulkopuolisia matkoja kuvaavissa muuttujissa sekä kunta-kunta-kalibroinnissa. |
| __county__ | Alueen maakunnan nimi. Käyttäjän ei tule muuttaa tätä saraketta. Sähköautojen osuudet luetaan maakunnittain kustannustietojen kohdasta `car_shares`. Lapilla (`Lappi`) on joissakin malleissa omat vakionsa. |
| __submodel__ | Alueen osamallin nimi. Käyttäjän ei tule muuttaa tätä saraketta. Käytetään tulosten alueluokituksena. |
| __pt_authority__ | Joukkoliikenteen toimivaltaisen viranomaisen alue (tyhjä, jos alue ei kuulu mihinkään). Alueilla `HSL`, `Tampere`, `Turku` ja `Oulu` on kysyntämalleissa omat vakionsa, esimerkiksi kotiperäisten työmatkojen joukkoliikenteen kulkutapavalinnassa. |
| __calibration_area__ | Kalibrointialue (voi olla tyhjä). Käytetään vain [kalibroinnissa](henkiloliikennemallin_kalibrointi.md). |
| __koko_suomi__ | Alueiden ryhmittely eri osamalleissa. Kun ajetaan "uusimaa"-osamallia, Uudenmaan ulkopuoliset alueet aggregoidaan kunta- tai maakuntatasolle tämän tiedot avulla. Sarakkeen arvo on sen sijoittelualueen (Emme-sentroidin) numero, johon syöttöalue kuuluu osamallissa. Käyttäjän ei tule muuttaa tätä saraketta. |
| __ita_suomi__ | kts. koko_suomi |
| __lounais_suomi__ | kts. koko_suomi |
| __pohjois_suomi__ | kts. koko_suomi |
| __uusimaa__ | kts. koko_suomi |

## Väestötiedot

| Kenttä | Kuvaus |
|---|---|
| __population__ | Alueen asukasluku 31.12. lähtien, kokonaislukuna. |
| __sh_age_7_17__ | Väestön ikäryhmien osuudet desimaalimuodossa 0–1. |
| __sh_age_18_29__ | kts. sh_age_7_17 |
| __sh_age_30_49__ | kts. sh_age_7_17 |
| __sh_age_50_64__ | kts. sh_age_7_17 |
| __sh_age_65_99__ | kts. sh_age_7_17 |
|__sh_adult_license__ | Ajokortillisten osuus 18 vuotta täyttäneistä. |

Ikäryhmien laskennassa ikäryhmien osuudet on imputoitu kunnan keskiarvon perusteella, jos alueella on alle 50 asukasta.
Väestön määrä ja ikäjakauma vaikuttaa ensisijaisesti alueelta lähtevien matkojen lukumäärään. Lisäksi väestön määrä vaikuttaa alueelle saapuvien vierailumatkojen määriin. Ajokortillisten osuutta käytetään muuttujana autonomistusta kuvaavassa mallissa.

## Kotitaloustiedot

| Kenttä | Kuvaus |
|---|---|
| __sh_income_0_19__ | Kotitalouksien osuus tuloluokittain desimaalimuodossa 0–1. Tuloluokka on 0–19 999 euroa. |
| __sh_income_20_39__ | Tuloluokka on 20 000–39 999 euroa.  |
| __sh_income_40_59__ | Tuloluokka on 40 000–59 999 euroa.  |
| __sh_income_60_79__ | Tuloluokka on 60 000–79 999 euroa.  |
| __sh_income_80_99__ | Tuloluokka on 80 000–99 999 euroa.  |
| `sh_income_100_` | Tuloluokka on vähintään 100 000 euroa.  |
| __sh_hh1__ | Kotitalouksien osuus kokoluokassa 1 henkilö, desimaalimuodossa 0–1. |
| __sh_hh2__ | Kotitalouksien osuus kokoluokassa 2 henkilöä, desimaalimuodossa 0–1. |
| __sh_hh3__ | Kotitalouksien osuus kokoluokassa 3+ henkilöä, desimaalimuodossa 0–1. |
| __sh_cars0_hh1 … sh_cars2_hh3__ | Kotitalouksien osuudet eri autokokoluokissa: 0, 1 ja 2+ autoa kotitalouskokoluokissa 1, 2 ja 3+. Muoto on sh_cars{N}_hh{M}, eli osuus hhM-kotitalouksista, joilla on N autoa. Malli ei lue näitä sarakkeita, vaan laskee autonomistuksen autonomistusmallilla. |

Tulotaso vaikuttaa auton omistukseen ja siten kulkutapamalleihin. Tietoja kotitalouden koostumuksesta käytetään autonomistusta kuvaavassa mallissa. Kotitalouksien kokojakaumaa käytetään lisäksi kiertomatkojen generoinnissa ja kulkutapavalinnassa. Tuloluokat kuvaavat kotitalouden yhteenlaskettuja ansio- ja pääomatuloja vuodessa.

Kotitalouksien määrää ei lueta tiedostosta. Malli laskee sen asukasluvusta ja kotitalouksien kokojakaumasta olettaen, että vähintään kolmen hengen kotitalouksien keskikoko on 4,13 henkilöä.

## Työpaikkatiedot

| Kenttä | Kuvaus |
|---|---|
| __workplaces__ | Työpaikkojen määrä alueella kokonaislukuna. Vaikuttaa kotiperäisten työmatkojen ja työasiamatkojen sekä työperäisten työasiamatkojen kohdevalintaan sekä väestön ja työpaikkojen tiheyteen. |
| __sh_wrk_healthcare__ | Terveys- ja sosiaalipalveluiden (TOL 2008, sektori Q) työpaikkojen osuus. Vaikuttaa kotiperäisten muiden ostos- ja asiointimatkojen kohdevalintaan. |
| __sh_wrk_shop__ | Vähittäiskaupan (TOL G47) työpaikkojen osuus. Vaikuttaa kotiperäisten päivittäistavaroiden ostosmatkojen ja muiden ostos- ja asiointimatkojen sekä työperäisten muiden matkojen ja ei-kotiperäisten matkojen kohdevalintaan. |
| __sh_wrk_hospitality__ | Majoitus- ja ravitsemistoiminnan (TOL I) työpaikkojen osuus. Vaikuttaa kotiperäisten vapaa-ajan matkojen ja yön yli -matkojen sekä työperäisten muiden matkojen ja ei-kotiperäisten matkojen kohdevalintaan. |
| __sh_wrk_recreation__ | Taiteiden, viihteen ja virkistyksen (TOL R) työpaikkojen osuus. Vaikuttaa kotiperäisten vapaa-ajan matkojen sekä työperäisten muiden matkojen ja ei-kotiperäisten matkojen kohdevalintaan. |
| __sh_wrk_edu_higher__ | Korkea-asteen koulutuksen (P854) työpaikkojen osuus. Malli ei lue tätä saraketta; korkea-asteen opiskelumatkojen kohdevalinta perustuu sarakkeeseen students_higher_education. |
| __sh_office__ | Toimistoammateissa työskentelevien osuus desimaalimuodossa 0–1. |

Työpaikkojen lukumäärä vaikuttaa eri tyypisten matkojen määränpään valintaan. Työpaikkojen kokonaismäärä määrittää työmatkojen suuntautumista ja kaupan työpaikkojen lukumäärä ostos- ja asiointimatkojen suuntautumista. Muuttujien käytöstä kysyntämalleissa voi lukea tarkemmin kysyntämallin raportista.

Toimistoammateissa työskentelevien osuus vaikuttaa alueelle saapuvien työmatkojen joukkoliikenteen käyttöön. Toimistoammatit perustuvat Ammattiluokitus 2010 -luokitukseen ja sisältävät johtajat, erityisasiantuntijat, asiantuntijat, toimisto- ja asiakaspalvelutyöntekijät sekä palvelu- ja myyntityöntekijät.

TOL 2008 on Tilastokeskuksen toimialaluokitus.

## Muut tiedot

| Kenttä | Kuvaus |
|---|---|
| __students_comprehensive__ | Perusopetuksen oppilaiden määrä kokonaislukuna. Luku vaikuttaa perusopetuksen matkojen kohdevalintaan. Oppilaat lasketaan opiskelupaikan mukaan, ja luku vaikuttaa myös kotiperäisten saattomatkojen kohdevalintaan. |
| __students_upper_secondary__ | Toisen asteen opiskelijoiden määrä opiskelupaikan mukaan kokonaislukuna. Vaikuttaa kotiperäisten opiskelumatkojen kohdevalintaan. |
| __students_higher_education__ | Korkea-asteen opiskelijoiden määrä opiskelupaikan mukaan kokonaislukuna. Vaikuttaa kotiperäisten opiskelumatkojen kohdevalintaan. |
| __sport_facility_indoor__ | Sisäliikuntapaikkojen pinta-ala Lipas-tietojen mukaan (JYU 2023). Vaikuttaa kotiperäisten urheilumatkojen kohdevalintaan. |
| __sport_facility_outdoor__ | Ulkoliikuntapaikkojen pinta-ala Lipas-tietojen mukaan (JYU 2023). Vaikuttaa kotiperäisten urheilumatkojen kohdevalintaan. |
| __area_leisure_buildings__ | Vapaa-ajan asuntojen pinta-ala neliömetreinä. Vaikuttaa kotiperäisten yön yli -matkojen ja vierailumatkojen kohdevalintaan. |
| __car_density__ | Autoja asukasta kohden. Yli yhden arvot rajataan arvoon 1. Malli lukee ja tarkistaa sarakkeen, mutta nykyiset malliparametrit eivät käytä sitä. |
| __avg_park_cost__ | Keskimääräinen pysäköintimaksu alueella euroina tunnissa. Lisätään alueelle suuntautuvien automatkojen kustannukseen kerrottuna aktiviteetin kestolla ja matkustajan itse maksamalla pysäköintikustannuksen osuudella. |
| __avg_park_time__ | Keskimääräinen pysäköintipaikan etsintäaika minuutteina. Lisätään alueelle suuntautuvien automatkojen matka-aikaan. Pysäköintipaikan ja lähtö- tai määräpaikan välinen kävelyaika annetaan erikseen sarakkeessa avg_walk_time. Arvo on laskettu kansallisesti kaavalla: 5,7 + 0,0452 × sqrt(population + workplaces / land_area). |
| __avg_walk_time__ | Keskimääräinen kävelyaika pysäköintipaikan ja lähtö- tai määräpaikan välillä minuutteina. Lisätään automatkojen matka-aikaan matkan molemmissa päissä. |
| __land_area__ | Alueen maapinta-ala neliökilometreinä. Lasketaan poistamalla vesialue alueen kokonaispinta-alasta. Käytetään väestötiheyden (autonomistus) sekä väestön ja työpaikkojen tiheyden (kohdevalinta) laskennassa. |
| __intra_dist_walk__ | Alueen sisäisen kävelymatkan keskimääräinen yhdensuuntainen pituus kilometreinä. Määritetty rakennusten keskinäisistä etäisyyksistä, ja se määrittää alueen sisäisen vastuksen kävelylle. |
| __intra_dist_bike__ | Kuten intra_dist_walk, pyöräilylle. |
| __intra_dist_car__ | Kuten intra_dist_walk, autolle. Alueen sisäinen auton matka-aika lasketaan nopeudella 20 km/h ja kustannus hintadatan kilometrikustannuksella. |
| __sh_row_or_detached__ | Rivi- tai pientaloasuntojen osuus asunnoista desimaalimuodossa 0–1. |

Pysäköintitiedot vaikuttavat voimakkaasti alueelle saapuvien matkojen kulkutapajakaumaan. Niitä on siksi syytä päivittää alueellisissa malleissa, jos tiedossa on tarkempia tietoja pysäköinnistä.

## Aggregointi

Kun syöttöalueet aggregoidaan ajettavan osamallin sijoittelualueiksi, sarakkeet yhdistetään seuraavasti:

| Aggregointitapa | Sarakkeet |
|---|---|
| Summa | population, workplaces, students_comprehensive, students_upper_secondary, students_higher_education, sport_facility_indoor, sport_facility_outdoor, area_leisure_buildings, land_area |
| Asukasluvulla (population) painotettu keskiarvo | sh_age_\*, sh_income_\*, sh_hh1, sh_hh2, sh_hh3, sh_adult_license |
| Työpaikkamäärällä (workplaces) painotettu keskiarvo | sh_wrk_healthcare, sh_wrk_shop, sh_wrk_hospitality, sh_wrk_recreation |
| Keskiarvo | avg_park_cost, avg_park_time, avg_walk_time, car_density, intra_dist_walk, intra_dist_bike, intra_dist_car, sh_office, sh_row_or_detached |
| Ensimmäisen syöttöalueen arvo | municipality, county, submodel, pt_authority, calibration_area, aggregate_results_\* |

# Kustannustiedot (Cost)
Aluetietojen lisäksi mallin lähtötiedoksi annetaan kustannustiedot (cost.json), jotka kuvaavat liikkumisen aiheuttamia euromääräisiä kustannuksia eri kulkutavoilla.

| Kenttä | Kuvaus |
|---|---|
| __vehicle_km_cost__ | Auton kilometrikustannus vuoden 2025 hintatasossa [eur / km]. Kustannus koostuu polttoainekustannuksista, huoltokustannuksista ja arvon alenemasta. |
| __transit_cost__ | Joukkoliikenteen lippukustannus, joka esitetään kahdessa osassa: nousukohtainen [eur / nousu] ja pituudesta riippuva [eur / km]. |
| __vehicle_hour_cost__ | Tavaraliikenteen ajoneuvotyyppien aikaan perustuva kustannus [eur / h]. |
| __car_shares__ | Täyssähköautojen (`bev`) ja lataushybridien (`phev`) osuus autokannasta maakunnittain (aluetietojen `county`-sarake). |
| __cost_changes__ | Kulkutapakohtaiset kustannusten kertoimet kysyntämalleissa. |
| __freight__ | Tavaraliikenteen mallin parametrit hyödykkeiden kustannusryhmittäin. |

Auton kilometrikustannus on laskettu valtakunnallisella tasolla perustuen autokannan koostumukseen. Kilometrikustannus vaikuttaa auton kulkutapavalintaan, mutta siinä ei tyypillisesti ole suurta alueellista vaihtelua, joten valtakunnallinen keskiarvo toimii alueellisissa tarkasteluissa hyvin.

Kilometrikustannus (`vehicle_km_cost`) annetaan erikseen jokaiselle ajoneuvotyypille: henkilöautoille käyttövoimittain (`icev`, `bev`, `phev`), pakettiautoille (`van`), eri kokoisille ja eri käyttövoimaisille kuorma-autoille (esim. `truck`, `truck_ev`, `truck_2n`, `semi_trailer`, `trailer_truck`, `trailer_truck_76t`), tavarajunille (`diesel_train`, `electric_train`) sekä kotimaan vesialuksille (`domestic_vessel`).

Kohdassa `transit_cost` jokaisella hinnoittelualueella tai operaattorilla on tunnus `id`, nousukohtainen hinta `firstb_single` (€) ja kilometrihinta `dist_single` (€/km). Tunnus `id` vastaa joukkoliikennelinjan hinta-id:tä (linja-attribuutti ut1, ks. [EMME-verkon kuvaus](emme_verkko.md)). Esimerkki (hinnat ovat esimerkkiarvoja):

```json
"transit_cost": {
    "HSL":                 {"id": 1, "firstb_single": 2.0, "dist_single": 0.1},
    "kaukojunat":          {"id": 32, "firstb_single": 3.0, "dist_single": 0.3}
}
```

Joukkoliikenteen lippukustannus on laskettu valtakunnallisella tasolla erikseen viranomaisalueille hakemalla lippujen hintoja eri pituisille matkoille ja muodostamalla näistä lineaarinen regressiomalli. Hinnat ovat siten likimääräisiä, joten alueellisissa tarkasteluissa lippuhintoja on suositeltavaa tarkentaa todellisilla taksoilla.

Sähköautojen osuudet annetaan kohdassa `car_shares` maakunnittain. Arvoja `default` käytetään maakunnille, joita ei ole lueteltu. Muiden autojen oletetaan olevan polttomoottoriautoja (`icev`).

```json
"car_shares": {
    "Uusimaa": {"bev": 0.10, "phev": 0.05},
    "default": {"bev": 0.05, "phev": 0.05}
}
```

Kohdassa `cost_changes` voidaan antaa yksittäisten kulkutapojen kustannuksille kertoimia, esimerkiksi auton käyttökustannusten yleisen muutoksen vaikutusten testaamiseksi. Kulkutapojen nimet ovat kysyntämallin kulkutapoja (ks. [Selitteet ja käännökset](selitteet_ja_kaannokset.md)):

```json
"cost_changes": {
    "cost": {"car_driver": 1.0, "car_passenger": 1.0}
}
```

Kohta `freight` sisältää tavaraliikenteen mallin parametrit hyödykkeiden kustannusryhmittäin (esim. `kemiat` kemikaaleille):
- `truck`: tyhjänä ajon osuus, ajoneuvotyyppien jakauma kotimaan ja ulkomaan kuljetuksissa, terminaalikustannukset ja keskikuormat
- `freight_train`: sähköjunien (`_J`) ja dieseljunien (`_D`) aika-, matka- ja terminaalikustannusparametrit
- `ship`: kotimaan vesiliikenteen aika-, matka- ja terminaalikustannusparametrit sekä kanavakustannus
- `foreign_ship`: kontti- ja ro-ro-alusten kustannusparametrit kokoluokittain.

# Muut lähtötiedot

## Tavaraliikenteen aluetiedot

Tavaraliikenteen malli käyttää erillistä GeoPackage-tiedostoa, jonka rakenne on sama kuin henkilöliikenteen aluetiedoissa (yksi taso, `input_zone_id`, osamallien kohdistussarakkeet sekä aluesarakkeet `municipality`, `county`, `submodel`, `calibration_area` ja `pt_authority`). Lisäksi tiedostossa ovat seuraavat muuttujat:

| Kenttä | Kuvaus |
|---|---|
| __gen_\<hyödyke\>__ | Hyödykkeen tuotanto (generaatio) alueella tonneina. |
| __att_\<hyödyke\>__ | Hyödykkeen kulutus (attraktio) alueella tonneina. |
| __lc_area__ | Logistiikkakeskusten pinta-ala. |
| __lc_area_elint__ | Elintarvikkeiden logistiikkakeskusten pinta-ala. |

*Taulukko x. Hyödykeryhmät*

| Koodi | Hyödykeryhmä |
|---|---|
| marita | Maataloustuotteet |
| metsat | Metsätaloustuotteet |
| kalevi | Elintarvikkeiden raaka-aineet |
| krhiil | Kivihiili |
| metkai | Metallimalmit |
| turve | Turve |
| elint | Elintarvikkeet |
| tekst | Tekstiilit |
| puukor | Puutuotteet |
| papsel | Massa |
| pappai | Paperi ja painotuotteet |
| kokbri | Koksi ja briketit |
| oljytu | Jalostetut öljytuotteet |
| oljyru | Muut öljytuotteet |
| kemlaa | Kemikaalit ja lääkkeet |
| kummuo | Kumi- ja muovituotteet |
| minkai | Muut mineraalituotteet |
| rauter | Rauta ja teräs |
| jaloml | Jalostetut metallit |
| mltuot | Metallituotteet |
| elektr | Elektroniikka |
| konela | Koneet ja laitteet |
| majon | Ajoneuvot |
| huonek | Huonekalut |
| jate | Jätteet |

Ulkomaankaupassa mallinnetaan tuontina lisäksi raakaöljy (`rkoljy`) ja maakaasu (`kaasu`).

## Vienti- ja tuontidata

Vienti- ja tuontidata on OMX-tiedosto, joka sisältää hyödykkeittäiset tuonti- ja vientimäärät. Tavaraliikenteen malli käyttää sitä ulkomaankaupan reitinvalinnassa. Tiedosto annetaan tavaraliikenteen skenaarion kohdassa _Vienti- ja tuontidata_.

## Kalibrointitiedostot

Henkilöliikenteen mallin kaksi valinnaista kalibrointitiedostoa, kulkutapa- ja matkakohdevalinnan kalibrointitiedosto (.json) sekä kunta-kunta-kalibroinnin tiedosto (.txt), annetaan projektiasetuksissa, ja ne koskevat kaikkia projektin skenaarioita. Tiedostojen muoto ja käyttö on kuvattu sivulla [Henkilöliikennemallin kalibrointi](henkiloliikennemallin_kalibrointi.md).

## Lähtötietojen vaikutus malliin

- __Autonomistus__ alueittain
  - kotitalouden koko, aikuisten määrä ja ajokortillisuus
  - kotitalouden tulot
  - rivi- ja pientalojen osuus
  - väestötiheys
- __Kiertomatkojen määrä__ alueittain
  - väestö ikäryhmittäin, tuloluokittain ja kotitaloustyypeittäin
  - autonomistus
- __Kulkutavan valinta__
  - alueiden väliset matka-ajat, etäisyydet ja kustannukset autolla, joukkoliikenteellä, pyörällä ja kävellen
  - pysäköintikustannus ja -aika määräpaikassa
  - joukkoliikenteen lippuhinnat ja auton käyttökustannukset (kustannustiedot)
  - autonomistus ja ajokortillisuus
- __Kohteen valinta__
  - kohteen saavutettavuus (aika, etäisyys ja kustannus kulkutavoittain)
  - työpaikat, opiskelijat, liikuntapaikat, vapaa-ajan asunnot ja väestö kohteessa
- __Reitinvalinta__
  - linkkien matka-ajat autolla, pyörällä ja joukkoliikenteellä
  - tienkäyttömaksut ja ajoneuvojen käyttökustannukset
- __Tavaraliikenne__
  - hyödykkeiden tuotanto ja kulutus alueittain
  - ulkomaankaupan määrät
  - tavaraliikenteen kustannukset kuljetustavoittain

## Lähtötietojen muokkaus

- __Aluetietoja__ voi muokata paikkatieto-ohjelmissa, kuten QGISissä, tai Pythonilla (esim. `geopandas`). Pidä tiedostossa vain yksi taso ja varmista, että osuussarakkeiden arvot pysyvät välillä 0–1.
- __Kustannustiedot ja kalibrointitiedostot__ ovat tekstitiedostoja, joita voi muokata millä tahansa tekstieditorilla. Tarkista, että tiedosto on edelleen kelvollista JSONia.
- __Verkkoja__ voi muokata EMMEssä (Network Editor, Modeller tai Prompt) tai suoraan verkkotiedostoissa. Noudata [verkon koodausperiaatteita](emme_verkko.md).

Dokumentoi kaikki lähtötietoihin tehdyt muutokset.

