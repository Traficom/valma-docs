---
nav_order: 
sort: 
title: Mallijärjestelmän käyttö
---

# Mallijärjestelmän käyttö

<!--Tähän yleisempää mallijärjestelmän käytöstä-->

## Malliajon ohje

1. Lataa tarvitsemasi malliajon lähtötiedot Sharefilestä<!--(linkki)-->.
   - Aluekohtaiset syöttötiedot; zone_data.
   - Liikenteen hintadata; cost_data (Tähän tiedostoon käyttäjä voi lisätä yleisiä korotuskertoimia sekä alueellisia kulkutapavalinnan kalibrointikertoimia. Lisätietoja saa Traficomilta.).
   - Lähtökysyntämatriisit (zip.) alueellisiin osamalliajoihin; baseline_data.
2. Alueellisten osamallien lähtökysyntämatriisien zip. -kansiot tulee purkaa. Pura tarvitsemasi kansiot Matrices-nimiseen kansioon niin, että Matrices-kansion alla on kansio(ita) nimetty alueellisen osamallin mukaan (esim. lounais_suomi). Matriisitiedostot ovat formaatissa .omx.
