---
nav_order: 4
sort: 4
title: Malliajon ohjeet
---

# Malliajon ohje

Tässä ohjeessa kerrotaan, mitstä löydät materiaalit malliajoihin ja miten suoritat ne VALMA-käyttöliittymällä.

### Valmistelu

1. Lataa malliajon tiedot [Sharefilestä](https://traficom.sharefile.eu/home/shared) VALMA-lahtotiedot kansiosta. Pyydä pääsyoikeutta Traficomilta.
   - Baseline_data: lähtökysyntämatriisit (zip.) alueellisiin osamalliajoihin.
   - Cost_data: liikenteen hintadata, jossa on ennustevuoden hintataso. (Tähän tiedostoon käyttäjä voi lisätä yleisiä korotuskertoimia sekä alueellisia kulkutapavalinnan kalibrointikertoimia. Lisätietoja saa Traficomilta.).
   - Emme_network: tarkasteluvuotesi EMME-verkot.
   - Zone_data: aluetiedot, jossa on ennustevuoden henkilöliikenteen aluedata-aineisto.
   
2. Lähtökysyntämatriisit:
   - Auleellisten osamallien lähtökysyntämatriisien zip. -kansiot tulee purkaa. Sinun tulee myöhemmässä vaiheessa viitata kansioon, jossa on Matrices-niminen kansio. Luo siis kansio, joka sisältää Matrices-kansion. Pura lähtökysyntämatriisit Matrices-kansioon. Osamallien kansioissa on vastaavan alueen matriisitiedostot, jotka ovat formaatissa .omx.
   - Koko Suomen ajoihin et tarvitse lähtökysyntämatriiseita, koska osamallit tuovat linkit ja niiden matka-ajat koko Suomen ajoon.
   
3. Lataa tuorein mallijärjestelmä [täältä](https://github.com/Traficom/lem-model-system).

4. Luo resurssinhallintaasi projektikansio, jonne VALMA-ajo tallentaa käyttöliittymän projektin asetukset, EMME-projektin ja mallitulokset. Projektikansiossa ei tarvitse olla sisältöä.
   
### VALMA-projekti

1. Avaa käyttöliittymä, luo uusi VALMA-projekti ja määrittele sen asetukset:
   - Nimeä projektisi.
   - Valitse projektikansioksi resurssinhallintaasi tallentamasi kansio.
   - Viittaa lataamasi mallijärjestelmän Scripts -kansioon kohdassa Valma Model System.
   - Viittaa kansioon, joka sisältää Matrices-kansion kohdassa lähtödatan sisältävä kansio.
   - Aseta tarvittaessa kulkutapa- ja suuntautumismallien kalibrointiparametrit (.json) tai kunta-kunta-kalibroinnin tiedosto (.txt). Tiedostojen käytöstä voit lukea lisää [täältä](henkiloliikennemallin_kalibrointi.md).
   - Tallenna asetukset.

2. Luo seuraavaksi Emme-pankki valitsemalla luo emmebank. Valitse osamalli ja skenaarioiden lukumäärä. Osamallin valinta vaikuttaa tässä vaiheessa vain Emme-pankin kokoon.
   > HUOM:
     > - Voit tarvittaessa luoda Emme-projektiin useita pankkeja. Ne voivat olla nimeltään _koko_Suomi_ tai _alueelliset_osamallit_ sekä _ita-suomi_, _uusimaa_, _pohjois-suomi_ tai _lounaus-suomi_ alueellisten osamallien mukaisesti.
   >   - Jos haluat että kaikentyyppiset verkot mahtuvat samaan pankkiin, valitse _koko Suomi_. Jos tarkoitus on luoda monta skenaariota jollekin alueelliselle osamallille, kannattaa luoda pienempi pankki. Koko Suomen verkko voi tarvittaessa olla omassa pankissa.
   >   - Käyttöliittymän ulkopuolella voit tarvittaessa kytkeä useampiakin pankkeja projektiin. Huolehdi siinä tapauksessa siitä, että Emme-pankin otsikko käyttöliittymässä on jonkin alueellisen osamallin mukainen tai _koko_suomi_ tai _alueelliset_osamallit_.
   > - "Tallenna ajanjaksot erillisiin Emme-skenaarioihin" -valinta vaikuttaa ekstra-attribuuttien tilatarpeeseen. Emme-skenaariot tarvitsevat vähemmän ekstra-attribuuttitilaa jos on tarkoitus tallentaa ajanjaksot erillisiin skenaarioihin. Silloin pitää kuitenkin muistaa luoda tarpeeksi skenaarioita (normaalitapauksessa viisi Emme-skenaarioita per Valma-skenaario. Jos on tarkoitus tehdä vain pitkien matkojen ennuste, täppä on mahdollinen laittaa päälle säästäkseen levytilaa vaikka malliajossa olisi tarkoitus käyttää vain yhtä Emme-skenaariota (vrk-sijoitteluihin).
   - Emme-pankin luominen avaa sen EMME-käyttöliittymään.
    
4. Tuo Emme-skenaarioksi lataamasi verkko tai verkot Emme-pankkiin Emmen Modeller Import Scenario työkalun avulla. Kopioi tarvittaessa skenaario Modellerin Copy Scenario työkalun avulla ja tee tarvittavat verkkomuutokset. Jos aiot tallentaa ajanjaksot erillisiin Emme-skenaarioihin, skenaarionumeroiden väliin pitää jättää neljä tyhjää skenaarionumeroa.

### VALMA-skenaariot

1. Luo VALMA-skenaario käyttöliittymässä. Voit luoda henkilöliikenteen pitkien matkojen skenaarion, tavaraliikenteen skenaarion sekä osamallien (lyhyet matkat) skenaariot.
    
__Pitkien matkojen skenaario:__    
          
- Pitkien matkojen skenaariossa tulee käyttää koko Suomen verkkoa. Laita _liikenneverkon sisälävä Emme-skenaario_ numero samaksi kuin luomasi Emme-skenaarion numero.
  - Jos Emme-projektissa on useita Emme-pankkeja, mallijärjestelmä yrittää löytää osamallin mukaan nimetyn Emme-pankin nimeltään "koko_suomi".
- Viittaa lataamaasi aluetietoon (.gpkg) kohdassa syöttötiedot.
- Viittaa lataamaasi hintadataan (.json) kohdassa liikenteen hintadata.
- Osamalli on KoKo Suomi.
- Valitse skenaario ja käynnistä se.

__Tavaraliikenteen skenaario:__

- Viittaa kohdassa "Liikenneverkon sisältävä Emme-skenaario" luomaasi Emme-skenaarioon.
- Viittaa lataamaasi aluekohtaiseen lähtötietoon (.gpkg) kohdassa syöttötiedot, jossa on ennustevuoden tavaraliikenteen aluedata.
- Viittaa lataamaasi hintadataan (.json) kohdassa liikenteen hintadata.
- Viittaa vienti- ja tuontidatassa...
- Tavaraliikenne käyttää automnaattisesti koko Suomen osamallia.

        
__Osamallien (lyhyiden matkojen) skenaario:__

-  Laita _liikenneverkon sisälävä Emme-skenaario_ numero samaksi kuin luomasi Emme-skenaarion numero.
   - Jos projektissa on useita Emme-pankkeja, mallijärjestelmä yrittää löytää osamallin mukaan nimetyn Emme-pankin nimeltään "alueelliset_osamallit". Katso kohta _tallennetun nopeuden sijoittelu_.
- Viittaa lataamaasi aluetietoon (.gpkg) kohdassa syöttötiedot.
- Viittaa lataamaasi hintadataan (.json) kohdassa liikenteen hintadata.
- Pitkien matkojen kysyntäennuste voi tulla projektin lähtödatasta, jolloin valikoi "ota projektin lähtödatasta". Se voi tulla myös erillisestä malliajosta, jolloin valikoi "ota malliajon tuloskansiosta" ja viittaa toisessa Valma-skenaariossa luodun kysyntäennusteen matriisituloskansioon. Tuloskansio löytyy malliajon jälkeen polusta `projektikansio/skenaarion_nimi/Matrices/koko_suomi`. Voit luoda kansion valmiiksi ja viitata siihen, vaikka ajo ei olisi vielä suoritettu.
- Valitse iteraatioiden enimmäismäärä (yleensä 15) tai pelkkä loppusijoittelu.
  - Jos ajat vain loppusijoittelun, kysyntämatriisit tulevat lähtödatasta. Jos haluat, että kysyntämatriisit tulevat projektikohtaisten pohjamatriisien sijaan jo tehdystä Valma-skenraariokohtaisesta kysyntäennusteesta, luo sille skenaariolle uusi aliskenaario. 
- Valitse osamalliksi jokin neljästä alueellisesta osamallista. Jos Emme-projektissa on useita emmepankkeja, mallijärjestelmä yrittää löytää osamallin mukaan nimetyn Emme-pankin tai Emme-pankin nimeltään "alueelliset_osamallit". Käytä Koko Suomen osamallia vain silloin, kun käytät tallennetun nopeuden sijoittelua (koko Suomen ruuhkasijoittelu voi viedä aikaa jopa viikon).

__Tallennetun nopeuden sijoitttelu (koko Suomen koontiajo):__

-  Tallennetun nopeuden sijoittelua tulee käyttää aina koko Suomen osamalliajossa.
-  Sijoittelu valitaan lyhyiden matkojen skenaarioasetusten lisävalinnoista ja se mahdollistaa vaikutusten nopean arvioinnin; perusmalliajon jälkeen voidaan nopeasti arvioida vaikutuksia esim. pienistä muutoksista joukkoliikennetarjonnassa.
-  Sitä voidaan käyttää, jos verkolla on auton linkkimatka-ajat network fiel -attribuuteissa "time_aht", "time_pt" sekä "time_iht. Nämä syntyvät automaattisesti osamallien perusmalliajosta.
-  Tallennetun nopeuden sijoittelu voidaan tehdä kahdella tavalla riippuen, onko sinulla osamallit jo ajettu vai ei.
   - Jos olet jo ajanut alueelliset osamallit ja saanut edellä mainitut linkkimatka-ajat, valikoi pelkästään tallennetun nopeuden sijoittelu.
   - Jos et ole vielä tehnyt alueellisia osamalli-ajoja, tallennetun nopeuden sijoittelulla voidaan myös käynnistää niitä. Valikoi tallennetun nopeuden sijoittelu sekä Emme-skenaarion numero. Numero vastaa asettamasi alueellisen osamallin Emme-skenaarion numeroa. Tällöin malli ajaa osamallit, tuottaa linkkimatka-ajat ja siirtää ne automaattisesti koko Suomen verkolle. Vasta tämän jälkeen se suorittaa koko Suomen malliajon tallennetun nopeuden sijoittelulla.
