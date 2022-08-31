---
layout: "default"
title: "Maankäyttörajoitukset - soveltamisprofiili"
description: ""
id: "soveltamisohje-mkr"
status: "Luonnos"
---
# Soveltamisprofiili

{:.no_toc}

1. 
{:toc}

## Johdanto

Tämän dokumentin vaatimukset ja suositukset muodostavat maankäyttörajoitusten loogisen tietomallin soveltamisprofiilin maankäyttörajoitus-aineistoille. Soveltamisprofiili kuvaa ne maankäyttörajoitukset ja lisävaatimukset, joita tulee noudattaa maankäyttörajoitusten tietomallin UML-kielisen kuvauksen ja sen sanallisen dokumentaation soveltamisessa maankäyttörajoitusten tietoaineistojen kuvaamiseen.

## Koodistot


### Käsittelytapahtuman laji

<!--Lisää sisäiset linkit vielä -->
{% include common/clause_start.html type="req" id="prof-mkr/vaat-maankayttorajoituskasittelytapahtuma" %}
Luokan AbstraktiKasittelytapahtumanLaji sijaan tulee käyttää tarkentavaa luokkaa MaankayttorajoitustenKasittelytapahtumanLaji.
{% include common/clause_end.html %}

## Maankäyttörajoituksen lajien arvot

