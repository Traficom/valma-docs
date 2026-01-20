---
nav_order: 
sort: 
title: Mallijärjestelmän käyttö
---

# Mallijärjestelmän käyttö

<!--Tähän yleisempää mallijärjestelmän käytöstä-->

## Malliajon ohje

1. Lataa tarvitsemasi malliajon tiedot [Sharefilestä](https://traficom.sharefile.eu/home/shared). Pyydä pääsyoikeutta Traficomilta.- 
   - Tarkasteluvuotesi EMME-verkot: Emme_network.
   - Aluekohtaiset syöttötiedot, jossa on ennustevuoden henkilöliikenteen aluedata-aineisto: zone_data.
   - Liikenteen hintadata, jossa on ennustevuoden hintataso: cost_data (Tähän tiedostoon käyttäjä voi lisätä yleisiä korotuskertoimia sekä alueellisia kulkutapavalinnan kalibrointikertoimia. Lisätietoja saa Traficomilta.).
   - Lähtökysyntämatriisit (zip.) alueellisiin osamalliajoihin: baseline_data.
     
2. Alueellisten osamallien lähtökysyntämatriisien zip. -kansiot tulee purkaa. Sinun tulee myöhemmässä vaiheessa viitata kansioon, jossa on Matrices-niminen kansio. Luo siis kansio, joka sisältää Matrices-kansion. Tämän jälkeen pura tarvitsemasi osamallit Matrices-kansioon niin, että se sisältää kunkin tarvitsemasi alueellisen osamallin mukaan nimetyn kansion. Osamallien kansioissa on vastaavan alueen matriisitiedostot, jotka ovat formaatissa .omx.

3. Koko Suomen ajoihin et tarvitse lähtökysyntämatriiseita, koska osamallit tuovat linkit ja niiden matka-ajat koko Suomen ajoon.
   
4. Lataa tuorein mallijärjestelmä [täältä](https://github.com/Traficom/lem-model-system).
   
5. Luo resurssinhallintaasi projektikansio, jonne VALMA-ajo tallentaa tänne käyttöliittymän projektin asetukset, EMME-projektin ja mallitulokset. Projektikansiossa ei tarvitse olla sisältöä, mutta VALMA ei aja siellä olevien tiedostojen päälle.
   
6. Avaa käyttöliittymä, luo uusi VALMA-projekti ja määrittele sen asetukset:
   - Nimeä projektisi saman nimiseksi kuin projektikansiosi.
   - Valitse projektikansioksi resurssinhallintaasi tallentamasi kansio.
   - Viittaa lataamasi mallijärjestelmän Scripts -kansioon kohdassa Valma Model System.
   - Viittaa kansioon, joka sisältää Matrices-kansion kohdassa lähtödatan sisältävä kansio.
   - Aseta tarvittaessa kulkutapa- ja suuntautumismallien kalibrointiparametrit (.json) tai kunta-kunta-kalibroinnin tiedosto (.txt). Tiedostojen käytöstä voit lukea lisää täältä. <!--tähän linkki ohjesivuston oikeaan sivuun-->
   - Tallenna asetukset.
  
7. Luo seuraavaksi Emme-pankki käyttöliittymän kautta. Valitse osamalli ja skenaarioiden lukumäärä. Osamallin valinta vaikuttaa tässä vaiheessa vain Emme-pankin kokoon.
   > HUOM:
     > - Voit tarvittaessa luoda Emme-projektiin useita pankkeja. Käyttöliittymän kautta pääset esim. luomaan yhden pankin nimeltään "koko_suomi" ja yhden nimeltään "alueelliset_osamallit". Käyttöliittymän ulkopuolella voit tarvittaessa kytkeä useampiakin pankkeja projektiin. Huolehdi siinä tapauksessa siitä, että Emme-pankin otsikko on jonkin alueellisen osamallin mukainen (tai "koko_suomi" tai "alueelliset_osamallit").
     > - Jos haluat että kaikentyyppiset verkot mahtuvat samaan pankkiin, valitse "Koko Suomi". Jos on tarkoitus luoda monta skenaariota jollekin alueelliselle osamallille, kannattaa kuitenkin luoda pienempi pankki. Koko Suomen verkko voi tarvittaessa olla omassa pankissa.
     > - "Tallenna ajanjaksot erillisiin Emme-skenaarioihin" -valinta vaikuttaa ekstra-attribuuttien tilatarpeeseen. Emme-skenaariot tarvitsevat vähemmän ekstra-attribuuttitilaa jos on tarkoitus tallentaa ajanjaksot erillisiin skenaarioihin. Silloin pitää kuitenkin muistaa luoda tarpeeksi skenaarioita (normaalitapauksessa viisi Emme-skenaarioita per Valma-skenaario. Jos on tarkoitus tehdä vain pitkien matkojen ennuste, täppä on mahdollinen laittaa päälle säästäkseen levytilaa vaikka malliajossa olisi tarkoitus käyttää vain yhtä Emme-skenaariota (vrk-sijoitteluihin).
   - Emme-pankin luominen avaa sen EMME-käyttöliittymään.
    
8. Tuo Emme-skenaarioksi tarvitsemasi verkko tai verkot Emme-pankkiin Emmen Modeller Import Scenario työkalun avulla. Kopioi tarvittaessa skenaario Modellerin Copy Scenario työkalun avulla ja tee tarvittavat verkkomuutokset. Jos aiot tallentaa ajanjaksot erillisiin Emme-skenaarioihin, skenaarionumeroiden väliin pitää jättää neljä tyhjää skenaarionumeroa. <!--miksi ja mitä tarkoittaa?-->

9. Emme-skenaarion luomisen ja verkkojen mahdollisten muokkausten jälkeen luo VALMA-skenaario käyttöliittymässä. Voit luoda henkilöliikenteen pitkien ja lyhyiden matkojen skenaariot sekä tavaraliikenteen skenaarion.
    
   - Pitkien matkojen skenaarion asetukset:
      - Pitkien matkojen skenaariossa tulee käyttää koko Suomen verkkoa. Laita kohdan liikenneverkon sisälävä Emme-skenaario numero samaksi kuin kohdassa 8 luodun Emme-skenaarion numero.
        >- Jos Emme-projektissa on useita Emme-pankkeja, mallijärjestelmä yrittää löytää osamallin mukaan nimetyn Emme-pankin nimeltään "koko_suomi".
      - Viittaa lataamaasi aluekohtaiseen lähtötietoon (.gpkg) kohdassa syöttötiedot.
      - Viittaa lataamaasi hintadataan (.json) kohdassa liikenteen hintadata.
      - Osamalli on KoKo Suomi.
      - <!--Mitä ovat sijoittelun strategiatiedostot?-->
        
   - Lyhyiden matkojen skenaarion asetukset:
     -  Laita kohdan liikenneverkon sisälävä Emme-skenaario numero samaksi kuin kohdassa 8 luodun Emme-skenaarion numero.
     > - Jos projektissa on useita Emme-pankkeja, mallijärjestelmä yrittää löytää osamallin mukaan nimetyn Emme-pankin nimeltään "alueelliset_osamallit". Katso kohta ##vi.
     - Viittaa lataamaasi aluekohtaiseen lähtötietoon (.gpkg) kohdassa syöttötiedot.
     - Viittaa lataamaasi hintadataan (.json) kohdassa liikenteen hintadata.
     - Pitkien matkojen kysyntäennuste voi tulla projektin lähtödatasta, jolloin valikoi "ota projektin lähtödatasta". Se voi tulla myös erillisestä malliajosta, jolloin valikoi "ota malliajon tuloskansiosta" ja viittaa toisessa Valma-skenaariossa luodun kysyntäennusteen matriisituloskansioon. Tuloskansio löytyy malliajon jälkeen polusta projektikansio/skenaarion_nimi/Matrices/koko_suomi. Voit luoda kansion valmiiksi ja viitata siihen, vaikka ajo ei olisi vielä suoritettu.
     - Valitse iteraatioiden enimmäismäärä tai pelkkä loppusijoittelu.
      >- Jos ajat vain loppusijoittelun, kysyntämatriisit tulevat lähtödatasta. Jos haluat, että kysyntämatriisit tulevat projektikohtaisten pohjamatriisien sijaan jo tehdystä Valma-skenraariokohtaisesta kysyntäennusteesta, luo sille skenaariolle uusi aliskenaario.
      >- aliskenaarion luominen: 
     - Valitse osamalliksi jokin neljästä alueellisesta osamallista sen mukaan, minkä liikenneverkon sisältävän EMME-skenaarion valitsit. Käytä Koko Suomen osamallia vain silloin, kun käytät tallennetun nopeuden sijoittelua (koko Suomen ruuhkasijoittelu voi viedä aikaa jopa viikon).
       >-  Tallennetun nopeuden sijoittelu mahdollistaa vaikutusten nopean arvioinnin ja se valitaan lisävalinnoista. Sitä voidaan käyttää, jos verkolla on auton linkkimatka-ajat network fiel -attribuuteissa "time_aht", "time_pt" sekä "time_iht (entä time_it). Nämä syntyvät automaattisesti osamallien perusmalliajosta.
       >-  Jos ajat koko Suomen osamallin tallennetun nopeuden sijoittelussa, valitse pelkästään tallennetun nopeude sijoittelu. Huomioi, että tarvitset edellä mainitut linkkimatka-ajat, jotka ajo osaa hakea automaattisesti kansioistasi.
       >- Tallennetun nopeuden sijoittelussa voidaan myös käynnistää alueellisia osamalliajoja, joiden ruuhkamatka-aikoja voidaan käyttää koko Suomen verkolla. Valitse käyttöliittymästä tallennettu nopeus sekä valikoi alueen Emme-skenaarion numeroksi asettamasi alueellisen osamallin Emme-skenaarion numero. Tällöin tallennetut matka-ajat siirtyvät automaattisesti koko Suomen verkolle _ennen??_ tallennetun nopeuden sijoittelua / ennen skenaarioajoa.
 
    - Tavaraliikenteen skenaarion asetukset:
      - Viittaa kohdassa "Liikenneverkon sisältävä Emme-skenaario" luomaasi Emme-skenaarioon.
      - Viittaa lataamaasi aluekohtaiseen lähtötietoon (.gpkg) kohdassa syöttötiedot, jossa on ennustevuoden tavaraliikenteen aluedata.
      - Viittaa lataamaasi hintadataan (.json) kohdassa liikenteen hintadata.
      - Viittaa vienti- ja tuontidatassa...
      - Tavaraliikenne käyttää automnaattisesti koko Suomen osamallia.
   

