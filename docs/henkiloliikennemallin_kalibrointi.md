---
nav_order: 5
sort: 5
title: Henkilöliikennemallin kalibrointi
---

# Henkilöliikennemallin kalibrointi

Tämä ohje on tarkoitettu tilanteeseen, jossa pitää tehdä tarkastelukohtainen mallikalibrointi.

**Tee kuitenkin aina ensin tarvittavat korjaukset verkkoon ja aluejakoon!**

Huomioi seuraavat _ennen_ kalibrointia:

1. Liikenne- ja matkustajamäärien vertaaminen laskentoihin. Syy poikkeamiin voi olla verkon koodauksessa; esimerkiksi linkin kapasiteetti tai nopeus voi olla virheellinen.
2. Joukkoliikenteen tarkastelussa tulee tarkistaa erityisesti kävelyetäisyydet.
3. Aluejako voi olla liian harva, jolloin sitä tulee tarkentaa.
       - Lisää sentroideja ja konnektoreita Emmeen.
       - Tee vastaavat lisäykset syöttötietoihin (.gpkg).

## Kulkutapa- ja matkakohdevalinnan kalibrointi
   
Kulkutapa- ja matkakohdevalinnan kalibroinnissa *lisätään* vaihtoehtokohtainen komponentti hyötyfunktioon $U$.

Logit-todennäköisyys $\frac{e^{U}}{\sum e^{U}}$ toimii yleisesti niin, että valintajakauma muuttuu suhteellisesti lisäkomponentin $e^{x}$ mukaan. Sen takia karkea arvio lisäkomponentin tarpeen suuruudesta saadaan kaavalla:

$$
\ln\left(\frac{\text{todellisuus}}{\text{kalibroimaton malli}}\right)
$$

> Esim. jos ruuhkatunnin joukkoliikennematkustaminen Helsingin kantakaupunkiin on todellisuudessa 30 % suurempi kuin malli sanoo, sopiva lisäkomponentti on  
> $\ln(1.3) = 0.26$.

Matkakohteen lisäattraktio kohdennetaan johonkin _aggregaatiotasoon_ syöttötiedostoissa (.gpkg). Aggregaatiotaso on sarake nimeltään _aggregate_results_x_, missä _x_ on esimerkiksi _subarea_. Lisäattraktio voidaan kohdentaa myös suoraan sijoittelualueeseen ("zone"). <!--Mitä meinaa?-->

Kalibrointia on hyvä hieman tasoittaa alueellisesti. Esim. jos lisätään attraktiota Helsingin kantakaupunkiin, olisi hyvä hieman lisätä attraktiota Helsingin esikaupunkialueillekin. Muuten malliin saattaa tulla erikoisia rajailmiöitä. Attraktio- ja kulkutapakalibrointi ei lisää kysyntää, vaan kysyntä siirretään tasaisesti kaikista matkakohteista tai kulkutavoista. Tämä tarkoittaa, että jos kalibroitu kulkutapa tai matkakohde muodostaa suuren osan todennäköisyydestä, kalibrointi pitää iteroida saavuttaakseen toivottu lopputulos.

Käyttöliittymässä kalibroinnin lisäkomponentit syötetään Valma-projektiasetuksissa json-formaatissa kohdassa "kulkutapa- ja matkakohdevalinnan kalibrointitiedosto (.json)".

1. Jos jonkin alueen _attraktio_ on pielessä, lisää sitä lisää esimerkiksi näin:
  ```json
  "destination_choice_calibration": {
    "subarea": {
      "Helsingin_kantakaupunki": {
        "transit_work": 0.26,
        "transit_leisure": 0.18
      },
      "Helsingin_esikaupunkialueet": {
        "transit_work": 0.13,
        "transit_leisure": 0.09
      }
    },
    "zone": {
      "202": {
        "car_work": 0.18
      }
    }
  }
```
2. Jos jonkin alueen _kulkutapajakauma_ on pielessä, korota kulkutapakohtaista vakiota näin:
```json
"mode_choice_calibration": {
    "municipality": {
        "Vantaa": {
            "car_work":  0.1
        }
    }
}
```

## Kunta-kunta-kalibrointi

Kunta–kunta‑kalibroinnilla voidaan räätälöidä matkojen suuntautuminen niin, että jokaiselle lähtökunnalle määritetään oma kohdekuntakohtainen kalibrointi. Kalibrointi toimii samalla logiikalla kuin edellä mainittu attraktiokalibrointi. Tällöin vain kunnasta lähtevien matkojen _suuntautuminen_ muuttuu ilman matkojen kokonaismäärän muuttumista. 

Kalibroinnin tiedoston tulee olla sarkaineroteltu tekstitiedosto (.txt). Siinä kahden ensimmäisen sarakeotsikon nimet ovat aina _generation_ ja _attraction_. Seuraavat sarakeotsikot kertovat, mihin kulkutapoihin kalibrointi kohdistuu.

<!--html-taulukko, koska GitHub Pages ei tue taulukoita blockquoten sisällä ja sarakkeet hajoavat.-->

>Esimerkkinä tiedosto, jossa lähtökuntina ovat Espoo ja Kauniainen ja näiden kohdekuntina Helsinki. Kulkutavoiksi on valittu autolla tehtävä työmatka ja pyörä.
><table style="text-align:center;">
><table>
>  <thead>
>    <tr>
>      <th>generation</th>
>      <th>attraction</th>
>      <th>car_work</th>
>      <th>bike</th>
>    </tr>
>  </thead>
>  <tbody>
>    <tr>
>      <td>Espoo</td>
>      <td>Helsinki</td>
>      <td>-0,1</td>
>      <td>0,1</td>
>    </tr>
>    <tr>
>      <td>Kauniainen</td>
>      <td>Helsinki</td>
>      <td>0,1</td>
>      <td>-0,1</td>
>    </tr>
>  </tbody>
></table>

Käyttöliittymässä tekstitiedosto syötetään Valma-projektiasetuksissa txt-formaatissa kohdassa
“kunta-kunta-kalibroinnin tiedosto (.txt)”.