Seuraavat **Maankäyttörajoituksen laji**-koodiston arvojen soveltamisohjeet huomioidaan vain Maankayttorajoitus-luokan ```voimaantuloTapa```-attribuutin arvon ollessa ```Päätöksellä annettu maankäyttörajoitus```. ```Automaattinen maankäyttörajoitus``` ja ```Voimassa olevan maankäyttöpäätöksen rajoitus``` tapauksissa Maankayttorajoitus-luokan ```arvo```-attribuutin arvo generoidaan automaattisesti tietojärjestelmässä kaavatietomallista ennalta määriteltyjen sääntöjen mukaisesti. Maankäyttörajoituksen ```voimaantuloTapa``` -attribuutin kanssa mahdolliset esiintyvät ```rajoituksenLaji```-attribuutin arvot on esitelty luvussa [Elinkaarisäännöt-sivulla](https://ym-rakennettu-ymparisto.github.io/maankayttorajoitusten-tietomalli/1.0-dev/looginenmalli/elinkaarisaannot.html#sallitut-maankäyttörajoituksen-voimaantulotavat-maankäyttörajoituksen-lajeille). 


### Asemakaavan rakennuskielto

**Koodi:** http://uri.suomi.fi/codelist/rytj/RY_MaankayttorajoituksenLaji/code/01

<!--Lisää sisäiset linkit vielä -->
{% include common/clause_start.html type="req" id="prof-mkp/vaat-asemakaavan-rakennuskielto" %}
Ilmaisee, että kyseinen maankäyttörajoitus koskee asemakaavan rakennuskieltoa.
{% include common/clause_end.html %}

<!--Lisää sisäiset linkit vielä -->
{% include common/clause_start.html type="req" id="prof--mkp/vaat-asemakaavan-rakennuskielto-arvot" %}
```arvo```-attribuutin arvona saa esiintyä TekstiArvo, joka kuvaa asemakaavan rakennuskiellon informatiivisen sisällön tietojärjestelmissä tai rekistereissä.
{% include common/clause_end.html %}

### Asemakaavan toimenpiderajoitus

**Koodi:** http://uri.suomi.fi/codelist/rytj/RY_MaankayttorajoituksenLaji/code/02

<!--Lisää sisäiset linkit vielä -->
{% include common/clause_start.html type="req" id="prof-mkp/vaat-asemakaavan-toimenpiderajoitus" %}
Ilmaisee, että kyseinen maankäyttörajoitus koskee asemakaavan toimenpiderajoitusta.
{% include common/clause_end.html %}

<!--Lisää sisäiset linkit vielä -->
{% include common/clause_start.html type="req" id="prof--mkp/vaat-asemakaavan-toimenpiderajoitus-arvot" %}
```arvo```-attribuutin arvona saa esiintyä TekstiArvo, joka kuvaa asemakaavan toimenpiderajoituksen informatiivisen sisällön tietojärjestelmissä tai rekistereissä.
{% include common/clause_end.html %}


### Yleiskaavan rakennuskielto

**Koodi:** http://uri.suomi.fi/codelist/rytj/RY_MaankayttorajoituksenLaji/code/03

<!--Lisää sisäiset linkit vielä -->
{% include common/clause_start.html type="req" id="prof-mkp/vaat-yleiskaavan-rakennuskielto" %}
Ilmaisee, että kyseinen maankäyttörajoitus koskee yleiskaavan rakennuskielto.
{% include common/clause_end.html %}

<!--Lisää sisäiset linkit vielä -->
{% include common/clause_start.html type="req" id="prof--mkp/vaat-yleiskaavan-rakennuskielto-arvot" %}
```arvo```-attribuutin arvona saa esiintyä TekstiArvo, joka kuvaa yleiskaavan rakennuskiellon informatiivisen sisällön tietojärjestelmissä tai rekistereissä.
{% include common/clause_end.html %}

### Yleiskaavan toimenpiderajoitus

**Koodi:** http://uri.suomi.fi/codelist/rytj/RY_MaankayttorajoituksenLaji/code/04

<!--Lisää sisäiset linkit vielä -->
{% include common/clause_start.html type="req" id="prof-mkp/vaat-yleiskaavan-toimenpiderajoitus" %}
Ilmaisee, että kyseinen maankäyttörajoitus koskee yleiskaavan toimenpiderajoitusta.
{% include common/clause_end.html %}

<!--Lisää sisäiset linkit vielä -->
{% include common/clause_start.html type="req" id="prof--mkp/vaat-yleiskaavan-rakennuskielto-arvot" %}
```arvo```-attribuutin arvona saa esiintyä TekstiArvo, joka kuvaa yleiskaavan toimenpiderajoituksen informatiivisen sisällön tietojärjestelmissä tai rekistereissä.
{% include common/clause_end.html %}

### Yleiskaavan rakentamisrajoitus

**Koodi:** http://uri.suomi.fi/codelist/rytj/RY_MaankayttorajoituksenLaji/code/05

<!--Lisää sisäiset linkit vielä -->
{% include common/clause_start.html type="req" id="prof-mkp/vaat-yleiskaavan-rakentamisrajoitus" %}
Ilmaisee, että kyseinen maankäyttörajoitus koskee yleiskaavan rakentamisrajoitusta.
{% include common/clause_end.html %}

<!--Lisää sisäiset linkit vielä -->
{% include common/clause_start.html type="req" id="prof--mkp/vaat-yleiskaavan-rakennuskielto-arvot" %}
```arvo```-attribuutin arvona saa esiintyä TekstiArvo, joka kuvaa yleiskaavan toimenpiderajoituksen informatiivisen sisällön tietojärjestelmissä tai rekistereissä.
{% include common/clause_end.html %}

### Yleiskaavan suunnittelutarvealue

**Koodi:** http://uri.suomi.fi/codelist/rytj/RY_MaankayttorajoituksenLaji/code/06

<!--Lisää sisäiset linkit vielä -->
{% include common/clause_start.html type="req" id="prof-mkp/vaat-yleiskaavan-erityisharkinta-alue" %}
Ilmaisee, että kyseinen maankäyttörajoitus koskee yleiskaavan suunnittelutarvealue.
{% include common/clause_end.html %}

<!--Lisää sisäiset linkit vielä -->
{% include common/clause_start.html type="req" id="prof--mkp/vaat-yleiskaavan-yleiskaavan-erityisharkinta-alue-arvot" %}
```arvo```-attribuutin arvona saa esiintyä TekstiArvo, joka kuvaa yleiskaavan suunnittelutarvealueen informatiivisen sisällön tietojärjestelmissä tai rekistereissä.
{% include common/clause_end.html %}

### Maakuntakaavan rakentamisrajoitus

**Koodi:** http://uri.suomi.fi/codelist/rytj/RY_MaankayttorajoituksenLaji/code/07

<!--Lisää sisäiset linkit vielä -->
{% include common/clause_start.html type="req" id="prof-mkp/vaat-maakuntakaavan-rakentamisrajoitus" %}
Ilmaisee, että kyseinen maankäyttörajoitus koskee maakuntakaavan rakentamisrajoitusta.
{% include common/clause_end.html %}

<!--Lisää sisäiset linkit vielä -->
{% include common/clause_start.html type="req" id="prof--mkp/vaat-maakuntakaavan-rakentamisrajoitus-arvot" %}
```arvo```-attribuutin arvona saa esiintyä TekstiArvo, joka kuvaa maakuntakaavan rakentamisrajoituksen informatiivisen sisällön tietojärjestelmissä tai rekistereissä.
{% include common/clause_end.html %}

### Rakennusjärjestyksen suunnittelutarvealue

**Koodi:** http://uri.suomi.fi/codelist/rytj/RY_MaankayttorajoituksenLaji/code/08

<!--Lisää sisäiset linkit vielä -->
{% include common/clause_start.html type="req" id="prof-mkp/vaat-erityisharkinta-alue" %}
Ilmaisee, että kyseinen maankäyttörajoitus koskee rakennusjärjestyksen suunnittelutarvealuetta 
{% include common/clause_end.html %}

<!--Lisää sisäiset linkit vielä -->
{% include common/clause_start.html type="req" id="prof--mkp/vaat-erityisharkinta-alue-arvot" %}
```arvo```-attribuutin arvona saa esiintyä TekstiArvo, joka kuvaa rakennusjärjestyksen suunnittelutarvealueen informatiivisen sisällön tietojärjestelmissä tai rekistereissä.
{% include common/clause_end.html %}