---
layout: "default"
title: "Maankäyttörajoitus - looginen tietomalli - Elinkaarisäännöt"
description: ""
id: "elinkaarisaannot"
status: "Luonnos"
---

# Elinkaarisäännöt
{:.no_toc}

1. 
{:toc}

## Johdanto

Tietomalleilla on elinkaari, joka määrää niiden sisältämien tietokohteiden: 

- Syntytavan
- Sen, voivatko ne muuttua
- Miten ne voivat muuttua
- Miten ne raukeaa tai kumoutuu johtaen niiden voimassaolon päättymiseen

Elinkaarisääntöjen määrittely liittyy olennaisesti tietokohteiden versionhallintaan, eli miten yksittäisten tietokohteiden niiden elinkaaren aikana muodostettavat versiot voidaan tallentaa ja yksilöidä viittauskelpoisten pysyvien tunnusten avulla. 

Tässä annetut säännöt pohjautuvat paikkatietokohteiden yksilöivien tunnusten ja elinkaarisääntöjen periaatteisiin, jotka on kuvattu jukishallinnon suosituksessa [JHS 193 - Paikkatiedon yksilöivät tunnukset](http://www.jhs-suositukset.fi/suomi/jhs193).

### HTTP URI -tunnukset

HTTP URI -muotoiset tunnukset ovat [RFC 3986 -standardiin](https://tools.ietf.org/html/rfc3986) perustuvia HTTP(S) -protokollan mukaisia URI-osoitteita (Uniform Resource Identifier), joiden globaali yksilöivyys varmistetaan Internetin DNS-nimipalveluun rekisteröityjen domain-nimien avulla. Kullakin DNS-palveluun rekisteröidyllä domain-nimellä (esim. ```uri.suomi.fi```) on yksiselitteinen omistaja, joka on suoraan tai välillisesti vastuussa ko. domain-nimen alla julkaistavasta sisällöstä. Nimen omistaja on myös ainoa taho, joka voi päättää ko. domain-nimeä käyttävien osoitteiden ohjautumisesta haluttuihin resursseihin, mikä tekee siitä luontevan perustan yksilöivien tunnusten nimiavaruuksille (esim. <http://uri.suomi.fi/object/rytj/kaava>). HTTP URI -muotoisen tunnuksen yksilöivyys perustuu siis domain-nimien ja siten niihin perustuvien nimiavaruuksien keskitettyyn hallintaprosessiin.

URI-tunnuksen ei tarvitse viitata konkreettiseen sijaintiin internetissä, vaan se voi olla abstraktimpi tunnus. [JHS 193 Paikkatiedon yksilöivät tunnukset](http://www.jhs-suositukset.fi/suomi/jhs193) määrittelee paikkatiedon yksilöiville tunnuksille muodon <http://paikkatiedot.fi/{tunnustyyppi}/{aineistotunnus}/{paikallinen tunnus}>, jossa paikkatietokohteiden ```tunnustyyppi``` on ```so```. Maankäyttörajoitusten tietomallissa on esimerkkinä käytetty tunnusmuotoa 
<http://uri.suomi.fi/object/rytj/{aineistotyyppi}/{TietotyypinNimi}/{paikallinenTunnus}>. HTTP URI -muotoisen tunnuksen etuna on luettavuus sekä DNS- ja HTTP-protokollien tarjoama kyky ratkaista (resolve) tunnus ja ohjata kysyjä sitä kuvaavaan Internet-resurssiin ilman tarvetta erityiselle keskitetylle tunnusrekisterille ja siihen perustuvalle ratkaisupalvelulle.

Maankäyttörajoitusten tietomallissa HTTP URI -muotoa käytetään [viittaustunnus](#viittaustunnus)-attribuutissa, jonka avulla viitataan tiettyyn versioon tietokohteesta maankäyttörajoitusten ulkopuolelta.

### UUID-tunnukset
UUID (Universally Unique Identifier) on OSF:n (Open Software Foundation) määrittelemä standardoitu tunnusmuoto, jonka avulla voidaan luoda vakiokokoisia, hyvin suurella todennäköisyydellä yksilöiviä tunnuksia ilman keskitettyä hallintajärjestelmää. UUID-tunnukset voivat perustua satunnaislukuihin, aikaleimoihin, tietokoneiden verkkokorttien MAC-osoitteisiin tai merkkijonomuotoisiin nimiavaruuksiin eri yhdistelmissä. UUID-tunnukset erityisen hyvin tietojärjestelmissä, joissa uusia globaalisti pysyviä ja yksilöiviä tunnuksia on tarpeen luoda hajautetusti ilman keskitettyä tunnusrekisteriä.


Maankäyttörajoitusten tietomallissa UUID-muotoisia tunnuksia suositellaan käytettäväksi [identiteettiTunnus-](#identiteettitunnus), maankäyttörajoituksenTunnus-attribuuttien arvoina.

## Tietomallien kohteiden elinkaaren hallinnan periaatteet

Maankäyttörajoitusten tietomallin elinkaarisäännöt mahdollistavat tietomallin tietokohteiden käsittelyn, tallentamisen ja muuttamisen hallitusti sekä niiden eri voimassaolovaiheissa. Maankäyttörajoitusten tietomallin mukaiset tietosisällöt ovat merkittäviä oikeusvaikutuksia aiheuttavia, juridisesti päteviä aineistoja, joita käsitellään hajautetusti eri toimijoiden tietojärjestelmissä. Tämän vuoksi niiden tunnusten, viittausten ja versionnin hallintaan on syytä kiinnittää erityistä huomiota.

Seuraavat keskeiset periaatteet ohjaavat maankäyttörajoitusten elinkaaren hallintaa:
* Kukin maankäyttörajoitusten tietovarastoon tallennettu versio maankäyttörajoituksesta saa pysyvän, versiokohtaisen tunnuksen.
* Kuhunkin maankäyttörajoitusten tietovarastoon tallennetun tietokohteen versioon voidaan viitata sen pysyvän tunnuksen avulla.
* Maankäyttörajoitusten tietomallin tietokohteiden väliset viittaukset toteutetaan hallitusti sekä maankäyttörajoitustietoa tuottavissa tietojärjestelmissä että yhteisissä maankäyttörajoitusten tietovarastoissa.
* Maankäyttörajoitusten tietovarasto vastaa pysyvien tunnusten luomisesta ja antamisesta tallennettaville tietokohteille.

Maankäyttörajoitusten tietomallin mukaisten aineistojen tallentamisessa erotetaan toisistaan tietojen tuottaminen ja muokkaus sisäisesti niiden tuottamiseen ja muokkaamiseen käytettävissä tietojärjestelmissä ja niiden hallinta yhteisessä versiohallitussa maankäyttörajoitusten tietovarastoissa. Maankäyttörajoitusten tietomallin ei ole mielekästä asettaa vaatimuksia maankäyttörajoitustietoa tuottavien tietojärjestelmien tunnusten ja versioiden hallintaan, vaan tietomallissa tulee varautua siihen, että yhteiseen tietovarastoon tallennettavia tietoja on muokattu ja tallennettu sisäisesti tuntematon määrä kertoja ennen ensimmäistä viemistä yhteiseen tietovarastoon, ja samoin tuntematon määrä kertoja kunkin yhteiseen varastoon vietävän version välillä. Näin ollen on mahdollista, että maankäyttörajoituksesta voi olla joissain tietojärjestelmissä tallennettuna paikallisia versiota, joita ei ole koskaan viety yhteiseen maankäyttörajoitusten tietovarastoon.

## Tunnukset ja niiden hallinta

### Identiteettitunnus
Identiteettitunnus yhdistää saman tunnistettavan tietokohteen kehitysversiot toisiinsa.

{% include common/clause_start.html type="req" id="elinkaari/vaat-identiteettitunnus-maar" %}
Tietomallin tietokohteissa identiteettitunnus kuvataan attribuutilla ```identiteettiTunnus```. Kahdella versioitavalla objektilla voi olla sama ```identiteettiTunnus```-attribuutin arvo ainoastaan, mikäli kaikki seuraavista ehdoista ovat tosia:

* Molemmat objektit kuvaavat saman tietokohteen tai sen sisältämän, nimettävissä olevan tietokohteen kehityskaaren eri tiloja.
* Molemmat objektit liittyvät samaan tietokohteeseen.
* Molemmat objektit ovat saman loogisen tietomallin luokan edustajia.
{% include common/clause_end.html %}

Yksittäisen tietokohteen koko ko. tietojärjestelmään tallennettu kehityshistoria saadaan noutamalla kaikki ko. tyyppisen tietokohteen objektit, joilla on sama ```identiteettiTunnus```-attribuutin arvo.

Yhteinen tietovarasto on vastuussa uusien identiteettitunnusten luomisesta tarvittaessa tallennustapahtumien yhteydessä, ja niiden välittämisestä tiedoksi tallentavalle tietojärjestelmälle. Tallentavan tietojärjestelmän tulee tallentaa itselleen kopiot tietovaraston tallennustapahtuman yhteydessä palautamista maankäyttörajoitusten tietokohteiden identiteettitunnuksista, sillä ne tulee sisällyttää ko. tietokohteiden seuraavien versioden tallennettavaksi lähetettäviin objekteihin.

{% include common/clause_start.html type="req" id="elinkaari/vaat-identiteettitunnus-gen" %}
* Mikäli tallennettavalle tietokohteelle ei ole annettu ```identiteettitunnus```-attribuuttia, tai tietovarasto ei sisällä sellaista saman luokan tietokohdetta, jolla on sama ```identiteettiTunnus```-attribuutin arvo, tietovarasto luo ko. objektille uuden identiteettitunnuksen, joka korvaa tuottavan tietojärjestelmän objektille mahdollisesti antaman ```identiteettiTunnus```-attribuutin arvon. Tällöin objektia pidetään uuden tietokohteen ensimmäisenä versiona.
* Mikäli tietovarasto sisältää saman luokan tietokohteen, jolla on sama ```identiteettiTunnus```-attribuutin arvo kuin tallennetavalla objektilla, objekti tallennetaan tietovarastoon ko. tietokohteen uutena versiona. Tällöin tallennettavan objektin ```identiteettiTunnus```-attribuutin arvo ei muutu.
{% include common/clause_end.html %}

<!--
{% include common/clause_start.html type="req" id="elinkaari/vaat-kaavan-identiteettitunnus" %}
[Maankayttorajoitus](../../looginenmalli/dokumentaatio/#maankayttorajoitus)-luokan tietokohteen tallennuksen yhteydessä maankäyttörajoitusten tietovarasto tarkistaa, että sen attribuutti ```maankayttorajoituksenTunnus``` on annettu ja validi.
* Mikäli kohde katsotaan sen ```identiteettiTunnus```-attribuutin arvon perusteella uudeksi tietokohteeksi, sama ```maankayttorajoituksenTunnus```-attribuutti ei saa olla käytössä muilla [Maankayttorajoitus](../../looginenmalli/dokumentaatio/#maankayttorajoitus)-luokan objekteilla.
* Mikäli kohde katsotaan sen ```identiteettiTunnus```-attribuutin arvon perusteella aiemmin tallennetun tietokohteen uudeksi versioksi, aiemmin tallennetun version ```maankayttorajoituksenTunnus```-attribuutin tulee olla sama kuin tallennettavassa objektissa.
{% include common/clause_end.html %}
-->

{% include common/clause_start.html type="rec" id="elinkaari/suos-identiteettitunnus-form" %}
Identiteettitunnuksen suositeltu muoto on UUID.
{% include common/clause_end.html %}

Esimerkki: ```640bff6b-c16a-4947-af8d-d86f89106be1```

### Paikallinen tunnus
Paikallinen tunnus yksilöi tietokohteen yhden version tietovaraston sisällä. 

{% include common/clause_start.html type="req" id="elinkaari/vaat-paikallinentunnus-maar" %}
Tietomallien tietokohteissa paikallinen tunnus kuvataan attribuutilla ```paikallinenTunnus```. Kaikilla saman tietovaraston objekteilla (ml. saman tietokohteen eri versiot) tulee olla eri ```paikallinenTunnus```-attribuutin arvo.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-paikallinentunnus-gen" %}
Tietokohteiden paikallinen tunnus muuttuu sen jokaisen version tallennuksen yhteydessä. Tietovarasto vastaa paikallisten tunnusten luomisesta tallennustapahtuman yhteydessä. Tuottavan tietojärjestelmän mahdollisesti asettamat arvot korvataan.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-paikallinentunnus-form" %}
Paikallinen tunnus koostuu identiteettitunnuksesta ja siihen erotinmerkillä liitetystä versiokohtaisesta, esimerkiksi tarkkaan tallennusajanhetkeen perustuvasta merkkijonosta.
{% include common/clause_end.html %}

{% include common/clause_start.html type="rec" id="elinkaari/suos-paikallinentunnus-merk" %}
Paikallisen tunnuksen muodostamisessa tulee välttää merkkejä, jotka joudutaan URL-koodaamaan rajapintapalvelujen kutsuissa. Paikkatietokohteen paikallista tunnusta käytetään fyysisten tietomallien pääavaimena, esim. GeoJSON Feature ```id```-omaisuuden ja GML:n ```gml:id```-attribuutin arvona, ja siten esimerkiksi OGC Web Feature Service (WFS) - ja OGC API - Features -rajapintapalvelujen paikkatietokohteen yksilöivissä kyselyissä.
{% include common/clause_end.html %}

Tallennusajanhetkeen päättyvää paikallista tunnusta voidaan käyttää ilman sekaannusmahdollisuuksia samalla logiikalla myös paikallisissa versionneissa, eli sellaisissa tietokohteen versioiden tallennuksissa, joita ei viedä lainkaan tietovarastoon.

Esimerkki:```640bff6b-c16a-4947-af8d-d86f89106be1.b05cf48d46d8c905c54522f44b0a12daff11604e```

{% include common/note.html content="Käyttämällä paikallisena tunnuksena pelkkää identiteettitunnuksesta riippumatonta UUID-tunnusta päästäisiin lyhyempiin tunnuksiin, mutta menetetään yhteys identiteettitunnusten ja paikallisten tunnusten välillä, mikä saattaa hankaloittaa erilaisten vikatilanteiden selvitystä ja toimintavarmuuden testaamista, kun pelkkien tunnusten perusteella ei voida päätellä ovatko kaksi objektia saman tietokohteen eri versioita." %}

### Nimiavaruus
{% include common/clause_start.html type="req" id="elinkaari/vaat-nimiavaruus-maar" %}
Nimiavaruus määrää tietomallin kaikkien tietokohteiden viittaustunnusten alkuosan yhden tietovaraston sisällä. Maankäyttörajoitusten tietomallin tietokohteissa paikallinen tunnus kuvataan attribuutilla ```nimiavaruus```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-nimiavaruus-form" %}
Nimiavaruus on HTTP URI -muotoinen.
{% include common/clause_end.html %}

Nimiavaruus on syytä valita huolella siten, että se olisi mahdollisimman pysyvä, eikä sitä tarvitsisi tulevaisuudessa muuttaa esimerkiksi valtionhallinnon virastojen tai ministeriröiden mahdollisten uudelleenorganisointien ja -nimeämisten johdosta. Valittu URL-osoite tulee myös voida aina tarvittaessa ohjata kulloinkin käytössä olevaan rajapintapalveluun (HTTP redirect). 

{% include common/clause_start.html type="req" id="elinkaari/vaat-nimiavaruus-gen" %}
Tietovarasto vastaa ```nimiavaruus```-attribuuttien asetamisesta tallennustapahtuman yhteydessä. Tuottavan tietojärjestelmän mahdollisesti antamat arvot korvataan.
{% include common/clause_end.html %}

Esimerkki: ```http://uri.suomi.fi/object/rytj/mkr```

### Viittaustunnus
{% include common/clause_start.html type="req" id="elinkaari/vaat-viittaustunnus-maar" %}
Viittaustunnus yksilöi tietokohteen yhden, keskitettyyn tietovarastoon tallennetun kehitysversion globaalisti. Tietomallin tietokohteissa paikallinen tunnus kuvataan attribuutilla ```viittausTunnus```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-viittaustunnus-form" %}
Viittaustunnus on HTTP URI -muotoinen ja se muodostuu nimiavaruudesta, tietokohteen luokan nimestä ja paikallisesta tunnuksesta yhdessä kauttaviivoilla (```/```) erotettuina.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-nimiavaruus-gen" %}
Tietovarasto vastaa ```viittausTunnus```-attribuuttien asetamisesta tallennustapahtuman yhteydessä. Tuottavan tietojärjestelmän mahdollisesti antamat arvot korvataan.
{% include common/clause_end.html %}

Tallentavan tietojärjestelmän ei siis tarvitse tallentaa luotuja viittaustunnuksia itselleen seuraavia tallennuksia varten.

{% include common/clause_start.html type="rec" id="elinkaari/suos-viittaustunnus-ohj" %}
Viittaustunnuksen on suositeltavaa ohjautua aina ko. tietokohteen version tietosisältöön kulloinkin toiminnassa olevassa tietovaraston latauspalvelussa.
{% include common/clause_end.html %}

Esimerkki: ```http://uri.suomi.fi/object/rytj/mkr/maankayttorajoitus/640bff6b-c16a-4947-af8d-d86f89106be1.b05cf48d46d8c905c54522f44b0a12daff11604e```

### Tuottajakohtainen tunnus

{% include common/clause_start.html type="req" id="elinkaari/vaat-tuottajakohtainen-tunnus-maar" %}
Tietokohdetietoa tuottavat järjestelmät voivat niin halutessaan käyttää tuottajakohtaista tunnusta niiden omien tietojärjestelmäspesifisten tunnusten antamiseen  tietomallin tietokohteille. Tietomallin tietokohteissa tuottajakohtainen tunnus kuvataan attribuutilla ```tuottajakohtainenTunnus```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-tuottajakohtainen-tunnus-gen" %}
Tietovarasto ei koskaan muuta tuottavan tietojärjestelmän mahdollisesti asettamia tuottajakohtaisia tunnuksia, ja ne palautetaan sellaisenaan latattaessa tietokohteita tietovarannosta.
{% include common/clause_end.html %}

Tietojärjestelmät voivat käyttää tuottajakohtaisia tunnuksia kohdistamaan tietovarastoon ja paikallisiin tietojärjestelmiin tallennettuja tietokohteita toisiinsa esimerkiksi päivitettäessä niiden tallennuksen yhteydessä syntyneitä tunnuksia, vertailtaessa tietovarastoon tallennettuja kohteita ja paikallisia kohteita toisiinsa, sekä esitettäessä validointipalvelun tuloksia suunnitteluohjelmiston käyttäjälle.

Tuottajakohtaisilta tunnuksilta ei vaadita yksilöivyyttä tai mitään tiettyä yhtenäistä muotoa, mutta UUID-muodon käyttäminen tarjoaa hyvin määritellyn ja standardoidun tavan luoda tuottajakohtaisista tunnuksista yksilöiviä eri tietojärjestelmien kesken. Tästä saattaa olla etua haluttaessa tehdä tuotettavista tietokohdetiedoista mahdollisimman järjestelmäriippumattomia ja esimerkiksi taata tuottajakohtaisten tunnusten yksilöivyys yli mahdollisten tietoa tuottavien tietojärjestelmien vaihdosten ja päivitysten.


{% include common/clause_start.html type="rec" id="elinkaari/suos-tuottajakohtainen-tunnus-form" %}
Tuottajakohtaisen tunnuksen suositeltu muoto on UUID.
{% include common/clause_end.html %}

Esimerkki: ```mkr-123445```

### Maankäyttörajoituksen tunnus
{% include common/clause_start.html type="req" id="elinkaari/vaat-maankayttorajoitustunnus-maar" %}
Maankäyttörajoituksen tunnus on maankäyttöpäätökselle ennakolta haettava, maankäyttöpäätöksen kansallisesti yksilöivä tunnus. Maankäyttörajoitusten tietomallissa maankäyttörajoituksen tunnus kuvataan [Maankayttorajoitus](../../looginenmalli/dokumentaatio/#maankayttorajoitus)-luokan attribuutilla ```maankayttorajoitusTunnus```.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-maankayttorajoitustunnus-gen" %}
Tuottava tietojärjestelmän vastaa maankäyttörajoituksen tunnuksen asettamisesta [Maankayttorajoitus](../../looginenmalli/dokumentaatio/#maankayttorajoitus)-luokan attribuutiksi. Se tulee olla asetettuna myös maankäyttörajoituksen ensimmäisen maankäyttörajoitusten tietovarastoon tallennuksen yhteydessä.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-maankayttorajoitustunnus-yks" %}
Maankäyttörajoituksen tunnus on [Maankayttorajoitus](../../looginenmalli/dokumentaatio/#maankayttorajoitus)-luokan objekteille globaalisti yksilöivä, eikä muutu saman Maankäyttörajoituksen eri elinkaaren aikaisten versioiden tallennuksen yhteydessä.
{% include common/clause_end.html %}

Käytännössä myönnetyt maankäyttörajoitusten tunnukset  kannattaa tallentaa valmiiksi maankäyttörajoitusten tietovarastoon, jotta voidaan tarkistaa, onko tallennettavaksi tarkoitettu maankäyttörajoituksen tunnus myönnetty organisaatiolle, jonka maankäyttörajoitusta ollaan tallentamassa. Kuntakoodin tai muun hallinnollisen alueen tunnuksen käyttö osana maankäyttörajoituksen tunnus tunnusta ei ole suositeltavaa, sillä hallinnolliset alueet muuttuvat ajan kuluessa. Kun sidos tunnuksen ja hallinnollisen alueen välillä ei näy tunnuksessa, voidaan maankäyttörajoituksen hallinnollista aluetta muuttaa joustavammin maankäyttörajoituksen elinkaaren aikana.

{% include common/clause_start.html type="rec" id="elinkaari/suos-maankayttorajoitustunnus-form" %}
Maankäyttörajoituksen tunnuksen suositeltu muoto on UUID.
{% include common/clause_end.html %}

Esimerkki: ```df5b2d6f-d6d6-4695-938c-dd7c4c784c28```

### Pysyvien tunnusten palauttaminen tuottavalle järjestelmälle

Versionhallinnan näkökulmasta on tärkeää, että maankäyttörajoituksen tuottava tietojärjestelmä käyttää saman maankäyttörajoituksen seuraavan version tallentamisessa maankäyttörajoituksen ensimmäisen version tallennuksen yhteydessä luotua identiteettitunnusta. Vastaavasti kaikkien maankäyttörajoituksen tietokohteiden osalta käytetään niiden ensimmäisen tallennuksen yhteydessä luotuja identiteettitunnuksia, mikäli objektin katsotaan kuvaavan ko. tietokohteen uutta versiota.

{% include common/clause_start.html type="req" id="elinkaari/vaat-tunnusten-palautus" %}
Tietovaraston tallennusrajapinta palauttaa tallennetun maankäyttörajoituksen tiedot tuottavalle tietojärjestelmälle tallennusoperaation yhteydessä siten, että ne sisältävät yllä mainittujen tunnustenhallintasääntöjen mukaisesti mahdollisesti generoidut tai muokatut identiteettitunnukset, paikalliset tunnukset, nimiavaruudet ja viittaustunnukset kaikille tallennetuille tietokohteille.
{% include common/clause_end.html %}

### Maankäyttörajoituksen tietokohteisiin viittaaminen ja viitteiden ylläpito

{% include common/clause_start.html type="req" id="vaat-tonttijakosuunnitelman-sisaiset-viittaukset" %}
Saman maankäyttörajoituksen tietokohteiden keskinäiset assosiaatiot toteutetaan viitattavan tietokohteen [paikallinenTunnus](#paikallinen-tunnus)-attribuuttia käyttäen.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-tietovaraston-sisaiset-viittaukset" %}
Maankäyttörajoituksen tietokohteen luokkien assosiaatiot eri maankäyttörajoitusten välillä tai maankäyttörajoituksen ja muiden maankäyttöpäätösten tietokohteiden välillä toteutetaan viitattavan tietokohteen [viittaustunnus](#viittaustunnus)-attribuuttia käyttäen.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-viittaukset-ulkoa" %}
Pysyvät viittaukset maankäyttörajoitusten tietomallin ulkopuolelta tietomallin tietokohteisiin toteutetaan viitattavan tietokohteen [viittaustunnus](#viittaustunnus)-attribuuttia käyttäen.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-viittaukset-tallennettaessa" %}
Tallennettaessa maankäyttörajoitusten tietomallin tietokohteita maankäyttörajoitusten tietovarastoon tietokohteiden tunnukset muuttuvat niiden pysyvään muotoon, kuten kuvattu luvussa [Tunnukset ja niiden hallinta](#tunnukset-ja-niiden-hallinta). Maankäyttörajoitusten tietovaraston vastuulla on päivittää kunkin paikallisen tunnuksen muuttamisen yhteydessä myös kaikkien ko. tietokohteen versioon sen paikallisen tunnuksen avulla viittaavien muiden ko. maankäyttörajoituksen tietokohteiden viittaukset käyttämään tietokohteen muutettua paikallista tunnusta.   
{% include common/clause_end.html %}

## Muutokset ja tietojen versionti
{% include common/clause_start.html type="req" id="elinkaari/vaat-pysyva-sisalto" %}
Kukin maankäyttörajoituksen tallennusoperaatio yhteiseen tietovarastoon muodostaa uuden version tallennettavista tietokohteista, mikäli yksittäinen tietokohde on miltään osin muuttunut verrattuna sen edelliseen versioon. Myös muutokset muissa maankäyttörajoitusten tietomallin tietokohteissa, joihin tietokohteesta on viittaus, lasketaan tietokohteen muutoksiksi. Tallennetun tietokohteen version sisältö ei voi muuttua tallennuksen jälkeen, poislukien sen voimassaolon päättymiseen, seuraavaan versioon linkittämiseen ja elinkaaritilaan liittyvät attribuutit, joita maankäyttörajoitusten tietovarasto itse päivittää tietyissä tilanteissa.
{% include common/clause_end.html %}

Näin taataan ulkoisten viittausten eheys, sillä maankäyttörajoituksen kaikkien kohteiden paikalliset ja viittaustunnukset viittaavat aina vain tietyn, sisällöllisesti muuttumattomaan versioon viittatusta kohteesta. Suositeltavaa on, että kaikki tallennusversiot myös pidetään pysyvästi tallessa, jotta mahdolliset keskenäiset ja ulkopuolelta tulevat linkit eivät mene rikki muutosten yhteydessä.

### Muutosten leviäminen viittausten kautta
Maankäyttörajoitusten tietomallin tietokohteiden keskinäiset viittaukset kohdistuvat aina viitattavien tietokohteiden tiettyyn versioon, ja toisaalta kaikki kohteiden sisällölliset muutokset johtavat uusien versioiden tallentamiseen. Siten kohteiden välisten linkkien kohdetietoa täytyy muuttaa mikäli halutaan viitata jollain tapaa muuttuneeseen kohteeseen. Tämä päivitystarve johtaa edelleen myös viittaavan tietokohteen uuden version luomiseen, vaikka ainoa muuttunut tieto olisi linkki uuteen versioon viitatusta tietokohteesta. Molempiin suuntiin tietokohteiden välillä tehty linkitys saattaa siten johtaa hyvin laajalle leviävään muutosketjuun.

### Yksittäisen maankäyttörajoituksen elinkaaren vaiheisiin liittyvät muutokset
Maankäyttörajoitusten tietomalli mahdollistaa tunnistettavien maankäyttörajoitusten tietokohteiden eri kehitysversioiden erottamisen toisistaan. Kullakin tietomallin kohteella on sekä sen tosimaailman identiteettiin liittyvä ns. identiteettitunnus että yksittäisen tallennusversion tunnus (paikallinen tunnus). Tallennettaessa uutta versiota samasta maankäyttörajoituksesta, sen identiteettitunnus pysyy ennallaan, mutta sen paikallinen tunnus muuttuu. Tallennettaessa Maankayttorajoitus-luokan objektia se katsotaan saman tietokohteen uudeksi versioksi, mikäli sen maankäyttörajoituksen tunnus on sama. Muiden maankäyttörajoitusten tietomallin versioitavien objektien suhteen samuuden määritteleminen on tietoja tuottavien järjestelmien vastuulla: mikäli objektilla on tallennettavaksi lähetettäessä saman ```identititeettiTunnus```-attribuutin arvo kuin aiemmin tallennetulla, samantyyppisellä tietokohteella, katsotaan uusi objekti on saman tietokohteen uudeksi versioksi.

{% include common/clause_start.html type="req" id="elinkaari/vaat-version-korvaus" %}
Kun maankäyttörajoituksen tietokohteesta tallennetaan uusi muuttunut versio, tulee tietokohteen edellisen version ```korvattuObjektilla```-assosiaatio asettaa viittaamaan tietokohteen uuteen versioon. Uuden tietokohteen version ```korvaaObjektin```-assosiaatio puolestaan asetetaan viittaamaan tietokohteen edelliseen, korvattavaan versioon. Molempien kohteiden ```tallennusAika```-attribuutin arvoksi asetetaan ajanhetki, jolloin tallennus ja muutos maankäyttörajoitusten tietovarastoon on tehty.
{% include common/clause_end.html %}

Yksittäisen tietokohteen yksityiskohtainen muutoshistoria maankäyttörajoitusten tietovarastossa saadaan seuraamalla sen ```korvattuObjektilla```- ja ```korvaaObjektin```-assosiaatioita. Ainoa muutos, joka ei näy tietokohteen omana versionaan, on kohteen kumoaminen, jolloin sen viimeisimmän version tietoja päivitetään sen elinkaaritilan, voimassaolon ja tallennusajan osalta.

{% include common/question.html content="Pitääkö [AbstraktiVersioituObjekti](dokumentaatio/#abstraktiversioituobjekti)-luokalle lisätä attribuutti ```ensimmainenTallennusAika```, joka kertoo ko. version alkuperäisen tallennusajan? Kumoamisen yhteydessä ```tallennusAika```-attribuutin arvoa muutetaan, jolloin hukkuu tieto ko. version alkuperäisestä tallennusajankohdasta." %}

Attribuutin ```viimeisinMuutos``` arvo kuvaa ajanhetkeä, jolloin ko. tietokohteeseen on tehty sisällöllinen muutos tiedontuottajan tietojärjestelmässä. Tiedontuottajan järjestelmän osalta ei vaadita tiukkaa versiointipolitiikkaa, eli ```paikallinenTunnus```-attribuutin päivittämistä jokaisen tietokohteen muutoksen johdosta. ```viimeisinMuutos```-attribuutin päivittämien riittää kuvaamaan tiedon todellisen muuttumisajankohdan.

### Maankäyttörajoituksen käsittelytapahtumien elinkaari
Maankäyttörajoitusprosessin historian yhdessä kuvaavat AbstraktiTapahtuma-luokasta perityt Kasittelytapahtuma-luokan tietokohteet linkitetään yksisuuntaisesti AbstraktiMaankayttoasia-luokkaan (Maankayttorajoitus-luokan yläluokka) päin. Tapahtumatietokohteiden uusina versiona tallennettavat muutokset eivät koskaan johda uuden version luomiseen Maankayttorajoitus-luokan tietokohteesta. Syy tähän on se, että käsittelytapahtumien on tärkeää kohdistua nimenomaan tiettyyn, pysyvään versioon maankäyttörajoituksesta.
<!--
Tietyllä ajanhetkellä nähtävillä olevat tai nähtävillä olleet tonttijakosuunnitelman versiot voidaan poimia valitsemalla ne tonttijakosuunnitelmat, joihin kohdistuu Vuorovaikutustapahtuma, jonka laji-attribuutin arvo on Nähtävilläolo, tapahtumaAika-attribuuttin aikaväli kattaa halutun ajankohdan ja peruttu-attribuutin arvo on false. Näiden vuorovaikutustapahtumien liittyvaAsia-assosiaatio viittaa siihen AbstraktiMaankayttoasia-luokan instanssiin, joka ko. aikaan on nähtävillä. Katso tonttijakosuunnitelmaehdotuksen nähtävilläolon ilmoittamiseen liittyvät vaatimukset kohdasta Tonttijakosuunniteman elinkaaritilan muutoksiin liittyvät käsittely- ja vuorovaikutustapahtumat.
-->
{% include common/clause_start.html type="req" id="elinkaari/vaat-tapahtumien-poistaminen" %}
Kerran tallennettuja AbstraktiTapahtuma-luokan tietokohteita ei voi poistaa maankäyttörajoitusten tietovarastosta. Mikäli suunniteltu käsittelytapahtumaan liittyvä päätös kumotaan, tulee sen attribuutti peruttu asettaa arvoon true.
{% include common/clause_end.html %}

{% include common/question.html content="Miten käsittelytapahtumat vaikuttavat versiointiin ja sen muutosketjuun?" %}

{% include common/question.html content="Miten maankäyttörajoitusten eri elinkaarikoodit vaikuttavat käsittelytapahtumiin?" %}

### Maankäyttörajoituksen voimaantulo
Kaavoitus- ja rakentamislaissa säädetään tavoista tai menettelyistä, joiden johdosta maankäyttörajoitus voi tulla voimaan. Kun maankäyttörajoitus tulee voimaan, tallennetaan maankäyttörajoitusten tietovarastoon ensimmäinen versio, jonka ```elinkaaritila```-attribuutin arvo on Voimassa. Maankäyttörajoitus voi syntyä tässä luvussa kuvatuilla tavoilla.

{% include common/clause_start.html type="req" id="elinkaari/vaat-voimaantulotapa" %}
Maankäyttörajoituksen voimaantulotapa kuvataan Maankäyttörajoitus-luokan ```voimaantuloTapa```-attribuutilla ja sen mahdolliset arvot kuvataan Maankäyttörajoituksen voimaantulotapa-koodiston avulla. Maankayttorajoitus-luokan ```voimaantuloTapa```-attribuutti on pakollinen.

**Maankäyttörajoituksen voimaantulotapa**-koodisto kuvaa 4 mahdollista tilaa, joissa maankäyttörajoitus voi tulla voimaan:
- Automaattinen maankäyttörajoitus
- Päätöksellä määrätty maankäyttörajoitus
- Voimassa olevan maankäyttöpäätöksen rajoitus
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-voimaantulo" %}
Maankäyttörajoituksen ```voimassaoloAika``` -attribuutin alkuaika on ajanhetki, jolloin maankäyttörajoitus on tullut voimaan ja loppuaika määräytyy voimaantulotavasta riippuen.


Maankäyttörajoituksen ```voimaantuloTapa```-attribuutin ollessa **Maankäyttörajoituksen voimaantulotapa**-koodiston arvo ```Päätöksellä määrätty maankäyttörajoitus```, voimassaolon määräaika alkaa ensimmäisen tallennettavan version voimaantulosta. Maankäyttörajoitusta jatkettaessa, voimassaolon alkuaika on aina ensimmäisen kerran tallennettavan version voimaantulon ajanhetki ja loppuaika määräytyy kustakin jatkettavasta maankäyttörajoituksesta eteenpäin. Maankäyttörajoitus raukeaa voimassaolon
päätyttyä.

Ensimmäisen päätöksellä määrätyn maankäyttörajoituksen voimaantulemisen yhteydessä maankäyttörajoituksesta tallennetaan maankäyttörajoitusten tietovarastoon uusi versio, jossa sen:
- Maankayttorajoitus-luokan objektin ```elinkaaritila```-attribuutin arvoksi on asetettu ```Voimassa```,
- Maankayttorajoitus-luokan objektin ```voimassaoloAika```-attribuutin alkuajaksi on asetettu käsittelytapahtuman ajanhetki, jolloin maankäyttöpäätöksen määräys on annettu ja loppuaika on siitä kaksi vuotta eteenpäin.

Maankäyttörajoituksen ```voimaantuloTapa```-attribuutin ollessa **Maankäyttörajoituksen voimaantulotapa**-koodiston arvo ```Automaattisen maankäyttörajoituksen``` tai ```Voimassa olevan maankäyttöpäätöksen rajoitus```, voimaantulemisen kuuluttamisen yhteydessä maankäyttörajoituksesta tallennetaan maankäyttörajoitusten tietovarastoon uusi versio, jossa sen:
- Maankayttorajoitus-luokan objektin ```elinkaaritila```-attribuutin arvoksi on asetettu ```Voimassa```,
- Maankayttorajoitus-luokan objektin ```voimassaoloAika```-attribuutin alkuajaksi on asetettu käsittelytapahtuman ajanhetki, jolloin maankäyttöpäätös on hyväksytty ja loppuajankohtaa ei olla annettu. Loppuajankohta määräytyy maankäyttöpäätöksen käsittelytapahtuman voimaantulon mukaan.

<!--
Vanhentuneen asemakaavan maankäyttörajoituksen voimaantulemisen yhteydessä maankäyttörajoituksesta tallennetaan maankäyttörajoitusten tietovarastoon uusi versio, jossa sen:
- Maankayttorajoitus-luokan objektin elinkaaritila-attribuutin arvoksi on asetettu Voimassa,
- Maankayttorajoitus-luokan objektin voimassaoloAika-attribuutin alkuajaksi on asetettu käsittelytapahtuman ajanhetki, jolloin maankäyttöpäätös on annettu ja loppuajankohtaa ei olla annettu.
-->

{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-voimassaoloaika" %}
Maankayttorajoitus on voimassa niiden ```voimassaoloAika```-attribuuttien määräämillä aikaväleillä. Mikäli ```voimassaoloAik```a-attribuutin loppuaika puuttuu, on tietokohde voimassa toistaiseksi.
{% include common/clause_end.html %}

{% include common/question.html content="Tallennetaanko automaattisen maankäyttörajoituksen tapauksessa maankäyttörajoitusten tietovarantoon automaattisesti kaavarajauksen mukainen geometria kaavan Käsittelytapahtuman lajin ollessa **Kaava hyväksytty**?" %}

### Maankäyttörajoituksen jatkaminen, raukeaminen ja kumoaminen 

Kaavoitus- ja rakentamislaissa säädetään maankäyttörajoituksen jatkamisesta, raukeamisesta ja kumoamisesta.

Voimassaoleva maankäyttörajoitus raukeaa sen voimassaoloajan mennessä umpeen. Päätöksellä annettu maankäyttörajoitus voi kumoutua kokonaan tai osittain päätöksellä, jos alueelle tulee voimaan kaava kokonaan tai osittain, jonka toteuttamiseksi maankäyttörajoitus on määrätty.

{% include common/clause_start.html type="req" id="elinkaari/vaat-jatkaminen" %}
Maankäyttörajoitusta jatkettaessa jonka elinkaarentila on Voimassa ilman, että rajoitusalueen geometria muuttuu mm. kaavan osittaisen vahvistumisen myötä, tallennetaan rajoituksesta uusi versio maankäyttörajoitusten tietovarastoon, jonka elinkaaritila-attribuutin arvo on Voimassa, maankäyttörajoitusten tietovarasto päivittää automaattisesti maankäyttörajoituksen edellisen version attribuutteja, joiden elinkaaritila-attribuutin arvo on Voimassa seuraavasti luomatta siitä uutta versioita:

- ```voimassaoloAika```-attribuutin päättymisaika asetetaan samaksi kuin uuden tallennetun version ```voimassaoloAika```-attribuutin alkamisaika. Alkamisaika on määritely kohdassa Maankäyttörajoituksen voimaantulo. 
- ```elinkaaritila```-attribuutin arvo säilyy Voimassa.
- ```tallennusAika```-attribuutin arvoksi asetetaan ajanhetki, jolloin versio muutokset tallennettiin maankäyttörajoitusten tietovarastoon elinkaaritilassa Voimassa.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-raukeaminen" %}
Maankäyttörajoituksen rauetessa voimassaoloajan mennessä umpeen ja jonka elinkaaritila-attribuutin arvo on Voimassa tai kumoutunut osittain, maankäyttörajoitusten tietovarasto päivittää automaattisesti maaakäyttörajoituksen attribuutteja seuraavasti luomatta siitä uutta versioita:

- ```voimassaoloAika```-attribuutin arvot säilyy ennalla.
- ```elinkaaritila```-attribuutin arvoksi asetetaan Rauennut kaikille edellisille versioille.
- ```tallennusAika```-attribuutin arvoksi asetetaan ajanhetki, jolloin maankäyttörajoitus tallennettiin maankäyttörajoitusten tietovarastoon elinkaaritilassa Rauennut.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-kumoutuminen-osittain" %}
Maankäyttörajoitusta jatkettaessa tai kaavan osittaisella vahvistumisella, jossa maankäyttörajoitus kumoutuu osittain tietyiltä alueilta, tallennetaan rajoituksesta uusi versio maankäyttörajoitusten tietovarastoon, jonka elinkaaritila-attribuutin arvo on Kumoutunut osittain, maankäyttörajoitusten tietovarasto päivittää automaattisesti maankäyttörajoituksen edellisen version attribuutteja seuraavasti luomatta siitä uutta versioita:

- ```voimassaoloAika```-attribuutin päättymisaika asetetaan samaksi kuin uuden tallennetun version ```voimassaoloAika```-attribuutin alkamisaika. Alkamisaika on määritely kohdassa Maankäyttörajoituksen voimaantulo. 
- ```elinkaaritila```-attribuutin arvoksi asetetaan Kumoutunut osittain kaikille edellisille versioille.
- ```tallennusAika```-attribuutin arvoksi asetetaan ajanhetki, jolloin versio muutokset tallennettiin maankäyttörajoitusten tietovarastoon elinkaaritilassa Kumoutunut osittain.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-kumoutuminen-kokonaan" %}
Maankäyttörajoituksen kumoutuessaan kokonaan kaavan voimaantulessa tai erillisellä päätöksellä, jonka elinkaaritila-attribuutin arvo on Voimassa tai Kumoutunut osittain, maankäyttörajoitusten tietovarasto päivittää attribuutteja seuraavasti luomatta siitä uutta versioita:

- ```voimassaoloAika```-attribuutin päättymisajaksi asetetaan kumoamispäätöksen ajankohta
- ```elinkaaritila```-attribuutin arvoksi asetetaan Kumoutunut kokonaan kaikille edellisille versioille.
- ```tallennusAika```-attribuutin arvoksi asetetaan ajanhetki, jolloin versio muutokset tallennettiin maankäyttörajoitusten tietovarastoon elinkaaritilassa Kumoutunut kokonaan.
{% include common/clause_end.html %}

{% include common/question.html content="Raukeaako automaattisen maankäyttörajoituksen tapauksessa maankäyttörajoitusten tietovarastossa kaavarajauksen mukainen maankäyttörajoitus kaavan Käsittelytapahtuman lajin ollessa **Kaavan voimaantulo**?" %}

## Maankäyttörajoituksen elinkaaren vaiheet ja elinkaaritila-attribuutin käyttötavat

Maankäyttörajoituksen elinkaareen liittyvää tilaa hallitaan ko. tietokohteiden elinkaaritila-attribuutin ja sen mahdolliset arvot kuvaavan Elinkaaren tila-koodiston avulla. Maankäyttörajoitus-luokan elinkaaritila-attribuutti on pakollinen.

**Elinkaaren tila**-koodisto kuvaa 4 mahdollista tilaa, joissa maankäyttörajoitus voi olla sen elinkaaren eri vaiheissa:

- Voimassa
- Rauennut
- Kumoutunut osittain
- Kumoutunut kokonaan

Maankäyttörajoitus, jonka elinkaaritila on Voimassa, Kumoutunut osittain, sisältää nykyajanhetkellä rajaamallaan alueella voimassa olevan maankäyttörajoituksen. Koodit Kumoutunut kokonaan ja Rauennut kuvaavat Maankäyttörajoituksen tiloja, joissa olevan maankäyttörajoituksen elinkaari on päättynyt.

### Sallitut maankäyttörajoituksen voimaantulotavat maankäyttörajoituksen lajeille

Maankäyttörajoituksen voimaantulotavan ollessa Automaattinen maankäyttörajoitus, Päätöksellä annettu maankäyttörajoitus tai Voimassa olevan maankäyttöpäätöksen rajoitus voi ```rajoituksenLaji``` -attribuutin arvo esiintyä vain tässä luvussa kuvatuilla tavoilla.

{% include common/clause_start.html type="req" id="elinkaari/vaat-ensimmainen-elinkaaritila" %}
Maankäyttörajoituksen voimaantulotapaa tallennettaessa ensimmäistä kertaa maankäyttörajoitusten tietovarastoon voi elinkaarentila olla vain tilassa Voimassa.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-voimaantulotapa" %}
Maankäyttörajoituksen ```voimaantuloTapa```-attribuutin arvo määrittelee ```rajoituksenLajin``` -attribuutin mahdolliset arvot seuraavilla tavoilla:

- Arvolla ```Automaattinen maankäyttörajoitus``` pakolliset arvot  ```Asemakaavan rakennuskielto``` ja ```Asemakaavan toimenpiderajoitus```.
- Arvolla ```Päätöksellä annettu maankäyttörajoitus``` mahdolliset arvot  ```Asemakaavan rakennuskielto```, ```Asemakaavan toimenpiderajoitus```, ```Yleiskaavan rakennuskielto```, ```Yleiskaavan toimenpiderajoitus```, ```Maakuntakaavan rakentamisrajoitus```.
- Arvolla ```Voimassa olevan maankäyttöpäätöksen rajoitus``` mahdolliset arvot  ```Yleiskaavan rakennuskielto```, ```Yleiskaavan toimenpiderajoitus```, ```Yleiskaavan rakentamisrajoitus```, ```Yleiskaavan erityisharkinta-alue```, ```Rakennusjärjestyksen erityisharkinta-alue```, ```Maakuntakaavan rakentamisrajoitus```.

{% include common/clause_end.html %}

### Sallitut maankäyttörajoituksen elinkaaren tilan muutokset

Maankäyttörajoituksen elinkaaritila voi sen voimassaolo-, raukeamis- ja kumoutumisvaiheidensa aikana esiintyä ja muuttua vain tässä luvussa kuvatuilla tavoilla.

{% include common/clause_start.html type="req" id="elinkaari/vaat-ensimmainen-elinkaaritila" %}
Maankäyttörajoituksen elinkaaritila tallennettaessa maankäyttörajoitusta ensimmäistä kertaa maankäyttörajoitusten tietovarastoon voi olla vain tilassa Voimassa.
{% include common/clause_end.html %}

{% include common/clause_start.html type="req" id="elinkaari/vaat-elinkaaritila-siirtymat" %}
Maankäyttörajoituksen ```elinkaaritila```-attribuutin arvo voi kahden sen peräkkäisen tallennusversion välillä vain seuraavilla tavoilla:

- Tilasta ```Voimassa``` tilaan ```Rauennut```, ```Kumoutunut osittain```, ```Kumoutunut kokonaan```.
- Tilasta ```Kumoutunut osittain``` tilaan ```Rauennut```, ```Kumoutunut kokonaan```.
- Tilasta ```Rauennut``` ei ole sallittuja siirtymiä.
- Tilasta ```Kumoutunut kokonaan``` ei ole sallittuja siirtymiä.
{% include common/clause_end.html %}

### Maankäyttörajoituksen elinkaaritilan muutoksiin liittyvät käsittelytapahtumat

Kun maankäyttörajoituksesta viedään maankäyttörajoitusten tietovarastoon uusi versio, jossa sen elinkaaritila on muuttunut, liittyy kyseisen maankäyttörajoituksen version syntymiseen tyypillisesti jokin käsittelytapahtuma.

{% include common/clause_start.html type="req" id="elinkaari/vaat-elinkaaritilan-muutostapahtumat" %}
Maankäyttörajoituksen ```elinkaaritila```-attribuutin arvon seuraaviin muutoksiin tulee aina liittyä **Kasittelytapahtuma**, jonka ```laji```-attribuutin arvo tulee olla elinkaarimuutosta vastaava:

- Muutos tilaan **Voimassa**: Liityttävä käsittelytapahtuman laji Maankäyttörajoituksen määrääminen tai Maankäyttörajoituksen jatkaminen .
- Muutos tilaan **Kumoutunut osittain**: Liityttävä käsittelytapahtuman laji Maankäyttörajoituksen jatkaminen.
- Muutos tilaan **Kumoutunut kokonaan**: Liityttävä käsittelytapahtuman laji Maankäyttörajoituksen kumoaminen.
{% include common/clause_end.html %}

Yllä luetellut käsittelytapahtumat tulee tallentaa samaan aikaan elinkaaritilaltaan muuttuneen maankäyttörajoituksen kanssa.

Huomaa, että muutos tilaan Rauennut, Kumoutunut osittain tai Kumoutunut kokonaan voi liittyä kaavan **Kasittelytapahtuma** -luokkaan, jonka ```laji```-attribuutin arvo voi olla maankäyttöpäätöksen voimaantuloon tai kumoaminen.

