---
nav_order: 4
sort: 4
---

# Aluetiedot (Zonedata)
Malli käyttää lähtötietona Zonedata geopackage-tiedostoa, jossa on esitetty maankäytön kuvaus. Aluetiedot koostuvat pakollisista ja vapaaehtoisista sarakkeista.

Pakollisia tietoja ovat mallin käyttämät alueiden hallinnolliset luokitukset ja maankäyttöä kuvaavat tunnusluvut, jotka toimivat kysyntämallien muuttujina. Väestön määrä kertoo matkojen kokonaismääristä, kun taas eri toimialojen työpaikkojen lukumäärä ja koulujen oppilaspaikkojen määrät ohjaavat matkojen suuntautumista.

Vapaaehtoisia aluetietoja ovat "aggregate_results" etuliitteellä esitetyt alueluokitukset. Näitä käytetään vain valmiiden mallitulosten ryhmittelyyn ja ne ovat vapaasti käyttäjän määritettävissä. Lisäämällä aluetietoihin sarakkeen "aggregate_results" etuliitteellä voi käyttäjä saada valmiiksi lasketut matkamäärät tälle samalle jaolle.

## Alueluokitukset
| Kenttä | Kuvaus |
| --- | --- |
| __input_zone_id__ | Alueen yksilöllinen tunniste. |
| __municipality__ | Alueen kunnan nimi. Käyttäjän ei tule muuttaa tätä saraketta. |
| __county__ | Alueen maakunnan nimi. Käyttäjän ei tule muuttaa tätä saraketta. |
| __submodel__ | Alueen osamallin nimi. Käyttäjän ei tule muuttaa tätä saraketta. |
| __koko_suomi__ | Alueiden ryhmittely eri osamalleissa. Kun ajetaan "uusimaa"-osamallia, Uudenmaan ulkopuoliset alueet aggregoidaan kunta- tai maakuntatasolle tämän tiedot avulla. Käyttäjän ei tule muuttaa tätä saraketta. |
| __ita_suomi__ | kts. koko_suomi |
| __lounais_suomi__ | kts. koko_suomi |
| __pohjois_suomi__ | kts. koko_suomi |
| __uusimaa__ | kts. koko_suomi |

## Väestötiedot
| Kenttä | Kuvaus |
| --- | --- |
| __population__ | Alueen asukasluku 31.12. lähtien, kokonaislukuna. |
| __sh_age_7_17__ | Väestön ikäryhmien osuudet desimaalimuodossa 0–1. |
| __sh_age_18_29__ | kts. sh_age_7_17 |
| __sh_age_30_49__ | kts. sh_age_7_17 |
| __sh_age_50_64__ | kts. sh_age_7_17 |
| __sh_age_65_99__ | kts. sh_age_7_17 |
 __sh_adult_license__ | Ajokortillisten osuus 18 vuotta täyttäneistä. |

Ikäryhmien laskennassa ikäryhmien osuudet on imputoitu kunnan keskiarvon perusteella, jos alueella on alle 50 asukasta.
Väestön määrä ja ikäjakauma vaikuttaa ensisijaisesti alueelta lähtevien matkojen lukumäärään. Lisäksi väestön määrä vaikuttaa alueelle saapuvien vierailumatkojen määriin. Ajokortillisten osuutta käytetään muuttujana autonomistusta kuvaavassa mallissa.

## Kotitaloustiedot
| Kenttä | Kuvaus |
| --- | --- |
| __sh_income_0_19__ | Kotitalouksien osuus tuloluokittain desimaalimuodossa 0–1. Tuloluokka on 0–19 999 euroa. |
| __sh_income_20_39__ | Tuloluokka on 20 000–39 999 euroa.  |
| __sh_income_40_59__ | Tuloluokka on 40 000–59 999 euroa.  |
| __sh_income_60_79__ | Tuloluokka on 60 000–79 999 euroa.  |
| __sh_income_80_99__ | Tuloluokka on 80 000–99 999 euroa.  |
| __sh_income_100__ | Tuloluokka on vähintään 100 000 euroa.  |
| __sh_hh1__ | Kotitalouksien osuus kokoluokassa 1 henkilö, desimaalimuodossa 0–1. |
| __sh_hh2__ | Kotitalouksien osuus kokoluokassa 2 henkilöä, desimaalimuodossa 0–1. |
| __sh_hh3__ | Kotitalouksien osuus kokoluokassa 3+ henkilöä, desimaalimuodossa 0–1. |
| __sh_cars0_hh1 … sh_cars2_hh3__ | Kotitalouksien osuudet eri autokokoluokissa: 0, 1 ja 2+ autoa kotitalouskokoluokissa 1, 2 ja 3+. Muoto on sh_cars{N}_hh{M}, eli osuus hhM-kotitalouksista, joilla on N autoa. |

Tulotaso vaikuttaa auton omistukseen ja siten kulkutapamalleihin. Tietoja kotitalouden koostumuksesta käytetään autonomistusta kuvaavassa mallissa.

