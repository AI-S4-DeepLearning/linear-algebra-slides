---
# try also 'default' to start simple
theme: ./slidev-theme-hu
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Template for HU.

  Learn more at [Sli.dev](https://sli.dev)
fonts:
  sans: 'Avenir'
  serif: 'Roboto Slab'
  mono: 'Iosevka'
# persist drawings in exports and build
drawings:
  persist: false
# page transition
transition: fade-out
# use UnoCSS
css: unocss
themeConfig:
  paginationX: r
  paginationY: t
  paginationPagesDisabled: [1]
layout: cover
---

<link rel="stylesheet" type="text/css" href="s4.css" />

# Data en Dimensionaliteit

## Lineaire Algebra 1

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->


---
layout: image-right
image: recap.jpg
---

# Recap

<br>

# Agenda

---
layout: image
image: wooclap.png
---

---
layout: chaptertitle
---

# Data

---

# Recap Data

- In S3 gekeken naar data binnen AI
  - 1- of laag-dimensionaal
- Datapunt wordt weergegeven door 1 of meer getallen
- Dataset: serie van datapunten

---

# Dimensionaliteit

**Voorbeeld** een serie verkoopwaardes van panden in de stad Utrecht
- `["Houtensepad 17", 695_000]`
- `["Adriaen van Ostadelaan 161-3", 375_000]`
- `["Bemuurde Weerd O.Z. 56", 2_750_000]`
- `["1e Daalsedijk 220", 475_000]`
- `["Texel 27", 19_000]`
- `["Ina Boudier-Bakkerlaan 14-B", 239_000]`

Data is 1-dimensionaal
- 1 getal is voldoende om alle (beschikbare) informatie weer te geven.
- Eenvoudig op een getallenlijn te plaatsen

---

# Dimensionaliteit

**Voorbeeld** een serie kleuren

<span style="padding: 3px; font-weight: bold; background: #c9a0dc">Wisteria</span> &nbsp;
<span style="padding: 3px; font-weight: bold; background: #bd55d3">Orchid</span> &nbsp;
<span style="padding: 3px; font-weight: bold; background: #e52b50">Amaranth</span> &nbsp;
<span style="padding: 3px; font-weight: bold; background: #2a3439">Gunmetal</span> &nbsp;
<span style="padding: 3px; font-weight: bold; background: #e5e4e2">Platinum</span> &nbsp;
<span style="padding: 3px; font-weight: bold; background: #00416a">Indigo</span> &nbsp;

Hoe zouden we dit op &eacute;&eacute;n getallenlijn plaatsen?

<v-click>

- Licht naar donker?
- Zwart-wit naar fel?
- Rood-paars-blauw?

&nbsp;

</v-click>

<v-click>

**Deze data is meer-dimensionaal**

*Voor kleuren doorgaans 3 dimensies (RGB-kubus, HSV kleuren)*

</v-click>

---
layout: image-right
image: colours1.svg
---

# Waarom 3D?

- Menselijk oog heeft drie typen lichtgevoelige kegels
  - Rood <span style="color: #f00">$\searrow$</span>
  - Blauw <span style="color: #0f0">$\nearrow$</span>
  - Groen <span style="color: #00f">$\uparrow$</span>
  - *(staafjes dragen nauwelijks bij aan kleurenvisie)*
  - *Kleurenblindheid $\to$ 2D-kleuren, of zelfs 1D*
- **We plotten kleuren in een 3D *ruimte***
- Alternatieve kleurmodellen $\to$ [transformaties op ruimtes](https://depasquale.art/works/3d-color-space-explorer/)

---
layout: image-right
image: colours2.svg
---

# Deelruimtes

In dit geval lijkt 2D bijna "voldoende"

- Kleuren liggen op een plat vak dat schuin door de ruimte loopt
- Groen-component lijkt (met verlies) te voorspellen uit andere componenten

<img src="/colours3.svg" style="margin: auto; height: 18vh" />

Wiskundige technieken om te bepalen hoe we hoger-dimensionele data in minder dimensies kunnnen weergeven (met verlies).

---
layout: image-left
image: lalg.png
---

# Lineaire Algebra

- Data gaan we beschouwen als punten in een ruimte
  - Voorbeelden 2D / 3D
  - Deep Learning praktijk: honderden dimensies
- Wiskundige taal om berekeningen ongeacht aantal dimensies op te schrijven
  - Variabelen staan niet (alleen) voor getallen (1D), maar voor meer-dimensionale objecten

---

# Vectoren

- Vector bestaat in een $n$-dimensionale ruimte
  - Coordinaat in de ruimte
  - Weer te geven als lijst van $n$ getallen (coordinaten)

&nbsp;

### Voorbeeld: 2D

$$\vec v = \begin{bmatrix}1 \\ 2 \end{bmatrix}\qquad \vec u = \begin{bmatrix}3 \\ -1 \end{bmatrix}$$

$\vec v$ en $\vec u$ zijn vectoren in een 2D ruimte. $\vec v$ is te lezen als het coordinaat $X = 1,\ Y = 2$.

**Teken deze punten op een vel papier met een assenstelsel. Teken voor beide punten een pijl van de oorsprong naar het coordinaat.**

*De ruimte waar alle 2D vectoren in vallen drukken we uit als $\mathbb R^2$. We gebruiken de set notatie $\vec v \in \mathbb R^2$ om uit te drukken dat $\vec v$ een 2D-vector is.*

---
layout: image-right
image: vec_add.svg
---

# Vectoren optellen

We kunnen 2 vectoren bij elkaar optellen: 
  - Geometrisch (plaatje)
  - Numeriek

$$\vec v = \begin{bmatrix}1 \\ 2 \end{bmatrix}\qquad \vec u = \begin{bmatrix}3 \\ -1 \end{bmatrix}$$
$$\vec z = \vec v + \vec u = \begin{bmatrix}1 \\ 2 \end{bmatrix} + \begin{bmatrix}3 \\ -1 \end{bmatrix} = \begin{bmatrix}3 + 1 \\ 1 + (-1) \end{bmatrix} = \begin{bmatrix}4 \\ 0 \end{bmatrix}$$


---
layout: image-right
image: vec_add.svg
---

# Regels voor optellen

Vectoren voldoen aan een aantal regels, waardoor optellen werkt zoals we gewend zijn van getallen:

- Associativiteit: $\vec u + \vec v = \vec v + \vec u$
- Commutativiteit: $(\vec u + \vec v) + \vec w = \vec u + (\vec v + \vec w)$
- Identiteit: $\exist\ \vec 0 \text{ zodat } \vec 0 + \vec v = \vec 0 = \vec v + \vec 0$
    - Er bestaat voor iedere ruimte een vector $\vec 0$ die als nul-element fungeert
- Inverse:  $\forall\ \vec v\ \ \exists(-\vec v) \text{ zodat }  \vec v + (- \vec v) = \vec 0$
    - Er bestaat voor elke vector $\vec v$ in iedere ruimte een inverse $-\vec v$
    - Meestal schrijven we niet $\vec u + (- \vec v)$, maar $\vec u - \vec v$ (aftrekken)


---
layout: image-right
image: vec_scale.svg
---

# Schalen (scalair product)

  - Vermeniguldigen met een gewoon (scalair) getal
  - Deze getallen komen uit dezelfde verzameling als de getallen binnen de vectoren
      - In ons geval ($\mathbb R^2$) is dit uit $\mathbb R$
  - Veelvouden van $\vec v$ vormen een soort getallenlijn

### Numeriek

We vermenigvuldigen elk getal in de vector:

$$2 \cdot \vec v = 2 \cdot \begin{bmatrix}1 \\ 2 \end{bmatrix} = \begin{bmatrix}2 \cdot 1 \\ 2 \cdot 2 \end{bmatrix} = \begin{bmatrix}2 \\ 4 \end{bmatrix}$$
$$-1 \cdot \vec v = -1 \cdot \begin{bmatrix}1 \\ 2 \end{bmatrix} = \begin{bmatrix}-1 \cdot 1 \\ -1 \cdot 2 \end{bmatrix} = \begin{bmatrix}-1 \\ -2 \end{bmatrix} = -\vec v$$
$$0 \cdot \vec v = 0 \cdot \begin{bmatrix}1 \\ 2 \end{bmatrix} = \begin{bmatrix}0 \cdot 1 \\ 0 \cdot 2 \end{bmatrix} = \begin{bmatrix}0 \\ 0 \end{bmatrix} = \vec 0$$

---
layout: image-right
image: vec_dist.svg
---

# Regels

- Identiteit: $1 \vec v = \vec v$
- Scalair vermenigvuldigen werkt samen met normaal vermenigvuldigen: $a \cdot (b \cdot \vec v) = (a \cdot b) \cdot \vec v$
- Distributiviteit over vector som: $a \cdot (\vec u + \vec v) = a \cdot \vec u + a \cdot \vec v$
- Distributiviteit over scalaire som: $(a + b) \cdot \vec v = a \cdot \vec v + b \cdot \vec v$

*Ook deze regels maken dat rekenen met vectoren zoveel mogelijk werkt als we gewend zijn (geen verrassingen)*

TODO plaatje

---

# Wiskundig gezien

... is alles dat aan deze regels voldoet een vector(ruimte)
  - Werkt dus ook in 3D, 4D, 1000D
  - Geldt ook voor andere wiskundige objecten:
      - Getallen
      - Functies
      - Matrices en Tensoren (die binnenkort aan bod komen)

**Een vector hoeft dus niet een lijst met getallen te zijn, maar dit is wel de weergave die wij zullen hanteren.**

&nbsp;

## Bonus
- Iets meer dan de helft van de regels werkt ook voor bijvoorbeeld `str` in Python. **Welke niet, en waarom?**

---
layout: image-right
---

# Lineaire combinaties

Door vectoren te schalen en op te tellen, kunnen we bestaande vectoren combineren:

$$\vec v = \begin{bmatrix}1 \\ 2 \end{bmatrix}\qquad \vec u = \begin{bmatrix}3 \\ -1 \end{bmatrix}$$

&nbsp;

$$2 \vec v + 3 \vec u = 2 \begin{bmatrix}1 \\ 2 \end{bmatrix} + 3 \begin{bmatrix}3 \\ -1 \end{bmatrix} = \begin{bmatrix}2 \\ 4 \end{bmatrix} + \begin{bmatrix}9 \\ -3 \end{bmatrix} = \begin{bmatrix}12 \\ 1 \end{bmatrix}$$

In dit geval kunnen we elke vector schrijven als een som van $\vec u$ en $\vec v$.

*Maar...* **Kan dit altijd?**

<div style="font-size: 0.9rem; margin-top: 30px">

**net als bij normale vermenigvuldiging laten we het multiplicatieteken vaak weg bij het scalair product, en gebruiken we $2 \vec x$ als shorthand voor $2 \cdot \vec x$*

</div>

---
layout: image-right
---

# Lineaire Onafhankelijkheid

- In het vorige voorbeeld hadden als het ware twee getallenlijnen die kruisen op de oorsprong (0, 0)
- Dit geeft een (alternatief) coordinatenstelsel voor de 2D ruimte
  - Voorwaarde: de twee vectoren liggen niet op &eacute;&eacute;n lijn
  - Werkt voor alle combinaties van 2 vectoren die geen veelvoud van elkaar zijn

---
layout: image-left
image: teapot.png
---

# In meer dimensies

- In 3D kan dit kan dit ook, maar nu hebben we drie vectoren nodig
  - 2 vectoren geven een 2D vlak dat dwars door de ruimte loopt
  - Een derde vector geeft de 3D ruimte
      - Deze mag geen lineaire combinatie zijn van de eerste twee
      - Het maakt niet uit in welke volgorde we de vectoren kiezen
      - **De drie vectoren zijn *lineair onafhankelijk***
- In $n$ dimensies zijn $n$ lineair onafhankelijke vectoren nodig

---

# Basis

- Met een lineair onafhankelijk set van $n$ vectoren kunnen we een $n$ dimensionale ruitme defini&euml;ren
- De vectoren geven een nieuw coordinatensysteem, dit noemen we de *basis*
  - Meestal werken we met de standaardbasis, bijvoorbeeld voor 3D:

  $$\vec x = \begin{bmatrix}1 \\ 0 \\ 0\end{bmatrix} \qquad \vec y = \begin{bmatrix}0 \\ 1 \\ 0\end{bmatrix} \qquad \vec z = \begin{bmatrix}0 \\ 0 \\ 1\end{bmatrix}$$
  - De vectoren hebben een standaard-lengte $1$ en staan haaks op elkaar --- dit rekent het makkelijkst

&nbsp;

**We kunnen de vector vectoren nu in termen van de basis schrijven**

$$\vec u = \begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix} \quad \iff \quad \vec u = 1 \vec x + 2 \vec y + 3 \vec z$$

---
layout: image-right
image: ltf.gif
---

# Dimensionaliteit van een basis

- Lengte vectoren niet belangrijk, maar aantal vectoren dat lineair onafhankelijk is, *bijvoorbeeld*

  $$\vec u = \begin{bmatrix}1 \\ 2 \\ 3\end{bmatrix} \qquad \vec v = \begin{bmatrix}3 \\ 2 \\ 1\end{bmatrix} \qquad \vec w = \begin{bmatrix}-2 \\ 0 \\ 2\end{bmatrix}$$

- De set $\{ \vec u, \vec v, \vec w \}$ is niet lineair onafhankelijk, maar elke subset van twee vectoren is dit wel
- We hebben een basis voor een 2D-ruimte, niet 3D

---

# Inwendig product

$$\vec v = \begin{bmatrix}1 \\ 2 \end{bmatrix}\qquad \vec u = \begin{bmatrix}3 \\ -1 \end{bmatrix}$$

$$\langle v \mid u \rangle = 1 \cdot 3 + 2 \cdot -1 = 3 - 2 = 1$$

Het inwendig product wordt ook wel geschreven als $\vec v \cdot \vec u$ of $\langle v, u \rangle$. In bepaalde contexten kun je ook de naam "dot-product" tegenkomen. In python gebruik je de `u.dot(v)` functie of `u @ v`.

- De waarde van een inwendig product hangt van een aantal dingen af:
  - Hoe groter de vectoren die erin gaan, hoe groter het inwendig product
  - Hoe meer vectoren op elkaar lijken, hoe groter het inwendig product
    - Twee vectoren die dezelfde kant op wijzen, hebben een positief product
    - Twee vectoren die van elkaar afwijzen, hebben een negatief product
    - Twee vectoren die haaks op elkaar staan, hebben een product van $0$

&nbsp;

**Merk op dat de volgorde van de vectoren net zo goed andersom had kunnen zijn, en de uitkomst gelijk was geweest. Toch geven we beide varianten een andere betekenis.**

---

# Rij-vectoren

In de originele berekening hadden we:

$$\langle v \mid u \rangle = 1 \cdot 3 + 2 \cdot -1 = 3 - 2 = 1$$

In dit geval beschouwen we de vector $\vec v$ als een soort van functie, die van de vector $\vec u$ een normaal getal in $\mathbb R$ maakt. In deze context schrijven we $\vec v$ als een rij, en $\vec u$ zoals gebruikelijk als kolom.

$$\begin{bmatrix}1 & 2\end{bmatrix} \begin{bmatrix}3 \\ -1\end{bmatrix}$$

Als we variabelen gebruiken, is een rij vector te schrijven als $\langle v|$, en een kolom als $|u \rangle$. Voor een willekeurige vector $\vec w$ gaan we uit van een kolom-vector $| w \rangle$.

### Andersom

$$\langle u \mid v \rangle = \begin{bmatrix}3 & -1\end{bmatrix} \begin{bmatrix}1 \\ 2\end{bmatrix} = 3 \cdot 1 + -1 \cdot 2 = 3 - 2 = 1$$

**De uitkomst is steeds hetzelfde, het verschil tussen rij en kolom zit hem in hoe we de vector zien: als data of als actie.**

---

# Cosine Similarity

---

# Projecties

---

# Transformaties
- Lineair
- Niet Lineair

---

# Matrices

Lineaire functies van vectoren naar vectoren

---

# Functies als data, data als functie

Rij/kolom elementen
- Mogelijk row/column/null?

## Covectoren

---

# 2-forms

Lineaire functies van 2 vectoren naar een getal

---

# Tensoren

- Generalisatie op matrices, 2-forms -> 3D arrays

Bijv: lineaire functie van 2 vectoren naar 1 vector

---

# Calculus

---

# Afgeleide van een getal-wise functie -> sigmoid?

---

# Afgeleide van een functie met 2 args

- Partieel
- Gradient

---

# Afgeleides van matrix-producten / tensoren etc

---

# Convoluties?

- Nee, later pas, ander slidedeck

---
layout: chaptertitle
---

# Werkcollege

---
layout: image-right
image: reps.jpg
---

# Aan de slag!

<br>

### Reader
- Opgave 1.1
- Opgave 1.2
- Opgave 1.3
- Opgave 1.4
- Opgave 1.5
