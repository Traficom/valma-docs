---
nav_order: 5
sort: 5
---

# Malliajojen tulokset

Tulosten tallennuspolku määritellään käyttöliittymän projektiasetuksissa kohdassa projektikansio. Ohjeet projektiasetuksiin löydät [täältä](mallijarjestelman_kaytto.md).
VALMA-skenaarioajojen eli malliajojen tulokset tallentuvat projektikansion alikansioon, jonka nimi vastaa ajetun skenaarion nimeä. Tulokset ovat tekstitiedostoja sekä matriiseja (.omx).

## Malliajon validointi

Malliajoissa käytetään suurta määrää erilaisia lähtötietoja, joten virheet ajoissa ovat tyypillisiä. Suositamme siksi tekemään malliajoille seuraavan validointirutiinin. Tärkein validointi on malliajon tulosten tulkinta, mutta rutiinin avulla voidaan varmistua että malliajossa ei ole ollut suuria virheitä.

### Vastukset
Malliajon tulostiedostoihin tulostuu mallista tiedosto "los_validation.txt", jossa on esitetty matka-ajat ja kustannukset valituille yhteysväleille. Näitä tietoja voi verrata nykytilanteen ajoon, jonka vastaava tiedosto on saatavilla Sharefilesta.
* Tulos ei eri skenaarioita kuvaavissa ajoissa ole välttämättä täysin sama kuin nykytilanteessa, mutta muutoksen tulee olla looginen suhteessa nykytilaan. Mikäli ratahanke nopeuttaa matka-aikaa, ei poikkeaman tulisi olla positiivinen.

### Kulkutapajakauma
Malliajon tulostiedostoihin tulostuu "mode_shares.txt", jossa on esitetty auton ja joukkoliikenteen kulkutapaosuus kunnittain. Sama tieto on saatavilla nykytilan ajoon Sharefilesta. 
* Tulos ei eri skenaarioita kuvaavissa ajoissa ole välttämättä täysin sama kuin nykytilanteessa, mutta muutoksen tulee olla looginen suhteessa nykytilaan. Mikäli joukkoliikenteen palvelutaso paranee, ei poikkeaman tulisi olla negatiivinen.

## Tulostiedostot

Seuraavassa esitetty malliajon tuottamien tulostiedostojen sisältö. 

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

 _(1) Miller, E. (2020), “Measuring Accessibility: Methods and Issues”, International Transport. Forum Discussion Papers, No. 2020/25, OECD Publishing, Paris._

## Tulosmatriisit

Matriisitiedostot ovat omx. -muodossa ja ne löytyvät alikansion kansiosta "Matrices".

__Matriisit:__

| Tiedoston nimi (jossa xxx on tunnin koodi) | Selite | Tarkempi kuvaus |
|--------------------------------------------|--------|-----------------|
| beeline_.omx | |  |
| car_time_xxx.omx | |  |
| cost_xxx.omx   | |  |
| demand_xxx.omx |  |  |
| dist_xxx.omx |  |  |
| inv_time_xxx.omx   |  |  |
| park_cost_xxx.omx   |  |  |
| time_xxx.omx   |  |  |
| toll_cost_xxx.omx   |  |  |
| transfer_time_xxx.omx   |  |  |
