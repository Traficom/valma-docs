---
nav_order: 
sort: 
title: Mallijärjestelmän käyttö
---

# Mallijärjestelmän käyttö

<!--Tähän yleisempää mallijärjestelmän käytöstä-->

## Malliajon ohje

1. Lataa tarvitsemasi malliajon tiedot [Sharefilestä](https://traficom.sharefile.eu/home/shared). Pyydä pääsyoikeutta Traficomilta.

   - Aluekohtaiset syöttötiedot: zone_data.
   - Liikenteen hintadata: cost_data (Tähän tiedostoon käyttäjä voi lisätä yleisiä korotuskertoimia sekä alueellisia kulkutapavalinnan kalibrointikertoimia. Lisätietoja saa Traficomilta.).
   - Lähtökysyntämatriisit (zip.) alueellisiin osamalliajoihin: baseline_data.
     
2. Alueellisten osamallien lähtökysyntämatriisien zip. -kansiot tulee purkaa. Sinun tulee myöhemmässä vaiheessa viitata kansioon, jossa on Matrices-niminen kansio. Luo siis kansio, joka sisältää Matrices-kansion. Tämän jälkeen pura tarvitsemasi osamallit Matrices-kansioon niin, että se sisältää kunkin tarvitsemasi alueellisen osamallin mukaan nimetyn kansion. Osamallien kansioissa on vastaavan alueen matriisitiedostot, jotka ovat formaatissa .omx.

3. Koko Suomen ajoihin et tarvitse lähtökysyntämatriiseita, koska osamallit tuovat linkit ja niiden matka-ajat koko Suomen ajoon.
   
4. Lataa tuorein mallijärjestelmä [täältä](https://github.com/Traficom/lem-model-system).
   
5. Luo resurssinhallintaasi projektikansio, jonne VALMA-ajo tallentaa tänne käyttöliittymän projektin asetukset, EMME-projektin ja mallitulokset. Projektikansiossa ei tarvitse olla sisältöä, mutta VALMA ei aja siellä olevien tiedostojen päälle.
   
6. Avaa käyttöliittymä, luo uusi VALMA-projekti ja määrittele sen asetukset:
   - Nimeä projektisi. Vinkki: Nimeä VALMA-projekti saman nimiseksi kuin projektikansiosi.
   - Valitse projektikansioksi resurssinhallintaasi tallentamasi kansio.
   - <!--varmista, miten python toimii muilla käyttäjillä-->
   - Viittaa lataamasi mallijärjestelmän Scripts -kansioon kohdassa Valma Model System. <!--varmista tässäkin, että toimii näin yleisesti-->
   - Viittaa kansioon, joka sisältää Matrices-kansion kohdassa lähtödatan sisältävä kansio.
   - Aseta tarvittaessa kulkutapa- ja suuntautumismallien kalibrointiparametrit (.json) tai kunta-kunta-kalibroinnin tiedosto (.txt). Tiedostojen käytöstä voit lukea lisää täältä. <!--tähän linkki ohjesivuston oikeaan sivuun-->
   - Tallenna asetukset.
  
7. Luo seuraavaksi Emme-pankki käyttöliittymän kautta. Valitse osamalli ja skenaarioiden lukumäärä. Osamallin valinta vaikuttaa tässä vaiheessa vain Emme-pankin kokoon.
   - HUOM:
     - Voit tarvittaessa luoda Emme-projektiin useita pankkeja. Käyttöliittymän kautta pääset esim. luomaan yhden pankin nimeltään "koko_suomi" ja yhden nimeltään "alueelliset_osamallit". Käyttöliittymän ulkopuolella voit tarvittaessa kytkeä useampiakin pankkeja projektiin. Huolehdi siinä tapauksessa siitä, että emme-pankin otsikko on jonkin alueellisen osamallin mukainen (tai "koko_suomi" tai "alueelliset_osamallit").
     - Jos haluat että kaikentyyppiset verkot mahtuvat samaan pankkiin, valitse "Koko Suomi". Jos on tarkoitus luoda monta skenaariota jollekin alueelliselle osamallille, kannattaa kuitenkin luoda pienempi pankki. Koko Suomen verkko voi tarvittaessa olla omassa pankissa.
     - "Tallenna ajanjaksot erillisiin Emme-skenaarioihin" -valinta vaikuttaa ekstra-attribuuttien tilatarpeeseen. Emme-skenaariot tarvitsevat vähemmän ekstra-attribuuttitilaa jos on tarkoitus tallentaa ajanjaksot erillisiin skenaarioihin. Silloin pitää kuitenkin muistaa luoda tarpeeksi skenaarioita (normaalitapauksessa viisi Emme-skenaarioita per Valma-skenaario. Jos on tarkoitus tehdä vain pitkien matkojen ennuste, täppä on mahdollinen laittaa päälle säästäkseen levytilaa vaikka malliajossa olisi tarkoitus käyttää vain yhtä Emme-skenaariota (vrk-sijoitteluihin).
    


