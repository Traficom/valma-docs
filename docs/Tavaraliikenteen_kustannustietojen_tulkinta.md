# **Kustannustiedoston tulkinta tavaraliikenteen osalta**
Tavaraliikenteen kuljetuskustannusten kustannusfunktioiden komponentit löytyvät mallin lähtötietona json-tiedostosta. Samaan tiedostoon sisältyy sekä henkilöliikenteen- että tavaraliikenteen yksikkökustannukset. Tässä tiedostossa käydään läpi kustannustiedoston (json) sisältöä ja tiedostosta löytyviä tavaraliikennemallin kuljetuskustannusten laskentaan vaikuttavia yksikkökustannuksia/kustannuskomponentteja. 

Huomionarvoista on, että tiedoston kustannuskomponentit vastaavat muuten kappaleissa tavaraliikennemallin dokumentaatiossa esitettyjä yksikkökustannuksia, mutta hallintokulujen kerroin ei ole mukana tieliikenteen kustannuksissa, vaan se huomioidaan vasta mallijärjestelmän laskennassa.

Kustannustiedostoon sisältyvien tavararyhmien (12 tavararyhmää = estimointiryhmittely) selitteet löytyvät taulukosta 1. 

*Taulukko 1. Kustannustiedostosta löytyvät tavararyhmien (estimointiryhmittely) selitteet*
| Tavararyhmän lyhenne | Tavararyhmän selite |
|---------------|---------|
| mameka      | Maatalous, metsästys ja kalastus |
| metsat | Metsätalous |
| energy | Kivihiili, raakaöljy, maakaasu, turve, koksi, briketit |
| kaivan | Kaivannaiset, raakamineraalit sekä ei-metalliset mineraalituotteet |
| elint | Elintarvikkeet |
| tekst | Tekstiilit, kankaat ja nahat |
| puukor | Puu- ja korkkituotteet |
| papsel | Paperi, kartonki, sellu |
| oljytu | Jalostetut öljytuotteet |
| kemiat | Metallit, koneet ja laitteet |
| jate | Jätteet |

Tiedostoon sisältyvien kuljetusmuotojen ja -tyyppien mallissa käytetyt nimet ja selitteet löytyvät taulukoista 2-4.

*Taulukko 2. Kustannustiedostosta löytyvät ajoneuvoluokat tieliikenteelle*
| Ajoneuvoluokka | Nimi kustannustiedostossa |
|---------------|---------|
| Kuorma-auto, N2 (<12t)  | truck_2n |
| Kuorma-auto, KAIP (12 t - ~40t) | truck |
| Puoliperävaunuyhdist. KAPP (~40t) | semi_trailer |
| Täysperävaunuyhdist, KATP (<64t) | trailer-truck |
| HCT-rekka, HCT (<76t)  | trailer_truck_76t |

*Taulukko 3. Kustannustiedostosta löytyvät ajoneuvoluokat rautatieliikenteelle*
| Ajoneuvoluokka | Nimi kustannustiedostossa |
|---------------|---------|
| Sähköjuna | freight_train_J |
| Dieseljuna | freight_train_D |

*Taulukko 4. Kustannustiedostosta löytyvät ajoneuvoluokat laivaliikenteelle*
| Ajoneuvoluokka | Nimi kustannustiedostossa |
|---------------|---------|
| Konttilaiva | container_ship |
| RoRo / RoPax | roro_vessel |
| Kuivalasti / irtolasti | general_cargo |
| Öljytankkeri | oil_tanker |
| Tuotesäiliölaiva | product_tanker |
| LNG säiliölaiva | lng_carrier |
| Kotimaan laivaliikenne | ship_W |


Kustannustiedoston parametrit muuttuvat ennustevuoden mukaan. Esimerkiksi käyttövoiman hinta muuttuu ennustettavan vuoden mukaan ja sähköautojen osuus kannassa samaten. ***Eri ennustevuosille tarvitaan näin ollen erilliset kustannustiedostot.*** 
