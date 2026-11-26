---
title: Ajoneuvokannan mallin ohjeistus
---

# Ajoneuvokannan malli
Tällä sivulla kuvataan ajoneuvokannan ajamisen kokonaisprosessi.

## Lähtötiedot ja valmistelevat toimepiteet
Ajoneuvokantamallin osalta kaikki olennaiset skriptit löytyvät [valma-fleet](https://github.com/Traficom/valma-fleet)-reposta. Autonomistuksen tarkempi lähtötieto tuotetaan kuitenkin [valma-model-systemin](https://github.com/Traficom/valma-model-system) avulla. Molemmissa ympäristöissä on käyttössä pipenv, mutta vaatimukset paketeille eroavat hieman, joten ajoneuvokannan osalta suositellaan käyettäväksi omaa ympäristöä. Valma-model-systemillä tehtävien autonomistustulosten ajoo voi käyttää olemassa olevaa ympäristöä, mikä model-system on jo otettu käyttöön.

### Autonomistuksen ajaminen
Autonomistuksen laskenta tehdään zonedata-lähtötietojen avulla, ja se on suositeltavaa tehdä jokaisella saatavissa olevalle poikkileikkausvuodelle. Laskenta tapahtuu seuraavasti:
1. Avaa */Scripts/dev-config.json* -tiedosto ja tarkista, että allamainitut tiedot ovat vastaavasti. Projekti- ja skenaarionimen sekä tuloskansion voi täyttää haluamakseen, se vaikuttaa vain tulosten kansiorakenteeseen.
```json
"SUBMODEL": "koko_suomi",
"ZONE_DATA_FILE": "polku kyseisen vuoden zonedata.gpkg -tiedostoon"
"OPTIONAL_FLAGS": ["DO NOT USE EMME"]
```
2. Kun json on tallennettu, voidaan ajaa */Scripts/valma_cars.py* (huomioi että model-system-pipenv ympäristö on valittu, jotta kaikki pakettiriippuvuudet on huomioitu).
3. Ajon lopputuloksena skenaarionimen mukaisesta results-kansiosta löytyy tiedosto *xone_car_ownership_by_segment.txt*, jota tarvitaan ajoneuvokannan laskennan lähtötietona
4. Kopioi tiedosto talteen tai nimeä se uudelleen (esim. *zone_car_ownership_by_segment_2023.txt*) käytössä olleen zonedatan vuoden mukaisesti.
5. Toista ylläolevat tiedot kaikkien lähtötietovuosien osalta päivittämällä kunkin vuoden .gpkg-lähtötieto ja ajamalla *valma-cars.py* uudelleen. **Mikäli et edellisessä vaiheessa kopioi tai uudelleennimeä tulostiedostoa, kirjoittaa sen seuraavan vuoden ajo sen yli.**
6. Kun kaikki vuodet on ajettu, ota tulostiedostot talteen seuraavaan vaiheeseen.