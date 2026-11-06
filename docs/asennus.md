---
nav_order: 1
sort: 1
title: Käyttöliittymän asennus
---

# Asennus

Ohjeessa kuvataan Bentleyn OpenPaths EMME -ohjelmiston, VALMA-käyttöliittymän sekä VALMA-mallijärjestelmän asennus.

Mallijärjestelmää voi käyttää myös ilman käyttöliittymää komentoriviltä. Tästä kerrotaan sivun lopussa sekä [mallijärjestelmän käyttöohjeessa](mallijarjestelman_kaytto.md).

## EMME-ohjelmiston asennus

VALMA UI -käyttöliittymän käyttö edellyttää EMME‑ohjelmistoa, tunnuksia ja lisenssiä.

Voit hankkia nämä [Bentleyn nettisivuilta](https://www.bentley.com/software/openpaths/).
- Tarkemmat ohjeet ohjelmiston asentamiseen löydät [täältä](https://docs.bentley.com/LiveContent/web/OpenPaths%20Help-v1/en/GUID-91E9693E-4255-48EE-B011-27E105B8CD57.html).

Mallijärjestelmä on kehitetty **EMME 24** -versiolle ja sen mukana asentuvalle **Python 3.11** -tulkille. VALMA käyttää EMMEn mukana asentuvia Python-kirjastoja, joten muita ohjelmia ei tarvitse asentaa.

Kun EMME on asennettu ja lisenssi aktivoitu, lisää EMMEn ohjelmat ja Python käyttäjän `PATH`-ympäristömuuttujaan:

1. Avaa Windowsin Ohjauspaneeli.
2. Valitse *Käyttäjätilit* (User Accounts), napsauta uudelleen *Käyttäjätilit* ja valitse vasemman reunan valikosta ympäristömuuttujien muokkaus (*Change my environment variables*).
3. Valitse ylemmästä laatikosta (*User variables for USERNAME*) muuttuja `Path` ja napsauta *Muokkaa…* (Edit…).
4. Lisää *Uusi*-painikkeella (New) seuraavat kolme riviä:
   - `%EMMEPATH%\Programs`
   - `%EMMEPATH%\Python311`
   - `%EMMEPATH%\Python311\Scripts`
5. Hyväksy muutokset *OK*-painikkeella sekä ympäristömuuttujan muokkausikkunassa että ympäristömuuttujaikkunassa.

## VALMA-käyttöliittymän asennus

Käyttöliittymän asennustiedosto ladataan GitHubista Liikenne- ja viestintävirasto Traficomin valma-ui-repositorion [Releases-sivulta](https://github.com/Traficom/valma-ui/releases). Asennustiedosto on nimeltään `VALMA-x.y.z.Setup.exe`, missä `x.y.z` on käyttöliittymän versionumero (esimerkiksi `VALMA-1.2.6.Setup.exe`). Samalla sivulla on myös zip-versio (`VALMA-win32-x64-x.y.z.zip`). Käyttöliittymällä voidaan käyttää mallijärjestelmän eri versioita, mutta suosittelemme käyttämään uusinta versiota.

> HUOM: Sovellus asennetaan niin harvoin, että Windows tai selain saattaa varoittaa siitä ja estää asennuksen. Eston voi ohittaa usealla tavalla, ja saatat joutua käyttämään useampaa niistä:
> - Kun lataat tiedostoa, valitse *Säilytä silti* (Keep anyway), jos selain ei tallenna tiedostoa automaattisesti.
> - Kun avaat asennustiedoston, valitse varoituksesta *Lisätietoja* (More info) ja sen jälkeen *Suorita silti* (Run anyway).
> - Napsauta ladattua `.exe`-tiedostoa hiiren oikealla painikkeella, valitse *Ominaisuudet* (Properties) ja rastita *Poista esto* (Unblock).

Sovellus asentuu käyttäjän `AppData`-kansioon: itse sovellus kansioon `AppData\Local` ja sen asetukset kansioon `AppData\Roaming`.

Kun sovellus käynnistetään ensimmäisen kerran, se yrittää löytää koneelta EMME-asennuksen ja sen Python-tulkin. Jos Python-polkua ei löydy automaattisesti, aseta se projektiasetusten kohtaan *Emme Python v311* (ks. [Mallijärjestelmän käyttö](mallijarjestelman_kaytto.md)). Tulkki on yleensä `%EMMEPATH%\Python311\python.exe`.

## VALMA-mallijärjestelmän asennus

Mallijärjestelmä koostuu mallijärjestelmän repositorion `Scripts`-kansion Python-skripteistä. Mallijärjestelmän voi asentaa kahdella tavalla.

__Käyttöliittymän kautta:__ Valitse projektiasetusten kohdassa *valma model system* painike *Lataa eri versio internetistä* ja valitse haluamasi versio. Käyttöliittymä lataa version GitHubista, purkaa sen käyttäjän kotikansioon ja asettaa sen `Scripts`-kansion projektin mallijärjestelmäksi.

__Käsin:__

1. Avaa [mallijärjestelmän repositorio](https://github.com/Traficom/valma-model-system) ja valitse käytettävä versio (julkaisu tai haara, esimerkiksi `dev`).
2. Lataa repositorio zip-tiedostona (*Code → Download ZIP*) ja pura se omalle koneellesi, tai kloonaa repositorio Gitillä.
3. Viittaa käyttöliittymän projektiasetuksissa ladatun mallijärjestelmän `Scripts`-kansioon kohdassa *valma model system* (ks. [Mallijärjestelmän käyttö](mallijarjestelman_kaytto.md)).

Aina kun mallijärjestelmän kansio vaihtuu, käyttöliittymä asentaa mallijärjestelmän tarvitsemat Python-kirjastot (`Scripts\requirements.txt`) EMMEn Python-tulkin pip-ohjelmalla. Jos pip-ohjelmaa tai `requirements.txt`-tiedostoa ei löydy, käyttöliittymä antaa virheilmoituksen (_pip.exe-sovellusta ei löydy sijainnista …_ tai _Tarvittavaa requirements.txt-tiedostoa ei löydy sijainnista …_). Tarkista silloin Python-polku ja mallijärjestelmän kansio.

> HUOM: Kirjaa aina ylös, mitä mallijärjestelmän versiota malliajossa käytettiin. Käyttöliittymästä ajettujen henkilöliikenteen ajojen lokitiedostoon tallentuu rivi `lem_version=…`, mutta oikea versio näkyy siinä vain, jos mallijärjestelmä on kloonattu Gitillä. Zip-tiedostona ladatun mallijärjestelmän lokissa versio on `v0.0.1`. Komentoriviltä oletuslokitasolla (`INFO`) ajettujen ajojen ja tavaraliikenteen mallin lokeihin versiota ei tallennu.

## Asennuksen testaaminen

EMME-yhteyden voi testata ilman projektiaineistoja. Avaa komentokehote mallijärjestelmän `Scripts`-kansiossa ja aja:

```
python -m tests.emme_only.test_assignment
```

Komento luo pienen EMME-testiverkon ja ajaa sillä testisijoittelut. Jos komento päättyy ilman virheitä, EMME ja sen Python-kirjastot on asennettu oikein.

## Käyttö ilman käyttöliittymää

Kokeneet käyttäjät voivat ajaa mallijärjestelmää suoraan komentoriviltä. Asennus tehdään kuten edellä, mutta ilman VALMA-käyttöliittymää. Ajon asetukset annetaan tällöin asetustiedostossa tai komentoriviparametreina (ks. [Mallijärjestelmän käyttö](mallijarjestelman_kaytto.md)).

Mallijärjestelmää voi ajaa myös ilman EMME-lisenssiä niin sanotulla mock-sijoittelulla, joka lukee valmiiksi lasketut vastusmatriisit sijoittelujen sijaan. Tämä on tarkoitettu vain testaukseen ja kehitystyöhön, eikä se tuota käyttökelpoisia ennusteita.

## Ohjeet mallin kehittämiseen

1. Lataa ja asenna [git](https://git-scm.com/). Kloonaa [mallijärjestelmän repositorio](https://github.com/Traficom/valma-model-system) omalle koneellesi.

   > HUOM: Traficomin kehittäjäkoneelle voi luoda GitHubin kanssa synkronoidun git-ympäristön (myös IkkunaVPN:n ollessa päällä), kun gitiin tehdään ensin seuraavat asetukset:
   >
   > ```
   > git config --global http.proxy "proxy.vpn.ikkuna.local:8080"
   > git config --global http.sslBackend schannel
   > ```
   >
   > Kun paikallinen repositorio on luotu, proxy-asetuksen voi rajata koskemaan vain sitä:
   >
   > ```
   > git config --global http.proxy ""
   > git config http.proxy "proxy.vpn.ikkuna.local:8080"
   > ```
   >
   > Jos haluat käyttää *samassa repositoriossa* useita remoteja, joista yksi on Traficomin sisäverkon Bitbucket (nimeltään esimerkiksi `bitbucket`), voit asettaa:
   >
   > ```
   > git config remote.bitbucket.proxy ""
   > ```

2. Noudata [mallijärjestelmän README-tiedoston](https://github.com/Traficom/valma-model-system/blob/main/README.md) ohjeita.
