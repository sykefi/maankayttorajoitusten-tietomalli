---
layout: "default"
title: "Looginen tietomalli - looginen tietomalli - dokumentaatio"
description: ""
id: "dokumentaatio"
status: "Luonnos"
---
# Loogisen tason maankäyttörajoitukset
{:.no_toc}

1. 
{:toc}

## Yleistä

Loogisen tason tietomalli määrittelee kaikille maankäyttörajoitusten kohteille yhteiset tietorakenteet, joita sovelletaan maankäyttörajoitusten ilmaisemiseen laadittujen [soveltamisohjeiden](../soveltamisohjeet/) ja niihin kiinnittyvien koodistojen sekä [elinkaari-](../elinkaarisaannot.html) ja [laatusääntöjen](../laatusaannot.html) mukaisesti. Looginen tietomalli pyrkii olemaan mahdollisimman riippumaton tietystä toteutusteknologiasta tai tiedon fyysisestä esitystavasta.

<!--**Graafinen mallinnus loogisesta tietomallista**

![Tonttijakosuunnitelman looginen malli graafisena mallinnuksena](looginenmalli.png "Looginen tietomalli -  graafinen mallinnus (Neo4j)")

(Lataa [Kaavio määritelmien kanssa](looginenmalli.png))-->

### Normatiiviset viittaukset
Tietomallit hyödyntävät samoja normatiivisia viittauksia kuin muutkin Ryhti-hankkeen tietomallit. Ne käsittävät seuraavat dokumentit:

* [ISO 639-2:1998 Codes for the representation of names of languages — Part 2: Alpha-3 code][ISO-639-2]
* [ISO 8601-1:2019 Date and time — Representations for information interchange — Part 1: Basic rules][ISO-8601-1]
* [ISO 19103:2015 Geographic information — Conceptual schema language][ISO-19103]
* [ISO 19107:2019 Geographic information — Spatial schema][ISO-19107]
* [ISO 19108:2002 Geographic information — Temporal schema][ISO-19108]
* [ISO 19109:2015 Geographic information — Rules for application schema][ISO-19109]
* [ISO 19505-2:ISO/IEC 19505-2:2012, Information technology — Object Management Group Unified Modeling Language (OMG UML) — Part 2: Superstructure][ISO-19505-2]

### Standardienmukaisuus

Tietomallien looginen tietomalli perustuu [ISO 19109][ISO-19109]-standardin yleiseen kohdetietomalliin (General Feature Model, GFM), joka määrittelee rakennuspalikat paikkatiedon ISO-standardiperheen mukaisten sovellusskeemojen määrittelyyn. GFM kuvaa muun muassa metaluokat ```FeatureType```, ```AttributeType``` ja ```FeatureAssociationType```. 

