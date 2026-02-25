---
nav_order: 4
sort: 4
---

# Mallijärjestelmän aluetiedot

Aluetiedot ovat sisäänlukutiedoista zonedata niminen gpkg -tiedosto.

__input_zone_id:__ alueen yksilöllinen tunniste.   

__municipality:__ alueen kunnan nimi (merkkijono). Käyttäjän ei tule muuttaa.   

__aggregate_results_municipality:__ kunta, jota käytetään aggregoinnissa/yhteenvedoissa (merkkijono). Käyttäjän ei tule muuttaa.   

__aggregate_results_county:__ maakunta, jota käytetään aggregoinnissa/yhteenvedoissa (merkkijono). Käyttäjän ei tule muuttaa.   

__aggregate_results_subarea:__ osa-alue, jota käytetään aggregoinnissa/yhteenvedoissa (merkkijono). Käyttäjä voi muuttaa.   

__aggregate_results_submodel:__ aggregointiin käytettävän osamallin nimi (merkkijono). Käyttäjän ei tule muuttaa.   

__koko_suomi, ita_suomi, lounais_suomi, pohjois_suomi, uusimaa:__ alueiden ryhmittely eri osamalleissa. Kun ajetaan ”uusimaa”-osamallia, Uudenmaan ulkopuoliset alueet aggregoidaan kunta- tai maakuntatasolle.  

__population:__ alueen asukasluku 31.12. (kokonaislukuna).   

__sh_age_7_17, sh_age_18_29, sh_age_30_49, sh_age_50_64, sh_age_65_99:__ 
   - Väestön ikäjakauman osuudet (desimaali, 0–1). 
   - Mikäli alueella on alle 50 asukasta, ikäryhmien osuudet on imputoitu kunnan keskiarvon perusteella.
   - Vaikuttaa vyöhykkeiden matkojen muodostukseen (matkan tarkoituksen mukaan). Ikäryhmä 7–17 tuottaa koulumatkoja jne.
     
__sh_income_0_19, sh_income_20_39, sh_income_40_59, sh_income_60_79, sh_income_80_99, sh_income_100:___
   - Kotitalouksien osuus tuloluokittain (desimaali, 0–1).
   - 00_19 = Kotitalouden yhteenlasketut ansio- ja pääomatulot 0–19 999 €.
   - 20_39 = Kotitalouden yhteenlasketut ansio- ja pääomatulot 20 000–39 999 €.
   - 40_59 = Kotitalouden yhteenlasketut ansio- ja pääomatulot 40 000–59 999 €.
   - 60_79 = Kotitalouden yhteenlasketut ansio- ja pääomatulot 60 000–79 999 €.
   - 80_99 = Kotitalouden yhteenlasketut ansio- ja pääomatulot 80 000–99 999 €.
   - 100_ = Kotitalouden yhteenlasketut ansio- ja pääomatulot vähintään 100 000 €.
   - Tulotasolla on vaikutus auton omistukseen ja siten kulkutapamalleihin.   

__households:__ ei enää käytössä. Kotitalouksien määrä johdetaan kotitalouskokoluokkien osuuksista ja väestömäärästä.   

__sh_hh1, sh_hh2, sh_hh3:__ kotitalouksien osuus kokoluokittain: 1, 2, 3+ henkilöä (desimaali, 0–1).   

__sh_cars0_hh1 … sh_cars2_hh3:__ kotitalouksien osuus, joilla 0/1/2+ autoa eri kotitalouskokoluokissa (desimaali, 0–1).
  - Muoto: sh_cars{N}_hh{M} → osuus M-henkisistä kotitalouksista, joilla N autoa.   

__land_area:__ alueen maapinta-ala (km²). Laskettu poistamalla vesialue kokonaispinta-alasta.   

__avg_building_distance:__ rakennusten keskimääräinen etäisyys toisistaan (metreinä).
  - Vaikuttaa sisäisen alueen vastukseen kävelylle, pyöräilylle ja autolle → vaikuttaa kulkutapa–kohdevalintaan.

__sh_row_or_detached:__ rivi- tai pientaloasuntojen osuus asunnoista (desimaali, 0–1). Vaikuttaa auton omistukseen.   

__workplaces:__ työpaikkojen määrä alueella (kokonaisluku). Vaikuttaa työmatkojen kohdevalintaan.   

__sh_wrk_healthcare:__ terveys- ja sosiaalipalveluiden (TOL 2008, sektori Q) työpaikkojen osuus. Vaikuttaa asiointimatkojen kohdevalintaan.   

__sh_wrk_shop:__ vähittäiskaupan (TOL G47) työpaikkojen osuus. Vaikuttaa ostosmatkojen kohdevalintaan.   

__sh_wrk_hospitality:__ majoitus- ja ravitsemistoiminnan (TOL I) työpaikkojen osuus. Vaikuttaa vapaa-ajan matkojen kohdevalintaan.   

__sh_wrk_recreation:__ taiteiden, viihteen ja virkistyksen (TOL R) työpaikkojen osuus. Vaikuttaa vapaa-ajan matkoihin.   

__sh_wrk_edu_higher:__ korkea-asteen koulutuksen (P854) työpaikkojen osuus. Vaikuttaa toisen asteen ja korkea-asteen opiskelumatkoihin.   

__sh_wrk_edu_other:__ muiden koulutusalan (P) työpaikkojen osuus. Ei tällä hetkellä käytössä mallissa.   

__sh_office:__
  - Toimistoammateissa työskentelevien osuus (desimaali, 0–1). Vaikuttaa työmatkojen joukkoliikenteen käyttöön — toimistotyöntekijät käyttävät joukkoliikennettä todennäköisemmin.
  - Toimistoammatit (Ammattiluokitus 2010): johtajat, erityisasiantuntijat, asiantuntijat, toimisto- ja asiakaspalvelutyöntekijät, palvelu- ja myyntityöntekijät.

__sport_facility_indoor:__ sisäliikuntapaikkojen pinta-ala (Lipas, JYU 2023).   

__sport_facility_outdoor:__ ulkoliikuntapaikkojen pinta-ala (Lipas, JYU 2023).   

__area_leisure_buildings:__ vapaa-ajan asuntojen pinta-ala (m²).   

__area_university_buildings:__ yliopistorakennusten pinta-ala (m²). Ei käytössä tietosuojahaasteiden vuoksi.   

__avg_park_cost:__ keskimääräinen pysäköintimaksu alueella (€/h).   

__avg_park_time__: keskimääräinen pysäköintiaika + kävelyaika pysäköintiin (min).
  - Laskettu kansallisesti kaavalla: 5,7 + 0,0452 × sqrt(population + workplaces / land_area).

__students_comprehensive:__ perusopetuksen oppilaiden määrä (kokonaisluku). Vaikuttaa perusopetuksen matkojen kohdevalintaan.

__sh_adult_license:__ 18 vuotiaat ja sitä vanhemmat ajokortilliset.