## Työpaikkatiedot
| Kenttä | Kuvaus |
| --- | --- |
| __workplaces__ | Työpaikkojen määrä alueella kokonaislukuna.  |
| __sh_wrk_healthcare__ | Terveys- ja sosiaalipalveluiden (TOL 2008, sektori Q) työpaikkojen osuus.  |
| __sh_wrk_shop__ | Vähittäiskaupan (TOL G47) työpaikkojen osuus.  |
| __sh_wrk_hospitality__ | Majoitus- ja ravitsemistoiminnan (TOL I) työpaikkojen osuus.  |
| __sh_wrk_recreation__ | Taiteiden, viihteen ja virkistyksen (TOL R) työpaikkojen osuus.  |
| __sh_wrk_edu_higher__ | Korkea-asteen koulutuksen (P854) työpaikkojen osuus. |
| __sh_office__ | Toimistoammateissa työskentelevien osuus desimaalimuodossa 0–1. |

Työpaikkojen lukumäärä vaikuttaa eri tyypisten matkojen määränpään valintaan. Työpaikkojen kokonaismäärä määrittää työmatkojen suuntautumista ja kaupan työpaikkojen lukumäärä ostos- ja asiointimatkojen suuntautumista. Muuttujien käytöstä kysyntämalleissa voi lukea tarkemmin kysyntämallin raportista.

Toimistoammateissa työskentelevien osuus vaikuttaa alueelle saapuvien työmatkojen joukkoliikenteen käyttöön. Toimistoammatit perustuvat Ammattiluokitus 2010 -luokitukseen ja sisältävät johtajat, erityisasiantuntijat, asiantuntijat, toimisto- ja asiakaspalvelutyöntekijät sekä palvelu- ja myyntityöntekijät.

## Muut tiedot
| Kenttä | Kuvaus |
| --- | --- |
| __students_comprehensive__ | Perusopetuksen oppilaiden määrä kokonaislukuna. Luku vaikuttaa perusopetuksen matkojen kohdevalintaan. |
| __sport_facility_indoor__ | Sisäliikuntapaikkojen pinta-ala Lipas-tietojen mukaan (JYU 2023). |
| __sport_facility_outdoor__ | Ulkoliikuntapaikkojen pinta-ala Lipas-tietojen mukaan (JYU 2023). |
| __area_leisure_buildings__ | Vapaa-ajan asuntojen pinta-ala neliömetreinä. |
| __avg_park_cost__ | Keskimääräinen pysäköintimaksu alueella euroina tunnissa. |
| __avg_park_time__ | Keskimääräinen pysäköintiaika plus kävelyaika pysäköintiin minuutteina. Arvo on laskettu kansallisesti kaavalla: 5,7 + 0,0452 × sqrt(population + workplaces / land_area). |
| __land_area__ | Alueen maapinta-ala neliökilometreinä. Lasketaan poistamalla vesialue alueen kokonaispinta-alasta. |
| __avg_building_distance__ | Rakennusten keskimääräinen etäisyys toisistaan metreinä. Määrittää alueen sisäisen vastuksen kävelylle, pyöräilylle ja autolle. |
| __sh_row_or_detached__ | Rivi- tai pientaloasuntojen osuus asunnoista desimaalimuodossa 0–1. |

Pysäköintitiedot vaikuttavat voimakkaasti alueelle saapuvien matkojen kulkutapajakaumaan. Niitä on siksi syytä päivittää alueellisissa malleissa, jos tiedossa on tarkempia tietoja pysäköinnistä.

# Kustannustiedot (Cost)
Aluetietojen lisäksi mallin lähtötiedoksi annetaan kustannustiedot (cost.json), jotka kuvaavat liikkumisen aiheuttamia euromääräisiä kustannuksia eri kulkutavoilla.

| Kenttä | Kuvaus |
| --- | --- |
| __vehicle_km_cost__ | Auton kilometrikustannus vuoden 2025 hintatasossa [eur / km]. Kustannus koostuu polttoainekustannuksista, huoltokustannuksista ja arvon alenemasta. |
| __transit_cost__ | Joukkoliikenteen lippukustannus, joka esitetään kahdessa osassa: nousukohtainen [eur / nousu] ja pituudesta riippuva [eur / km]. |

Auton kilometrikustannus on laskettu valtakunnallisella tasolla perustuen autokannan koostumukseen. Kilometrikustannus vaikuttaa auton kulkutapavalintaan, mutta siinä ei tyypillisesti ole suurta alueellista vaihtelua, joten valtakunnallinen keskiarvo toimii alueellisissa tarkasteluissa hyvin.

Joukkoliikenteen lippukustannus on laskettu valtakunnallisella tasolla erikseen viranomaisalueille hakemalla lippujen hintoja eri pituisille matkoille ja muodostamalla näistä lineaarinen regressiomalli. Hinnat ovat siten likimääräisiä, joten alueellisissa tarkasteluissa lippuhintoja on suositeltavaa tarkentaa todellisilla taksoilla.

