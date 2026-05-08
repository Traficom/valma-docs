---
nav_order: 5
sort: 5
---

# Selitteet ja käännökset
Alla esitetty mallin kuvaamien matkaryhmien nimet ja selitteet. Matkaryhmä määrittyy lähtöpaikan ja pääasiallisen matkakohteen perusteella.

| Koodi   | Kiertomatkan tyyppi                         |
|---------|---------------------------------------------|
| hb_work    | Kotiperäinen työmatka, jonka pääasiallinen matkakohde on työpaikka.  |
| hb_edu_basic    | Kotiperäinen koulumatka, jonka pääasiallinen matkakohde on koulu ja matkustaja on alle 15 vuotias.  |
| hb_edu_student    | Kotiperäinen opiskelumatka, jonka pääasiallinen matkakohde on opiskelupaikka ja matkustaja on yli 15 vuotias.  |
| hb_grocery | Kotiperäinen päivittäistavaroiden ostosmatka, jonka pääasiallinen matkakohde on päivittäistavarakauppa.  |
| hb_other_shop | Kotiperäinen muu ostos- tai asiointimatka, jonka pääasiallinen matkakohde on kauppakeskus, muu kauppa tai asiointipaikka. Sisältää myös sosiaali- ja terveyspalveluiden asioinnin. |
| hb_leisure | Kotiperäinen vapaa-ajan matka, jonka pääasiallinen matkakohde on ravintola, kahvila, kulttuurikohde tai muu vapaa-ajan kohde.  |
| hb_sport | Kotiperäinen urheilumatka, jonka pääasiallinen matkakohde on liikuntapaikka.  |
| hb_visit | Kotiperäinen vierailumatka, jonka pääasiallinen matkakohde on vierailupaikka ystävien, sukulaisten tai tuttavien luona.  |
| hb_escort | Kotiperäinen saattomatka, jonka pääasiallinen matkakohde on paikka henkilön noutamiseen tai jättöön kyydistä.  |
| hb_business | Kotiperäinen työasiamatka, jonka pääasiallinen matkakohde on työasiointikohde.  |
| hb_overnight | Kotiperäinen yön yli matka, joissa pivän ensimmäinen tai viimeinen matkakohde on ollut hotelli, kesämökki, kakkoskoti tai vierailupaikka. Matka on avoin kiertomatka, eli siltä ei ole palattu kotiin samana päivänä. |
| wb_business | Työperäinen työasiamatka, jolle on lähdetty työpaikalta ja pääasiallinen matkakohde on työasiointikohde.  |
| wb_other | Työperäinen muu matka, jolle on lähdetty työpaikalta ja pääasiallinen matkakohde on muu kuin työasiointikohde. Esimerkiksi työpäivän aikana tehtävät kauppa- tai ravintolavierailut. |
| ob_other |  Ei-kotiperäinen muu matka, jolle on lähdetty pääasiallisesta matkakohteesta. Sisältää muita vierailupaikoista tai vapaa-ajan kohteista käsin tehtäviä matkoja. |

Pääasiallinen matkakohde määritetään kiertomatkan aikana käydyistä paikoista seuraavalla prioriteeteilla:

1) Työpaikka
2) Opiskelupaikka
3) Vierailulupaikka, vapaa-ajan kohde, liikuntakohde
4) Kaupat, saattopaikat

Eli pääasialliseksi kohteeksi katsotaan ensisijaisestityöpaikka tai opiskelupaikka, jos kiertomatkan aikana on käyty näissä kohteissa. Mikäli kiertomatkalla on useampi kohden samalla prioriteetilla, on pääasiallinen kohde se paikka, jossa on vietetty eniten aikaa. 

## Aikajaksot
Malli kuvaa matkavalintoja ja liikennettä vuoden keskimääräisenä päivänä. Poikkeuksena joukkoliikenteen tarjonta kuvaa arkipäivän vuorotarjontaa ja palvelutasoa. Mallin tulosten laajentaminen vuositasolle tapahtuu kertoimella 365.

| Nimi          | Vastine suomeksi                   | Määritelmä |
|---------------|------------------------------------|-------------------|
| AHT          | Aamuhuipputunti | Kellonajat 07:10-08:10 |
| AH          | Aamuhuippu | Kellonajat 06:00-09:00 |
| IHT          | Iltahuipputunti | Kellonajat 16:10-17:10 |
| IH          | Iltahuippu | Kellonajat 15:00-18:00 |
| PT          | Päivätunti | Keskimääräinen päivätunti, joka on joukkoliikenteelle klo 09-15 ja muille kulkutavoille klo 09-15 ja klo 18-22. |
| IT          | Iltatunti  | Käytössä vain joukkoliikenteelle. Kellonajat klo 18-22. |
| VRK   | Vuorokausi | Koko vuorokausi |

## Kulkutavat liikenneverkolla
Alla on esitetty liikenneverkolle sijoiteltavien kulkutapojen nimet ja yksiköt. 

| Nimi          | Vastine suomeksi                   | Sijoitteluyksikkö |
|---------------|------------------------------------|-------------------|
| car          | Henkilöauto | Ajoneuvoa / [vrk/aht/iht/pt] |
| van          | Pakettiauto | Ajoneuvoa / [vrk/aht/iht/pt] |
| bike          | Pyörät | Henkilöä / [vrk/aht/iht/pt] |
| transit   | Joukkoliikenne | Henkilöä / [vrk/aht/iht/pt] |
| walk           | Kävely | Henkilöä / [vrk/aht/iht/pt] |
| airplane           | Lentokone | Henkilöä / [vrk/aht/iht/pt] |

## Kulkutavat kysyntämallissa
Alla on esitetty kysyntämallin kuvaamien kulkutapojen nimet ja yksiköt. 

| Nimi          | Vastine suomeksi                   | Sijoitteluyksikkö |
|---------------|------------------------------------|-------------------|
| car_drv          | Henkilöauto kuljettajana. | Sijoitellaan liikenneverkolle. |
| car_pax          | Henkilöauto matkustajana  | Ei sijoitella liikenneverkolle. |
| bike          | Pyöräily | Sijoitellaan liikenneverkolle. |
| transit   | Joukkoliikenne | Sijoitellaan liikenneverkolle. |
| walk           | Kävely | Ei sijoitella liikenneverkolle. |
| airplane           | Lentokone | Sijoitellaan liikenneverkolle. |
