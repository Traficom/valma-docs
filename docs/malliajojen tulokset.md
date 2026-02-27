---
nav_order: 5
sort: 5
---

# Malliajojen tulokset

Tulosten tallennuspolku määritellään käyttöliittymän projektiasetuksissa kohdassa projektikansio. Ohjeet projektiasetuksiin löydät [täältä](mallijarjestelman_kaytto.md).
VALMA-skenaarioajojen eli malliajojen tulokset tallentuvat projektikansion alikansioon, jonka nimi vastaa ajetun skenaarion nimeä. Tulokset ovat tekstitiedostoja sekä matriiseja (.omx).

## Tuloksiin liittyviä epävarmuuksia

<!--täytetään myöhemmin-->

## Tekstitiedostojen kuvaukset

### Tulostiedostojen lyhenteet ja termit

| Koodi | Selite           |
|-------|-----------------|
| hb   |  |
| wb   |  |
| ob    |   |

| Koodi | Selite           |
|-------|-----------------|
| business    |   |
| edu    |   |
| escort    |   |
| grocery    |   |
| other    |   |
| visit    |   |

| Koodi   | Kiertomatkan tyyppi                         |
|---------|---------------------------------------------|
| work    |  |
| leisure |                                  |
| pax |                          |


| Nimi          | Vastine suomeksi                   | Sijoitteluyksikkö |
|---------------|------------------------------------|-------------------|
| car          |                         |           |
| bike          |                          |            |
| transit   |  |            |
| walk           |                         |           |




### Tiedostot

Pitkien matkojen ja osamallien (lyhyiden matkojen) skenaarioden tulostiedosto eivät ole täysin samat. Alla olevaan taulukkoon on merkattu, kuuluuko tulostiedosto vain toisen vai molempien ajojen tuloksiin.

| Tiedoston nimi                               | Selite | Tarkempi kuvaus | Skenaario |
|----------------------------------------------|--------|-----------------|-----------------|
| accessibility.txt                             |  |  |Molemmat |
| aggregated_demand_country/municipality/subarea/submodel.txt |  | | Molemmat |
| aggregated_demand_ykr_km                        |  | | Pitkät |
| car_ownership                            | Kotitalouden autonomistus | hh_lic, cars koostuu kotitaloudesta (hh), jossa voi olla 1 tai 2 aikuista, ajokortillisista henkilöistä (lic), joita voi olla 1 tai 2 sekä kotitalouden autoista, joita voi olla 0, 1 tai 2+.| Osamallit |
| demand_convergence.txt                        |  |  | Molemmat |
| link_lengths.txt                        |  |  | Pitkät |
| municipality_boardings.txt                        |  |  | Pitkät |
|netfield_links_koko_suomi.txt                        |  |  | Pitkät |
| noise_areas.txt                        |  |  | Osamallit |
| purpose_mode_shares.txt                        |  |  | Osamallit |
| result_summary.txt                        |  |  | Pitkät |
| tour_lengths.txt                        |  | | Molemmat |
| transit_kms.txt                        |  |  | Pitkät |
| vehicle_kms_county.txt                        |  | | Pitkät |
| vehicle_kms_vdfs.txt                        |  | | Pitkät |
| vehicle_kms_vdfs_county.txt                        |  | | Pitkät |
| within_zone_tours.txt                        |  | | Molemmat |
| zone_attraction_by_mode/purpose.txt                        |  | | Molemmat |
| zone_attraction_dist_by_mode/purpose.txt                        |  | | Molemmat |
|zone_generation_by_mode/purpose.txt                        |  | | Molemmat |
| zone_generation_dist_by_mode/purpose.txt                        |  | | Molemmat |
| zonedata_input.txt                        |  | | Molemmat |

## Matriisien kuvaukset

Matriisitiedostot ovat omx. -muodossa ja ne löytyvät alikansion kansiosta "Matrices".
Kysyntä- ja vastusmatriisit ovat tuntimatriiseita

| Koodi | Tunti           |
|-------|-----------------|
| aht   | aamuhuipputunti |
| iht   | iltahuipputunti |
| it    | iltapäivätunti  |
| pt    | päivätunti      |

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