Tietomalleissa kaikki tietokohteet, joilla on tunnus ja jotka voivat esiintyä erillään toisista kohteista on määritelty kohdetyypeinä stereotyypin ```FeatureType``` kautta. Sellaiset tietokohteet, joilla ei ole omaa tunnusta ja jotka voivat esiintyä vain kohdetyyppien attribuuttien arvoina on määritelty [ISO 19103][ISO-19103]-standardin ```DataType```-stereotyypin avulla. Lisäksi [HallinnollinenAlue](#hallinnollinenalue) ja [Organisaatio](#organisaatio) on mallinnettu vain rajapintojen (```Interface```) avulla, koska niitä ei ole tarpeen kuvata maankäyttörajoitusten tietomallissa yksityiskohtaisesti, ja on todennäköistä, että suunnitelmia ylläpitävät tietojärjestelmät tarjoavat niille konkreettiset toteuttavat luokat.

[ISO 19109][ISO-19109] -standardin lisäksi tietomallit perustuvat muihin paikkatiedon ISO-standardeihin, joista keskeisimpiä ovat [ISO 19103][ISO-19103] (UML-kielen käyttö paikkatietojen mallinnuksessa), [ISO 19107][ISO-19107] (sijaintitiedon mallintaminen) ja [ISO 19108][ISO-19108] (aikaan sidotun tiedon mallintaminen).

### Muualla määritellyt luokat ja tietotyypit

#### CharacterString

Kuvaa yleisen merkkijonon, joka koostuu 0..* merkistä, merkkijonon pituudesta, merkistökoodista ja maksimipituudesta. Määritelty rajapinta-tyyppisenä [ISO 19103][ISO-19103]-standardissa.

#### LanguageString

Kuvaa kielikohtaisen merkkijonon. Laajentaa CharacterString-rajapintaa lisäämällä siihen language-attribuutin, jonka arvo on LanguageCode-koodiston arvo. Kielikoodi voi [ISO 19103][ISO-19103]-standardin määritelmän mukaan olla mikä tahansa ISO 639 -standardin osa.

#### Number

Kuvaa yleisen numeroarvon, joka voi olla kokonaisluku, desimaaliluku tai liukuluku. Määritelty rajapintana [ISO 19103][ISO-19103]-standardissa.

#### Integer

Laajentaa Number-rajapintaa kuvaamaan numeron, joka on kokonaisluku ilman murto- tai desimaaliosaa. Määritelty rajapintana [ISO 19103][ISO-19103]-standardissa.

#### Decimal

Laajentaa [Number](#number)-rajapintaa kuvaamaan numeron, joka on desimaaliluku. Decimal-rajapinnan toteuttava numero voidaan ilmaista virheettä yhden kymmenysosan tarkkuudella. Määritelty rajapintana [ISO 19103][ISO-19103]-standardissa. Decimal-numeroita käytetään, kun desimaalien käsittelyn tulee olla tarkkaa, esim. rahaan liityvissä tehtävissä.

#### Real

Laajentaa [Number](#number)-rajapintaa kuvaamaan numeron, joka on tarkkudeltaan rajoitettu liukuluku. Real-rajapinnan numero voi ilmaista tarkasti vain luvut, jotka ovat 1/2:n (puolen) potensseja. Määritelty rajapintana [ISO 19103][ISO-19103]-standardissa. Käytännössä esitystarkkuus riippuu numeron tallentamiseen varattujen bittien määrästä, esim. ```float (32-bittinen)``` (tarkkuus 7 desimaalia) ja ```double (64-bittinen)``` (tarkkuus 15 desimaalia).

#### TM_Object

Aikamääreiden yhteinen yläluokka, jota käytetään, mikäli arvo voi olla joko yksittäinen ajanhetki tai aikaväli. Määritelty luokkana [ISO 19108][ISO-19108]-standardissa. 

#### TM_Instant

Kuvaa yksittäisen ajanhetken 0-ulotteisena ajan geometriana, joka vastaa pistettä avaruudessa. Määritelty luokkana [ISO 19108][ISO-19108]-standardissa. Aikapisteen arvo on määritelty ```TM_Position```-luokalla [ISO 8601][ISO-8601-1]-standardin mukaisilla päivämäärä- tai kellonaikakentilla tai niiden yhdistelmällä, tai muulla ```TM_TemporalPosition```-luokan avulla kuvatulla aikapisteellä. Viimeksi mainitun luokan attribuutti ```indeterminatePosition``` mahdollistaa ei-täsmällisen ajanhetken ilmaisemisen liittämällä mahdolliseen arvoon luokittelun *tuntematon*, *nyt*, *ennen*, *jälkeen* tai *nimi*.

#### TM_Period

Kuvaa aikavälin [TM_Instant](#tm_instant)-tyyppisten ```begin```- ja ```end```-attribuuttien avulla. Molemmat attribuutit ovat pakollisia, mutta voivat sisältää tuntemattoman arvon hyödyntämällä ```indeterminatePosition = unknown``` -attribuuttia. Määritelty luokkana [ISO 19108][ISO-19108]-standardissa.

#### URI

Määrittää merkkijonomuotoisen Uniform Resource Identifier (URI) -tunnuksen [ISO 19103][ISO-19103]-standardissa. URIa voi käyttää joko pelkkänä tunnuksena tai resurssin paikantimena (Uniform Resource Locator, URL).

#### Geometry

Kaikkien geometria-tyyppien yhteinen rajapinta [ISO 19107][ISO-19107]-standardissa. Tyypillisimpiä [ISO 19107][ISO-19107]-standardin Geometry-rajapintaa laajentavia rajapintoja ovat ```Point```, ```Curve```, ```Surface``` ja ```Solid``` sekä ```Collection```, jota käyttämällä voidaan kuvata geometriakokoelmia (multipoint, multicurve, multisurface, multisolid).

#### Point
Täsmälleen yhdestä pisteestä koostuva geometriatyyppi. Määritelty rajapintana [ISO 19107][ISO-19107]-standardissa.

## Tietomallin yleispiirteet

Tietomalli perustuu maankäyttöpäätösten yhteiskäyttöisiin tietokomponentteihin. Maankäyttöpäätösten tietokomponenttien MKP-ydin (maankäyttöpäätökset, MKP) kuvaa maankäyttöpäätösten tietomallintamisessa yleiskäyttöisiksi suunnitellut luokat ja niihin liittyvät koodistot, joita hyödynnetään maankäyttörajoitusten tietokomponenttien kautta. MKP-ytimen lisäksi hyödynnetään laajasti Maankäyttöpäätösten tietokomponenttien abstrakteja ja muita luokkia maankäyttöpäätösten tietomallin määrittelemien koodistojen ja soveltamisprofiilin avulla. 

Tietomallien UML-luokkakaaviot ovat saatavilla erillisellä [UML-kaaviot-sivulla](../uml/doc/).

## Maankäyttörajoitusten tietomallin suhde ja tietovirrat Ryhti-hankkeen toisiin tietomalleihin

## Maankäyttöpäätöksien ydin (MKP-ydin)

### AbstraktiVersioituObjekti

Englanninkielinen nimi: AbstractVersionedObject

Stereotyyppi: FeatureType (kohdetyyppi)

Yhteinen yläluokka kaikille maankäyttörajoitusten versiohallituille luokille. Kuvaa kaikkien kohdetyyppien yhteiset ominaisuudet ja assosiaatiot.

Nimi             | Tyyppi              | Kardinaliteetti | Kuvaus
-----------------|---------------------|-----------------|------------------------------------
paikallinenTunnus| [CharacterString](#characterstring)     | 0..1 | kohteen pääavain (id)
nimiavaruus      | [URI](#uri) | 0..1  | tunnusten nimiavaruus
viittausTunnus   | [URI](#uri) | 0..1  | johdettu nimiavaruudesta, luokan englanninkielisestä nimestä ja paikallisesta tunnuksesta
identiteettiTunnus | [CharacterString](#characterstring)     | 0..1  | kohteen versioriippumaton tunnus
tuottajakohtainenTunnus | [CharacterString](#characterstring) | 0..1 | kohteen tunnus tuottajatietojärjestelmässä
viimeisinMuutos  | [TM_Instant](#tm_instant) | 0..1 | ajanhetki, jolloin kohteen tietoja on viimeksi muutettu tuottajatietojärjestelmässä
tallennusAika    | [TM_Instant](#tm_instant) | 0..1 | ajanhetki, jolloin kohde on tietojärjestelmään


### AbstraktiMaankayttoasia

Englanninkielinen nimi: AbstractLandUseMatter

Erikoistaa luokkaa [AbstraktiVersioituObjekti](#abstraktiversioituobjekti).

Stereotyyppi: FeatureType (kohdetyyppi)

Nimi             | Tyyppi              | Kardinaliteetti | Kuvaus
-----------------|---------------------|-----------------|------------------------------------
nimi| [LanguageString](#languagestring)     | 0..* | asian nimi
kuvaus      | [LanguageString](#languagestring) | 0..* | asian kuvausteksti
metatietokuvaus  | [URI](#uri) | 0..1  | viittaus ulkoiseen metatietokuvaukseen

### Asiakirja

Englanninkielinen nimi: Document

Kuvaa käsitteen [maankayttorajoitusten viiteasiakirjan](../kasitemalli/#maankayttorajoitusten-viiteasiakirja). Erikoistaa luokkaa [AbstraktiVersioituObjekti](#abstraktiversioituobjekti). 

Stereotyyppi: FeatureType (kohdetyyppi)

Nimi             | Tyyppi              | Kardinaliteetti | Kuvaus
-----------------|---------------------|-----------------|------------------------------------
asiakirjatunnus | [URI](#uri) | 0..* | asiakirjan pysyvä tunnus, esim. diaarinumero tai muu dokumentinhallinnan tunnus
laji | [MaankayttorajoitustenAsiakirjanLaji](#maankayttorajoitustenasiakirjanlaji) | 1  | asiakirjan tyyppi
lisatietolinkki  | [URI](#uri) | 0..1 | viittaus ulkoiseen lisätietokuvaukseen asiakirjasta
metatietolinkki | [URI](#uri) | 0..1 | viittaus ulkoiseen metatietokuvaukseen asiakirjasta
nimi | [LanguageString](#languagestring) | 0..* | asiakirjan nimi

### AbstraktiTapahtuma

Englanninkielinen nimi: AbstractEvent

Erikoistaa luokkaa [AbstraktiVersioituObjekti](#abstraktiversioituobjekti).

Stereotyyppi: FeatureType (kohdetyyppi)

Nimi             | Tyyppi              | Kardinaliteetti | Kuvaus
-----------------|---------------------|-----------------|------------------------------------
nimi |[LanguageString](#languagestring) | 0..* | tapahtuman kuvaus
tapahtumaAika | [TM_Object](#tm_object) | 0..1  | tapahtuman aika (hetki tai aikaväli)
kuvaus  | [LanguageString](#languagestring) | 0..* | tapahtuman tekstimuotoinen kuvaus

### Kasittelytapahtuma

Englanninkielinen nimi: HandlingEvent

Kuvaa käsitteen käsittelytapahtuma. Erikoistaa luokkaa [AbstraktiTapahtuma](#abstraktitapahtuma).

Stereotyyppi: FeatureType (kohdetyyppi)

Nimi             | Tyyppi              | Kardinaliteetti | Kuvaus
-----------------|---------------------|-----------------|------------------------------------
laji | [AbstraktiKasittelytapahtumanLaji](#abstraktikasittelytapahtumanlaji) | 1  | käsittelytapahtuman tyyppi

### Vuorovaikutustapahtuma

Englanninkielinen nimi: InteractionEvent

Kuvaa käsitteen Vuorovaikutustapahtuma. Erikoistaa luokkaa [AbstraktiTapahtuma](#abstraktitapahtuma).

Stereotyyppi: FeatureType (kohdetyyppi)

Nimi             | Tyyppi              | Kardinaliteetti | Kuvaus
-----------------|---------------------|-----------------|------------------------------------
laji | [AbstraktiVuorovaikutustapahtumanLaji](#abstraktivuorovaikutustapahtumanlaji) | 1  | vuorovaikutustapahtuman tyyppi

### HallinnollinenAlue

Englanninkielinen nimi: AdministrativeArea

Stereotyyppi: Interface (rajapinta)

Hallinnollinen alue on kuvattu maankäyttörajoitusten tietomallissa ainoastaan rajapintana, koska sen mallintaminen on kuulu maankäyttörajoitusten tietomallin sovellusalaan. Toteuttavien tietojärjestelmien tulee tarjota rajapinnan määrittelemät vähimmäistoiminnallisuudet.

Nimi             | Tyyppi              | Kardinaliteetti | Kuvaus
-----------------|---------------------|-----------------|------------------------------------
hallintoaluetunnus | [CharacterString](#characterstring) | 1  | palauttaa hallinnollisen alueen tunnuksen
alue | [geometry](#geometry) | 1  | palauttaa hallinnollisen alueen aluerajauksen
nimi | [CharacterString](#characterstring) | 1  | palauttaa hallinnollisen alueen nimen valitulla kielellä

### Organisaatio

Englanninkielinen nimi: Organization

Stereotyyppi: Interface (rajapinta)

Organisaatio on kuvattu maankäyttörajoitusten tietomallissa ainoastaan rajapintana, koska sen mallintaminen on kuulu maankäyttörajoitusten tietomallin sovellusalaan. Toteuttavien tietojärjestelmien tulee tarjota rajapinnan määrittelemät vähimmäistoiminnallisuudet.

Nimi             | Tyyppi              | Kardinaliteetti | Kuvaus
-----------------|---------------------|-----------------|------------------------------------
nimi | [CharacterString](#characterstring) | 1  | palauttaa organisaation alueen nimen valitulla kielellä

### Päätöksentekijä

Englanninkielinen nimi: Decision-maker

Stereotyyppi: Interface (rajapinta)

Päätöksentekijä on kuvattu maankäyttörajoitusten tietomallissa ainoastaan rajapintana, koska sen mallintaminen on kuulu maankäyttörajoitusten tietomallin sovellusalaan. Toteuttavien tietojärjestelmien tulee tarjota rajapinnan määrittelemät vähimmäistoiminnallisuudet.

Nimi             | Tyyppi              | Kardinaliteetti | Kuvaus
-----------------|---------------------|-----------------|------------------------------------
nimi | [CharacterString](#characterstring) | 1  | palauttaa päätöksentekjän nimen valitulla kielellä

### Koodistot

#### AbstraktiKasittelytapahtumanLaji

Englanninkielinen nimi: AbstractHandlingEventKind

Stereotyyppi: CodeList (koodisto)

Laajennettavuus: Ei laajennettavissa

{% include common/codelistref.html id="RY_MaankayttorajoituksenKasittelytapahtumanLaji" name="Maankäyttörajoituksen käsittelytapahtuman laji" %}


## Maankäyttörajoitusten tiedot

### Maankayttorajoitus

Kuvaa käsitteen Maankayttorajoitus, erikoistaa luokkaa AbstraktiMaankayttoasia, stereotyyppi: FeatureType (kohdetyyppi)

Nimi             | Tyyppi              | Kardinaliteetti | Kuvaus
-----------------|---------------------|-----------------|------------------------------------
arvo | [Abstraktiarvo](#Abstraktiarvo) | 0..1  | maankäyttörajoituksen kuvaava tekstiarvo
elinkaarentila | [Codelist](#MaankayttorajoituksenElinkaarentila) | 1 | yleisimmät arvot hyväksytty, voimassa tai rauennut
geometria | [Geometry](#geometry) | 0..1  | maankäyttörajoituksen sijainti
hyvaksymisAika | [TM_Instant](#TM_Instant) | 0..1 | aika, jolloin maankäyttörajoitus on tullut virallisesti hyväksyttyä
maankayttorajoituksenTunnus  | [CharacterString](#CharacterString) | 1 | yksilöivä ID
rajoituksenLaji | [Codelist](#MaankayttorajoituksenLaji) | 1  | kertoo, millainen maankäyttörajoitus on laadittu
voimaantuloTapa | [Codelist](#MaankayttorajoituksenVoimaantulotapa) | 1  | kertoo tavan tai menettelyn, jonka johdosta maankäyttörajoitus on tullut voimaan

<!-- kaavaTunnus | [URI](#uri) | 0..1  | liittyvän kaavan viittaustunnus, jota käytetään kaavatietovarannon suunnasta oikean maankäyttörajoituksen kohdistamiseen kaavan elinkaaren tilojen muutoksen yhteydessä -->

**Assosiaatiot**

Roolin nimi        | Kohde | Kardinaliteetti | Kuvaus
-----------------|--------------------|---------------------|-----------------
liittyvaKaavarajaus | [Kaava](#Kaava) | 1 | viittaustunnus Kaava-luokkaan, johon kohdistuu maankäyttörajoituskaavamääräyksiä
liittyvaKaavakohde | [Kaavakohde](#Kaavakohde) | 1 | viittaustunnus Kaavakohde-luokkaan, johon kohdistuu maankäyttörajoituskaavamääräyksiä

### Koodisto

#### MaankayttorajoituksenLaji

Englanninkielinen nimi: 

Stereotyyppi: CodeList (koodisto)

Laajennettavuus: Ei laajennettavissa

{% include common/codelistref.html id="RY_MaankayttorajoitustenLaji" name="Maankäyttörajoituksen laji" %}

#### MaankayttorajoituksenElinkaarentila

Englanninkielinen nimi: 

Stereotyyppi: CodeList (koodisto)

Laajennettavuus: Ei laajennettavissa

{% include common/codelistref.html id="RY_MaankayttorajoituksenElinkaarentila" name="Maankäyttörajoituksen elinkaaren tila" %}

#### MaankayttorajoituksenSyntytapa

Englanninkielinen nimi: 

Stereotyyppi: CodeList (koodisto)

Laajennettavuus: Ei laajennettavissa

{% include common/codelistref.html id="RY_MaankayttorajoituksenSyntytapa" name="Maankäyttörajoituksen syntytapa" %}



<!-- linkit standardeihin, joihin mainittu sivun alussa -->
[ISO-8601-1]: https://www.iso.org/standard/70907.html "ISO 8601-1:2019 Date and time — Representations for information interchange — Part 1: Basic rules"
[ISO-639-2]: https://www.iso.org/standard/4767.html "ISO 639-2:1998 Codes for the representation of names of languages — Part 2: Alpha-3 code"
[ISO-19103]: https://www.iso.org/standard/56734.html "ISO 19103:2015 Geographic information — Conceptual schema language"
[ISO-19107]: https://www.iso.org/standard/66175.html "ISO 19107:2019 Geographic information — Spatial schema"
[ISO-19108]: https://www.iso.org/standard/26013.html "ISO 19108:2002 Geographic information — Temporal schema"
[ISO-19109]: https://www.iso.org/standard/59193.html "ISO 19109:2015 Geographic information — Rules for application schema"
[ISO-19505-2]: https://www.iso.org/standard/52854.html "ISO/IEC 19505-2:2012, Information technology — Object Management Group Unified Modeling Language (OMG UML) — Part 2: Superstructure"