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

# AI-S4 Deep Learning
## Lineaire Algebra

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

# [LA-1] Data en Dimensionaliteit

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

<hsp />

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
  - Notatie: $\mathbf v$, $\vec v$ of $\ket v$


### Voorbeeld: 2D

$$\ket v = \begin{bmatrix}1 \\ 2 \end{bmatrix}\qquad \ket u = \begin{bmatrix}3 \\ -1 \end{bmatrix}$$

$\ket v$ en $\ket u$ zijn vectoren in een 2D ruimte. $\ket v$ is te lezen als het coordinaat $X = 1,\ Y = 2$. Doorgaans hebben we het niet over $X$ en $Y$, maar over elementen o.b.v. een vector en index: $u_1 = 3$ en $u_2 = -1$.

**Teken deze punten op een vel papier met een assenstelsel. Teken voor beide punten een pijl van de oorsprong naar het coordinaat.**

*De ruimte waar alle 2D vectoren in vallen drukken we uit als $\mathbb R^2$. We gebruiken de set notatie $\ket v \in \mathbb R^2$ om uit te drukken dat $\ket v$ een 2D-vector is.*

---
layout: image-right
image: vec_add.svg
---

# Vectoren optellen

We kunnen 2 vectoren bij elkaar optellen: 
  - Geometrisch (plaatje)
  - Numeriek

$$\ket v = \begin{bmatrix}1 \\ 2 \end{bmatrix}\qquad \ket u = \begin{bmatrix}3 \\ -1 \end{bmatrix}$$
$$\ket z = \ket v + \ket u = \begin{bmatrix}1 \\ 2 \end{bmatrix} + \begin{bmatrix}3 \\ -1 \end{bmatrix} = \begin{bmatrix}3 + 1 \\ 1 + (-1) \end{bmatrix} = \begin{bmatrix}4 \\ 0 \end{bmatrix}$$

<hsp />

*Vectoren voldoen aan een aantal regels, waardoor optellen werkt zoals we gewend zijn van getallen.*

---
layout: image-right
image: vec_add.svg
---

# Regels voor optellen


### Associativiteit 
$$\ket u + \ket v = \ket v + \ket u$$
### Commutativiteit
$$\big(\ket u + \ket v\big) + \ket w = \ket u + \big(\ket v + \ket w\big)$$
### Identiteit
$$\exist\ \ket 0 \text{ zodat } \ket 0 + \ket v = \ket v = \ket v + \ket 0$$
**Er bestaat voor iedere ruimte een vector $\ket 0$ die als nul-element fungeert**
$$\ket 0 = \begin{bmatrix} 0 \\ \vdots \\ 0 \end{bmatrix}$$

---
layout: image-right
image: vec_add.svg
---

# Vectoren aftrekken

Aftrekken wordt gedefinieerd aan de hand van optellen met een inverse, net als bij getallen:
$$2 - 1 = 2 + (-1)$$

### Inverse
$$\forall\ \ket v\ \ \exists\ket{-v} \text{ zodat }  \ket v + \ket{-v} = \ket 0$$
**Er bestaat voor elke vector $\ket v$ in iedere ruimte een inverse $-\ket v$**

$$\ket{v} = \begin{bmatrix}1 \\ 2 \end{bmatrix} \iff \ket{-v} = \begin{bmatrix} -1 \\ -2 \end{bmatrix}$$
$$\ket{u} = \begin{bmatrix}3 \\ -1 \end{bmatrix} \iff \ket{-u} = \begin{bmatrix} -3 \\ 1 \end{bmatrix}$$

---
layout: image-right
image: vec_scale.svg
---

# Schalen (scalair product)

  - Vermeniguldigen met een gewoon (scalair) getal
  - Deze getallen komen uit dezelfde verzameling als de getallen binnen de vectoren ($\mathbb R$)
  - Veelvouden van $\ket v$ vormen een soort getallijn

### Numeriek

We vermenigvuldigen elk getal in de vector:

$$2 \ket v = 2 \cdot \begin{bmatrix}1 \\ 2 \end{bmatrix} = \begin{bmatrix}2 \cdot 1 \\ 2 \cdot 2 \end{bmatrix} = \begin{bmatrix}2 \\ 4 \end{bmatrix}$$
$$-1 \cdot \ket v = -1 \cdot \begin{bmatrix}1 \\ 2 \end{bmatrix} = \begin{bmatrix}-1 \cdot 1 \\ -1 \cdot 2 \end{bmatrix} = \begin{bmatrix}-1 \\ -2 \end{bmatrix} = \ket{-v}$$
$$0 \cdot \ket v = 0 \cdot \begin{bmatrix}1 \\ 2 \end{bmatrix} = \begin{bmatrix}0 \cdot 1 \\ 0 \cdot 2 \end{bmatrix} = \begin{bmatrix}0 \\ 0 \end{bmatrix} = \ket 0$$

---
layout: image-right
image: vec_dist.svg
---

# Regels voor schalen

*Ook hier zijn er regels die maken dat rekenen met vectoren zoveel mogelijk werkt als we gewend zijn:*

### Identiteit 
Schalen met een factor $1$ doet niets
$$1 \ket v = \ket v$$

### Combinatie met normaal product
Het maakt niet uit in welke volgorde we scalair product en "normaal product" uitvoeren
$$a \cdot \big(b \cdot \ket v\big) = \big(a \cdot b\big) \cdot \ket v$$


TODO plaatje

---
layout: image-right
image: vec_dist.svg
---

# Distributiviteit
Het principe van distributie kennen we van getallen:
$$2 \cdot (3 + 1) = 2 \cdot 3 + 2 \cdot 1$$

### Distributiviteit over vector som
Schalen van een som is hetzelfde als de som van geschaalde vectoren
$$a \cdot \big(\ket u + \ket v\big) = a \cdot \ket u + a \cdot \ket v$$
### Distributiviteit over scalaire som
Schalen met een som is hetzelfde als de som van geschaalde vectoren
$$(a + b) \cdot \ket v = a \cdot \ket v + b \cdot \ket v$$

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

<hsp />
<hsp />
<hsp />
<hsp />

## Bonus
- Iets meer dan de helft van de regels werkt ook voor bijvoorbeeld `str` in Python. **Welke niet, en waarom?**

---
layout: chaptertitle
---

# [LA-2] Vectoren en lineaire combinaties

---
layout: image-right
---

# Lineaire combinaties

Door vectoren te schalen en op te tellen, kunnen we bestaande vectoren combineren:

$$\ket v = \begin{bmatrix}1 \\ 2 \end{bmatrix}\qquad \ket u = \begin{bmatrix}3 \\ -1 \end{bmatrix}$$

<hsp />

$$2 \ket v + 3 \ket u = 2 \begin{bmatrix}1 \\ 2 \end{bmatrix} + 3 \begin{bmatrix}3 \\ -1 \end{bmatrix} = \begin{bmatrix}2 \\ 4 \end{bmatrix} + \begin{bmatrix}9 \\ -3 \end{bmatrix} = \begin{bmatrix}12 \\ 1 \end{bmatrix}$$

In dit geval kunnen we elke vector schrijven als een som van $\ket u$ en $\ket v$.

*Maar...* **Kan dit altijd?**

<div style="font-size: 0.9rem; margin-top: 30px">

**net als bij normale vermenigvuldiging laten we het multiplicatieteken vaak weg bij het scalair product, en gebruiken we $2 \ket x$ als shorthand voor $2 \cdot \ket x$*

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

- Met een lineair onafhankelijk set van $n$ vectoren kunnen we een $n$ dimensionale ruimte defini&euml;ren
- De vectoren geven een nieuw coordinatensysteem, dit noemen we de *basis*
  - Meestal werken we met de standaardbasis, bijvoorbeeld voor 3D:

  $$\ket {e_1} = \begin{bmatrix}1 \\ 0 \\ 0\end{bmatrix} \qquad \ket {e_2} = \begin{bmatrix}0 \\ 1 \\ 0\end{bmatrix} \qquad \ket {e_3} = \begin{bmatrix}0 \\ 0 \\ 1\end{bmatrix}$$
  - De vectoren hebben een standaard-lengte $1$ en staan haaks op elkaar --- dit rekent het makkelijkst

<hsp />

**We kunnen de vector vectoren nu in termen van de basis schrijven**

$$\ket u = \begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix} \quad \iff \quad \ket u = 1 \ket {e_1} + 2 \ket {e_2} + 3 \ket {e_3}$$

---
layout: image-right
image: ltf.gif
---

# Dimensionaliteit van een basis

- Lengte vectoren niet belangrijk, maar aantal vectoren dat lineair onafhankelijk is, *bijvoorbeeld*

  $$\ket u = \begin{bmatrix}1 \\ 2 \\ 3\end{bmatrix} \qquad \ket v = \begin{bmatrix}3 \\ 2 \\ 1\end{bmatrix} \qquad \ket w = \begin{bmatrix}-2 \\ 0 \\ 2\end{bmatrix}$$

- De set $\big\{ \ket u, \ket v, \ket w \big\}$ is niet lineair onafhankelijk, maar elke subset van twee vectoren is dit wel
- We hebben een basis voor een 2D-ruimte, niet 3D

---

# Inwendig product

**Kunnen we vectoren vermenigvuldigen?** In tegenstelling tot wat we gewend zijn, zijn er meerdere producten voor vectoren. De belangrijkste is het inwendig product $\langle u \mid v \rangle$, dat twee vectoren "vermenigvuldigt" tot een getal:

$$\ket v = \begin{bmatrix}1 \\ 2 \end{bmatrix}\qquad \ket u = \begin{bmatrix}3 \\ -1 \end{bmatrix}\qquad\Rightarrow\qquad\langle v \mid u \rangle = 1 \cdot 3 + 2 \cdot -1 = 3 - 2 = 1$$

Het inwendig product wordt ook wel geschreven als $\vec v \cdot \vec u$ of $\langle v, u \rangle$. In bepaalde contexten kun je ook de naam "dot-product" tegenkomen. In Python / Numpy gebruik je de `u.dot(v)` functie of `u @ v`.

- De waarde van een inwendig product hangt van een aantal dingen af:
  - Hoe groter de vectoren die erin gaan, hoe groter het inwendig product
  - Hoe meer vectoren op elkaar lijken, hoe groter het inwendig product
    - Twee vectoren die dezelfde kant op wijzen, hebben een positief product
    - Twee vectoren die van elkaar afwijzen, hebben een negatief product
    - Twee vectoren die haaks op elkaar staan, hebben een product van $0$

<hsp />

**Merk op dat de volgorde van de vectoren net zo goed andersom had kunnen zijn, en de uitkomst gelijk was geweest. Toch geven we beide varianten een andere betekenis.**

---

# Rij-vectoren

In de originele berekening hadden we:

$$\langle v \mid u \rangle = 1 \cdot 3 + 2 \cdot -1 = 3 - 2 = 1$$

In dit geval beschouwen we de vector $\bra v$ als een soort van functie, die van de vector $\ket u$ een normaal getal in $\mathbb R$ maakt. In deze context schrijven we de vector als $\bra v$, en de waardes ervan in een rij.

$$\begin{bmatrix}1 & 2\end{bmatrix} \begin{bmatrix}3 \\ -1\end{bmatrix}$$

In het algemeen maken we een onderscheid tussen rij-vectoren (ookwel covectoren), geschreven als $\bra v$, en kolom-vectoren, $\ket u$. Een kolom-vector bevat data, een rij vector bevat gewichten voor een gewogen som.

### Andersom

$$\langle u \mid v \rangle = \begin{bmatrix}3 & -1\end{bmatrix} \begin{bmatrix}1 \\ 2\end{bmatrix} = 3 \cdot 1 + -1 \cdot 2 = 3 - 2 = 1$$

**De uitkomst is steeds gelijk, het verschil tussen kolom en rij zit in hoe we de vector zien: als data of als actie.**

---
layout: image-right
image: pythagoras.jpg
---

# Norm

We kunnnen het inwendig product gebruiken om de lengte van een vector te bepalen:

$$\lvert u \rvert = \sqrt{\langle u\mid u \rangle}$$

Bijvoorbeeld:

$$\ket v = \begin{bmatrix}3 \\ 4 \end{bmatrix}\qquad\qquad \begin{align*}\lvert v \rvert &= \sqrt{\langle u\mid u \rangle} \\&= \sqrt{3^2 + 4^2} \\&= \sqrt{25} \\&= 5\end{align*}$$

Dit is eigenlijk gewoon de formule van Pythagoras:

$$a^2 + b^2 = c^2$$

*De norm van een vector is altijd een normaal getal groter of gelijk aan $0$.*


---
layout: image-right
image: cos.gif
---

# Cosine Similarity

- De waarde van een inwendig product hing af van een aantal dingen:
  - De lengte van de vectoren
  - De hoek tussen de vectoren

**Dit kunnen we iets exacter maken:**

*De waarde van het inwendig product is het product van de lengte van beide vectoren met de cosinus van de hoek tussen de vectoren.*

$$\langle u\mid v \rangle
=\lvert u\vert \vert v\vert \cos\theta$$

Dit geeft de cosine similarity --- een getal dat uitdrukt hoe sterk twee vectoren gelijke richting hebben op een schaal van $-1$ tot $1$:

$$S_C (u,v):= \cos(\theta) = {\langle u \mid v \rangle \over \lvert u\rvert \ \lvert v\rvert}
= \frac{ \langle u \mid v \rangle }{ \langle u \mid u \rangle \langle v \mid v \rangle }$$

---
layout: image-right
image: vec_proj.svg
---

# Projecties

We kunnen de normale basisvectoren gebruiken om elementen uit een vector te halen:

$$\ket{e_1} = \begin{bmatrix}1 \\ 0\end{bmatrix}\qquad \ket{e_2} = \begin{bmatrix}0 \\ 1\end{bmatrix}$$
$$\ket v = \begin{bmatrix}3 \\ 4\end{bmatrix}\qquad \langle e_1 \mid u \rangle = 3\qquad \langle e_2 \mid u \rangle = 4$$

Dit is de projectie van de vector of de $x$- en $y$-as.

Op dezelfde manier kunnen we op een arbitraire vector projecteren, bijvoorbeeld

$$\ket p = \begin{bmatrix}2 \\ 1\end{bmatrix}\qquad \langle p \mid v \rangle = 10 \qquad \frac{\langle p \mid v \rangle}{\langle p \mid p \rangle} = \frac{10}{5} = 2$$
$$\frac{\langle p \mid v \rangle}{\langle p \mid p \rangle}\ket{p} = 2  \begin{bmatrix}2 \\ 1 \end{bmatrix} = \begin{bmatrix}4 \\ 2 \end{bmatrix}$$

---
layout: image-right
image: vec_proj.svg
---

# Decompositie

Gegeven
$$\ket v = \begin{bmatrix}3 \\ 4\end{bmatrix}\qquad \ket p = \begin{bmatrix}2 \\ 1\end{bmatrix}$$

hebben we de projectie $\text{proj}_{\ket p}(\ket v)$ van $\ket v$ op $\ket p$ berekend met
$$\frac{\langle p \mid v \rangle}{\langle p \mid p \rangle}\ket{p} = 2  \begin{bmatrix}2 \\ 1 \end{bmatrix} = \begin{bmatrix}4 \\ 2 \end{bmatrix}$$

Hiermee kunnen we de vector $\ket v$ in twee&euml;n splitsen:
- Het deel parallel aan $\ket p$, i.e. ${\color{#ff33ff}\ket v_{\parallel p}} = \text{proj}_{\color{#0099ff}\ket p}({\color{#da291c}\ket v})$
- Het deel haaks op $\ket p$, i.e. ${\color{#ff9900}\ket v_{\perp p}} = {\color{#da291c}\ket v} - {\color{#ff33ff}\ket v_{\parallel p}}$

---
layout: image-right
image: conformal.gif
---

# Transformaties

Functies werken op individuele vectoren, maar ook op hele ruimtes.

- Lineaire transformaties
  - Uitrekken / Schalen
  - Rotatie
  - Shears

- Niet-lineaire transformaties
  - Buiten de focus van lineaire algebra
  - Wel belangrijk in bijv. neurale netwerken
    - *Activatielaag*
  - Kan nog steeds afgekaderd zijn, e.g. conforme afbeelding

---

# Lineaire transformaties

Een transformatie is lineair als deze:
- De oorsprong in stand houdt, d.w.z. de nul-vector blijft de nul-vector
- Parallelle lijnen blijven parallel
- Afstanden behouden dezelfde verhouding
- Oppervlaktes schalen met een vaste factor

<hsp />

**Een lineaire transformatie in $n$-dimensies is te defini&euml;ren met $n$ vectoren binnen deze ruimte: elke vector beschrijft dan waar exact een basis-vector naartoe getransformeerd wordt.**

*Alle andere vectoren zijn te formuleren als lineaire combinaties van de basis-vectoren, een getransformeerde vector is dezelfde lineaire combinatie van de getransformeerde basisvectoren.*

---
layout: iframe
url: lin_trans.html
---

---
layout: image-right
image: thematrix.jpg
---

# Matrices

Een lineaire functie van vector naar vector in $n$ dimensies is te schrijven met $n$ vectoren (met elk $n$ elementen). Dit betekent dat $n \times n$ getallen genoeg zijn om een lineaire transformatie uit te drukken.

- Omdat we hier vaak mee moeten werken speciale notatie: *de matrix*

$$\mathbf{M} = \begin{bmatrix}1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9\end{bmatrix} \qquad \mathbf M \in \mathbb R^{3 \times 3}$$

- Matrices zijn een op zichzelf staand wiskundig object
  - Getypeerd o.b.v. dimensies (2 getallen), niet per s&eacute; vierkant
  - Voldoen aan alle eisen van vectoren (optellen, schalen)

---

# Matrix-vector Multiplicatie

- Om een matrix-transformatie op een vector toe te passen, gebruiken we een vermenigvuldiging of product.
- Hiertoe gaan we de matrix beschouwen als een rij van kolommen:

$$\mathbf{M} = \begin{bmatrix}1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9\end{bmatrix} = \begin{bmatrix}\begin{bmatrix} 1 \\ 4 \\ 7\end{bmatrix}  & \begin{bmatrix}2 \\ 5 \\ 8\end{bmatrix}  & \begin{bmatrix}3 \\ 6 \\ 9\end{bmatrix} \end{bmatrix} \qquad\qquad \ket v = \begin{bmatrix}1 \\0 \\-1\end{bmatrix}$$

- Met deze matrix notatie en de voorbeeld-vector $\ket v$ kunnen we dezelfde stappen toepassen als in het inwendig product:
  -  ~~Elke waarde uit de rij-vector~~ **elke kolom uit de matrix** wordt vermenigvuldigd met elke waarde uit de kolom-vector
  - Het resultaat wordt bij elkaar opgeteld

$$\mathbf{M}\ket v = \begin{bmatrix}\begin{bmatrix} 1 \\ 4 \\ 7\end{bmatrix}  & \begin{bmatrix}2 \\ 5 \\ 8\end{bmatrix}  & \begin{bmatrix}3 \\ 6 \\ 9\end{bmatrix} \end{bmatrix} \begin{bmatrix}1 \\0 \\-1\end{bmatrix} = 1\begin{bmatrix}1 \\ 4 \\ 7 \end{bmatrix} + 0\begin{bmatrix}2 \\ 5 \\ 8 \end{bmatrix} -1\begin{bmatrix}3 \\ 6 \\ 9 \end{bmatrix} = \begin{bmatrix}-2 \\ -2 \\ -2 \end{bmatrix} $$

---

# Niet vierkante matrices

Een matrix hoeft niet vierkant te zijn; voor vermenigvuldiging met een vector is alleen van belang dat de matrix het juiste aantal kolommen heeft:

$$\begin{bmatrix}\begin{bmatrix} 1 \\ 4 \end{bmatrix}  & \begin{bmatrix}2 \\ 5 \end{bmatrix}  & \begin{bmatrix}3 \\ 6 \end{bmatrix} \end{bmatrix} \begin{bmatrix}1 \\0 \\-1\end{bmatrix} = 1\begin{bmatrix}1 \\ 4  \end{bmatrix} + 0\begin{bmatrix}2 \\ 5  \end{bmatrix} -1\begin{bmatrix}3 \\ 6  \end{bmatrix} = \begin{bmatrix}-2 \\ -2  \end{bmatrix} $$

Hier werd een 3D vector door een rechthoekige matrix naar $\mathbb R^2$ getransformeerd.

$$\begin{bmatrix}\begin{bmatrix} 1 \\ 4 \\ 7\end{bmatrix}  & \begin{bmatrix}2 \\ 5 \\ 8\end{bmatrix}  \end{bmatrix} \begin{bmatrix}6 \\3 \end{bmatrix} = 6\begin{bmatrix}1 \\ 4 \\ 7 \end{bmatrix} + 3\begin{bmatrix}2 \\ 5 \\ 8 \end{bmatrix} = \begin{bmatrix}12 \\ 39 \\ 66 \end{bmatrix} $$

Hier werd een 2D vector in $\mathbb R^3$ geplaatst. **Merk op deze matrix maar 2 basis-vectoren kan gebruiken om 3D-vectoren mee te bouwen, dus alle vectoren die uit deze transformatie komen zullen in een 2D vlak liggen binnen de 3D ruimte.**

---

# Matrix-matrix multiplicatie

We kunnen ook twee matrices met elkaar vermenigvuldigen.
- Conceptueel betekent dit dat we twee lineaire transformaties combineren door ze na elkaar toe te passen.
- $\mathbf N \mathbf M$ betekent dat eerst $\mathbf{M}$ wordt toegepast, en daarna $\mathbf{N}$.
  - We gaan dus van rechts naar links, net als bij functies: $\mathbf N \mathbf M \ket x \cong N(M(x))$

&nbsp;

## Calculatie
Om twee matrices te vermenigvuldigen, beschouwen we de tweede matrix als een rij van kolommen:

$$\mathbf M = \begin{bmatrix}1 & 0 \\ 2 & -1\end{bmatrix} \qquad\mathbf N = \begin{bmatrix}3 & 4 \\ 5 & 0\end{bmatrix} \Rightarrow \begin{bmatrix}\begin{bmatrix}3 \\ 5\end{bmatrix} & \begin{bmatrix} 4 \\ 0 \end{bmatrix} \end{bmatrix}$$


---

# Matrix-matrix multiplicatie

Nu kunnen we de matrix $\mathbf M$ individueel vermenigvuldigen met kolommen van $\mathbf N$. De resulterende kolommen zetten we op dezelfde volgorde terug in de rij.

$$\begin{align*}\mathbf M \mathbf N &=
{ \color{#aaaaaa} \begin{bmatrix}1 & 0 \\ 2 & -1 \end{bmatrix} }
\begin{bmatrix}\color{#ff00aa} \begin{bmatrix}3 \\ 5\end{bmatrix} & \color{#00aaff} \begin{bmatrix} 4 \\ 0 \end{bmatrix} \end{bmatrix} \\[5mm]
&= \begin{bmatrix}
\color{#ff00aa} \begin{bmatrix}1 & 0 \\ 2 & -1\end{bmatrix}  \begin{bmatrix}3 \\ 5 \end{bmatrix} &
\color{#00aaff} \begin{bmatrix}1 & 0 \\ 2 & -1\end{bmatrix}  \begin{bmatrix}4 \\ 0 \end{bmatrix} 
\end{bmatrix} \\[5mm]
&= \begin{bmatrix}
\color{#ff00aa} \begin{bmatrix}\begin{bmatrix}1 \\ 2\end{bmatrix} & \begin{bmatrix} 0 \\ -1\end{bmatrix}\end{bmatrix}  \begin{bmatrix}3 \\ 5 \end{bmatrix} &
\color{#00aaff} \begin{bmatrix}\begin{bmatrix}1 \\ 2\end{bmatrix} & \begin{bmatrix} 0 \\ -1\end{bmatrix}\end{bmatrix}  \begin{bmatrix}4 \\ 0 \end{bmatrix} 
\end{bmatrix} \\[5mm]
&= \begin{bmatrix}
\color{#ff00aa} 3 \cdot \begin{bmatrix}1 \\ 2\end{bmatrix} + 5 \cdot \begin{bmatrix}0 \\ -1 \end{bmatrix} &
\color{#00aaff} 4 \cdot \begin{bmatrix}1 \\ 2\end{bmatrix} + 0 \cdot \begin{bmatrix}0 \\ -1 \end{bmatrix} 
\end{bmatrix} \\[5mm]
&= \begin{bmatrix}
\color{#ff00aa} \begin{bmatrix}3 \\ 1\end{bmatrix} & \color{#00aaff} \begin{bmatrix}4 \\ 8 \end{bmatrix} 
\end{bmatrix} \\[5mm]
\end{align*}$$

---

# Matrices als getallen

- Matrix-vermenigvuldiging geeft een tweede manier om 2 matrices tot 1 te combineren (naast optellen)
- Voor vierkante matrices blijft het resultaat in de familie: $\mathbb R^{n\times n} \times \mathbb R^{n\times n} \to \mathbb R^{n\times n}$
- Matrices zijn daarmee  te beschouwen als een soort supercharged getallen (!)

<hsp />

### Rekenregels
Vrijwel alle rekenregels voor re&euml;ele getallen gaan ook op voor matrices:
- Identiteit (vermenigvuldiging)
$$\mathbf I = \begin{bmatrix}1 & 0 & 0\\0 & 1 & 0\\0 & 0 & 1\end{bmatrix}$$
- Distributie $\mathbf M (\mathbf N + \mathbf O) = \mathbf M \mathbf N + \mathbf M \mathbf O$ en $(\mathbf M + \mathbf N) \mathbf O = \mathbf M \mathbf O + \mathbf N \mathbf O$ 
- Associativiteit: $\mathbf M (\mathbf N \mathbf O) = (\mathbf M \mathbf N) \mathbf O)$
- **Maar niet commutativiteit**: $\mathbf N \mathbf O \not= \mathbf O \mathbf N$ **!**
  - *(voor 2 specifieke matrices kan het zo uitkomen dat de volgorde niet uitmaakt)*



---
layout: chaptertitle
---

# [LA-3] Matrices en Tensoren


---

# Systemen van vergelijkingen

Een matrix is ook te lezen als een systeem van vergelijkingen met onbekenden. Geveven de matrix van een paar slides terug, representeert deze het volgende systeem van drie vergelijkingen met 3 onbekenden:

$$\mathbf{M} = \begin{bmatrix}3 & 2 & 4 \\ 1 & 2 & 1 \\ 3 & 5 & 0\end{bmatrix} \qquad \iff \qquad \begin{align*} 3x + 2y + 4z \\ 1x + 2y + 1z \\ 3x + 5y + 0z \end{align*}$$

Door een uitkomst voor de vergelijkingen te defini&euml;ren kunnen we op zoek naar een oplossing:

$$\mathbf{M} = \begin{bmatrix}3 & 2 & 4 \\ 1 & 2 & 1 \\ 3 & 5 & 0\end{bmatrix}\begin{bmatrix}x \\ y \\ z\end{bmatrix}=\begin{bmatrix}26 \\ 13 \\ 0 \end{bmatrix}  \qquad \iff \qquad \begin{align*} 3x + 2y + 4z = 26 \\ 1x + 2y + 1z = 13 \\ 3x + 5y + 0z = 0 \end{align*}$$

In dit geval heeft het systeem een unieke oplossing, die we kunnen vinden met Gauss-Jordan Eliminatie

---

# Gauss-Jordan Eliminatie

Hiertoe schrijven we de matrix-vergelijking in een minimale vorm:

$$\begin{bmatrix}
    3 & 2 & 4 &\bigm| & 26 \\
    1 & 2 & 1 &\bigm| & 13 \\
    3 & 5 & 0 &\bigm| & 0 \\ 
\end{bmatrix}$$

Hier kunnen we vervolgens rij-operaties op toepassen:
 - Een rij mag een $n$ aantal keer bij een andere rij worden opgeteld / afgetrokken
 - Een rij kan gedeeld worden door een getal

We kunnen bijvoorbeeld de middelste rij keer drie doen:
$$\begin{bmatrix}
    3 & 2 & 4 &\bigm| & 26 \\
    3 & 6 & 3 &\bigm| & 39 \\
    3 & 5 & 0 &\bigm| & 0 \\ 
\end{bmatrix}$$

---

Vervolgens kunnen we de onderste rij van de middelste aftrekken:

$$\begin{bmatrix}
    3 & 2 & 4 &\bigm| & 26 \\
    3 & 6 & 3 &\bigm| & 39 \\
    3 & 5 & 0 &\bigm| & 0 \\ 
\end{bmatrix} \to \begin{bmatrix}
    3 & 2 & 4 &\bigm| & 26 \\
    0 & 1 & 3 &\bigm| & 39 \\
    3 & 5 & 0 &\bigm| & 0 \\ 
\end{bmatrix}$$

Vervolgens: 
$$\begin{bmatrix}
    3 & 2 & 4 &\bigm| & 26 \\
    0 & 1 & 3 &\bigm| & 39 \\
    0 & 3 & -4 &\bigm| & -26 \\ 
\end{bmatrix} \to_{R_3 -= 3R_2} \begin{bmatrix}
    3 & 2 & 4 &\bigm| & 26 \\
    0 & 1 & 3 &\bigm| & 39 \\
    0 & 0 & -13 &\bigm| & -143 \\ 
\end{bmatrix} \to_{R_3 /= -13} \begin{bmatrix}
    3 & 2 & 4 &\bigm| & 26 \\
    0 & 1 & 3 &\bigm| & 39 \\
    0 & 0 & 1 &\bigm| & 11 \\ 
\end{bmatrix}\to_{R_2 -= 3R_3} $$

$$\begin{bmatrix}
    3 & 2 & 4 &\bigm| & 26 \\
    0 & 1 & 0 &\bigm| & 6 \\
    0 & 0 & 1 &\bigm| & 11 \\ 
\end{bmatrix} \to_{R_1 -= 2R_2} \begin{bmatrix}
    3 & 0 & 4 &\bigm| & 14 \\
    0 & 1 & 0 &\bigm| & 6 \\
    0 & 0 & 1 &\bigm| & 11 \\ 
\end{bmatrix} \to_{R_1 -= 4R_3}  \begin{bmatrix}
    3 & 0 & 0 &\bigm| & -30 \\
    0 & 1 & 0 &\bigm| & 6 \\
    0 & 0 & 1 &\bigm| & 11 \\ 
\end{bmatrix} \to_{R_1 /= 3}$$

Na de laatste stap hebben we een identiteitsmatrix, en kunnen we de antwoorden aflezen:
$$\begin{bmatrix}
    1 & 0 & 0 &\bigm| & -10 \\
    0 & 1 & 0 &\bigm| & 6 \\
    0 & 0 & 1 &\bigm| & 11 \\ 
\end{bmatrix} \qquad \Rightarrow \qquad \begin{align*} x = -10 \\ y = 6 \\ z = 11 \end{align*}\qquad \Rightarrow \qquad
\begin{align*} 3 \cdot -10 + 2 \cdot 6 + 4 \cdot 11 = 26 \\ 1 \cdot -10 + 2 \cdot 6 + 1 \cdot 11 = 13 \\ 3 \cdot -10 + 5 \cdot 6 + 0 \cdot 11 = 0 \end{align*}$$

---

# Over- en ondergedetermineerde systemen

In dit geval was er een unieke oplossing voor het systeem van vergelijkingen. **Dit is niet altijd het geval --- een systeem kan ook $0$ of oneindig oplossingen hebben.**

$$\begin{align*} x + y &= 0 \\ x + y &= 3\end{align*}$$

heeft geen oplossingen (overgedetermineerd)

$$\begin{align*} x + y &= 0 \\ x + y &= 0\end{align*}$$

heeft er oneindig (ondergedetermineerd).

**Of een systeem een unieke oplossing heeft, hangt af van de matrix; of een systeem zonder unieke oplossing er $0$ of oneindig heeft, hangt af van de vector (rechterkant is).**

---

# Determinant
Om te bepalen hoeveel oplossingen er zijn kunnen we de determinant van de matrix nemen:

- Een matrix met unieke oplossing heeft een determinant die niet $0$ is. 
- Een determinant van 0 komt overeen met een lineaire transformatie die een of meer dimensie verliest,
  - E.g. een matrix die een 3D ruimte projecteert naar 2D of 1D.
- Een matrix met een determinant $\not = 0$ is **omkeerbaar**, we kunnen er door delen.

**De determinant vertelt de factor van de schaling die de matrix uitvoert; in 2D betreft dit de oppervlakten, in 3D de inhoud, etc. Bij een determinant van 0 gaan we bijvoorbeeld van 3D naar 2D, en wordt de inhoud 0.**

<hsp />
<hsp />
<hsp />
<hsp />

### Formule in 2D en 3D

Voor $\mathbf{M} = \begin{bmatrix} a & b \\ c & d\end{bmatrix}$ is de determinant te berekenen met $\det(\mathbf M) = ad - bc$

Voor $\mathbf{M} = \begin{bmatrix} a & b & c \\ d & e & f \\ g & h & i \end{bmatrix}$ is de determinant $\det(\mathbf M) = aei + bfg + cdh - gec - hfa - idb$

---

# Niet vierkante matrices

- Hebben geen determinant en is niet omkeerbaar.
- Zijn met elkaar te vermenigvuldigen, afhankelijk van de vormen van beide matrices:
$$\mathbb R^{m\times n} \times \mathbb R^{n \times k} \to \mathbb R^{m \times k}$$
- De vorm van het resultaat is bepaald door de vorm van de beide matrices.
- Een manier om dit te checken, de vorm van het resultaat te weten, en de berekening van de elementen te onthouden is als volgt:

$$\begin{align*}
&\begin{bmatrix}3 & 4 \\ 5 & 0 \\ 1 & 3 \\ 2 & 1\end{bmatrix} \\
\underbrace{\begin{bmatrix}1 & 0 & -2 & 0 \\ 2 & -1 & 3 & 1 \\ 0 & -2 & 1 & 1\end{bmatrix}}_{\mathbb R^{\textcolor{#00aaff}{3} \times \textcolor{red}{4}}}
\underbrace{\begin{bmatrix}3 & 4 \\ 5 & 0 \\ 1 & 3 \\ 2 & 1\end{bmatrix}}_{\mathbb R^{\textcolor{red}{4} \times \textcolor{#00aaff}{2}}}
\Rightarrow
\begin{bmatrix}1 & 0 & -2 & 0 \\ 2 & -1 & 3 & 1 \\ 0 & -2 & 1 & 1\end{bmatrix}
&\underbrace{\begin{bmatrix}a & b \\ \_ & \_ \\ \_ & \_ \end{bmatrix}}_{\mathbb R^{\textcolor{#00aaff}{3} \times \textcolor{#00aaff}{2}}}
\begin{matrix}
\qquad a =& 1 \cdot 3 + 0 \cdot 5 -2 \cdot 1 + 0 \cdot 2 \\
\qquad b =& 1 \cdot 4 + 0 \cdot 0 -2 \cdot 3 + 0 \cdot 1 \\
\qquad c =& \dots
\end{matrix}
\end{align*}$$

---
layout: image-right
image: Matrix_transpose.gif
---

# Transpositie

Niet vierkante matrices zijn dus niet altijd met elkaar te combineren, maar soms kan het wel bijna...  Een mogelijkheid om het puzzelstukje te laten passen kan dan zijn om deze te draaien. Bij vectoren en matrices is hier een standaard manier voor, *transpositie*.

Bij transpositie worden de elementen in een matrix of vector gespiegeld:
- Een kolom wordt een rij
- Een rij wordt een kolom
- Een matrix wordt gespiegeld over de diagonaal (plaatje!)

---

# Oefening

TODO aantal berekeningen

---
layout: image-right
image: tensor.svg
---

# Tensoren

- De notatie met kolommen voor vectoren en de manier waarop de elementen in een matrix toegepast worden, is (slechts) een afspraak
- We werken toe naar tensoren: een categorie waar o.a. vectoren en matrices onder vallen
    - Getallen zijn 0D tensoren (geen index)
    - Vectoren zijn 1D tensoren (1 index)
    - Matrices zijn 2D tensoren (2 indices)
    - Orde-3 tensoren zijn 3-dimensionaal: een kubus van getallen(!)
- In dit geval worden weergave en het praten in rijen en kolommen snel dubbelzinnig
- Daarom notatie in termen van van basis-&ZeroWidthSpace;(co)vectoren

---

# Covectoren

- Covectoren zijn de rij-vectoren die we eerder al zagen in het inwendig product.
- Conceptueel zien we de covector als een functie $\mathbb R^n \to \mathbb{R}$
  - Weergave in computergeheugen is identiek, maar gedraagt zich anders met basis-verandering
      - Vector: Basis vectoren twee keer zo groot $\to$ elementen halveren (compenseren)
      - Covectoren: Basis vectoren twee keer zo groot $\to$ elementen verdubbelen mee

**Een covector is een functie, hoe plotten we die?**

---
layout: image-right
image: covector.svg
---

# Covectoren als contouren

**Plot de covector $\bra k = \begin{bmatrix}1 & \frac12  \end{bmatrix}$**

*We kunnen per waarde $n \in \mathbb R$ een lijn tekenen voor alle vectoren $\ket v$ zodat $\langle k \mid v \rangle = n$*

Voor $n = 0$ liggen o.a. $\begin{bmatrix}0\\0\end{bmatrix}$ en $\begin{bmatrix}1\\-2\end{bmatrix}$ op de lijn
<hsp />
Voor $n = 1$ liggen o.a. $\begin{bmatrix}1\\0\end{bmatrix}$ en $\begin{bmatrix}0\\2\end{bmatrix}$ op de lijn

Met deze lijnen maken we een contour-map:

- In 2D is dit een reeks paralelle lijnen
- In 3D worden de lijnen 2D vlakken
- In algemene zin hyperplanes van dimensie $n-1$

---
layout: image-right
image: vector-basis.svg
---

# Basis-notatie

Net als dat we een basis-vector kunnen schrijven in termen van basis-vectoren:

$$\begin{bmatrix} 1 \\ 2 \end{bmatrix} \iff 1e_1 + 2e_2 \text{ waar } e_1 = \begin{bmatrix} 1 \\ 0 \end{bmatrix}\text{ en } e_2 = \begin{bmatrix} 0 \\ 1 \end{bmatrix}$$

Doen we nu hetzelfde voor covectoren (rijen):

$$\epsilon^1 = \begin{bmatrix} 1 & 0 \end{bmatrix}$$
$$\epsilon^2 = \begin{bmatrix} 0 & 1 \end{bmatrix}$$
$$\begin{bmatrix} 1 & 2 \end{bmatrix} \iff 1\epsilon^1 + 2\epsilon^2$$

*Voor basis-covectoren gebruiken we de griekse letter $\epsilon$ (epsilon) en noteren de index hoog i.p.v. laag*

---

# Matrix producten in basis-notatie

- We kunnen matrices beschouwen als een vector- en een covector component: een vector wordt door het-covector deel geabsorbeerd om een nieuwe vector te maken
- Deze combineren we (denk als een tuple) met het tensor-product $\otimes$
- De basis van een matrix schrijven we aan de hand van basis-matrices in de set $\{ e_1\otimes\epsilon^1, e_1\otimes\epsilon^2, \dots, e_2\otimes\epsilon^1, \dots, e_n\otimes\epsilon^n \}$

$$e_1\otimes\epsilon^1 = \begin{bmatrix}1 & 0 \\ 0 & 0\end{bmatrix} \qquad e_1\otimes\epsilon^2 = \begin{bmatrix}0 & 1 \\ 0 & 0\end{bmatrix}$$
$$e_2\otimes\epsilon^1 = \begin{bmatrix}0 & 0 \\ 1 & 0\end{bmatrix} \qquad e_2\otimes\epsilon^2 = \begin{bmatrix}0 & 0 \\ 0 & 1\end{bmatrix}$$

*In een matrix-vector of matrix-matrix vermenigvuldiging gaan we steeds de termen vermenigvuldigen, de getallen naar voren halen, en dan de volgende vereenvoudiging toepassen:*

$$\epsilon^i e_j = \begin{cases} 1 \text{ if }  i = j \\ 0 \text{ if } i\ne j \end{cases}$$

---
layout: two-cols-header
---

# Basis-notatie: Matrix-vector

::left::

$$\mathbf M = \begin{bmatrix}\color{#ff00aa} 1 & \color{#66ffaa} 0 \\ \color{#00aaff} 2 & \color{#ffff99} -1 \end{bmatrix}$$
$$\ket v = \begin{bmatrix}\color{#ff33ff} 7 \\ \color{#ff9900} 6 \end{bmatrix}$$
$$\Updownarrow$$
$$\begin{align*}\mathbf M &= {\color{#ff00aa} 1}{\color{grey}e_1\otimes\epsilon^1} + {\color{#66ffaa}0}{\color{grey}e_1\otimes\epsilon^2} \\&+ {\color{#00aaff}2}{\color{grey}e_2\otimes\epsilon^1} {\color{#ffff99}\ -\ 1} {\color{grey}e_2\otimes\epsilon^2}\end{align*}$$
$$\ket v = {\color{#ff33ff}7}{\color{grey}e_1} + {\color{#ff9900}6}{\color{grey}e_2}$$

&nbsp;

$$\epsilon^i e_j = \begin{cases} 1 \text{ if }  i = j \\ 0 \text{ if } i\ne j \end{cases}$$

::right::

$$\begin{align*}\mathbf M \ket v &= \left({\color{#ff00aa}1}{\color{grey}e_1\otimes\epsilon^1} + {\color{#66ffaa}0}{\color{grey}e_1\otimes\epsilon^2} + {\color{#00aaff}2}{\color{grey}e_2\otimes\epsilon^1} {\color{#ffff99}\ -\ 1}{\color{grey}e_2\otimes\epsilon^2}\right) \cdot \left({\color{#ff33ff}7}{\color{grey}e_1} + {\color{#ff9900}6}{\color{grey}e_2}\right) \\[2mm]
&= \left({\color{#ff00aa}1}{\color{grey}e_1\otimes\epsilon^1} + {\color{#66ffaa}0}{\color{grey}e_1\otimes\epsilon^2} + {\color{#00aaff}2}{\color{grey}e_2\otimes\epsilon^1} {\color{#ffff99}\ -\ 1}{\color{grey}e_2\otimes\epsilon^2}\right) \cdot {\color{#ff33ff}7}\color{grey}e_1 \\
&+ \left({\color{#ff00aa}1}{\color{grey}e_1\otimes\epsilon^1} + {\color{#66ffaa}0}{\color{grey}e_1\otimes\epsilon^2} + {\color{#00aaff}2}{\color{grey}e_2\otimes\epsilon^1} {\color{#ffff99}\ -\ 1}{\color{grey}e_2\otimes\epsilon^2}\right) \cdot {\color{#ff9900}6}\color{grey}e_2 \\[2mm]
&= {\color{#ff00aa}1}{\color{grey}e_1\otimes\epsilon^1} \cdot {\color{#ff33ff}7}{\color{grey}e_1} + {\color{#66ffaa}0}{\color{grey}e_1\otimes\epsilon^2} \cdot {\color{#ff33ff}7}{\color{grey}e_1} + {\color{#00aaff}2}{\color{grey}e_2\otimes\epsilon^1} \cdot {\color{#ff33ff}7}{\color{grey}e_1} {\color{#ffff99}\ -\ 1}{\color{grey}e_2\otimes\epsilon^2} \cdot {\color{#ff33ff}7}{\color{grey}e_1} \\
&+ {\color{#ff00aa}1}{\color{grey}e_1\otimes\epsilon^1} \cdot {\color{#ff9900}6}{\color{grey}e_2} + {\color{#66ffaa}0}{\color{grey}e_1\otimes\epsilon^2} \cdot {\color{#ff9900}6}{\color{grey}e_2} + {\color{#00aaff}2}{\color{grey}e_2\otimes\epsilon^1} \cdot {\color{#ff9900}6}{\color{grey}e_2} {\color{#ffff99}\ -\ 1}{\color{grey}e_2\otimes\epsilon^2} \cdot {\color{#ff9900}6}{\color{grey}e_2}\\[2mm]
&= {\color{#ff00aa}1}\cdot {\color{#ff33ff}7} {\color{darkgrey}e_1\otimes\epsilon^1e_1} + {\color{#66ffaa}0}\cdot {\color{#ff33ff}7} {\color{#333333}e_1\otimes\epsilon^2e_1} + {\color{#00aaff}2}\cdot {\color{#ff33ff}7} {\color{darkgrey}e_2\otimes\epsilon^1e_1} {\color{#ffff99}\ -\ 1}\cdot {\color{#ff33ff}7} {\color{#333333}e_2\otimes\epsilon^2e_1} \\
&+ {\color{#ff00aa}1}\cdot {\color{#ff9900}6} {\color{#333333}e_1\otimes\epsilon^1e_2} + {\color{#66ffaa}0}\cdot {\color{#ff9900}6} {\color{darkgrey}e_1\otimes\epsilon^2e_2} + {\color{#00aaff}2}\cdot {\color{#ff9900}6} {\color{#333333}e_2\otimes\epsilon^1e_2} {\color{#ffff99}\ -\ 1}\cdot {\color{#ff9900}6} {\color{darkgrey}e_2\otimes\epsilon^2e_2}\\[2mm]
&= {\color{#ff00aa}1}\cdot {\color{#ff33ff}7} {\color{grey}e_1} + {\color{#00aaff}2}\cdot {\color{#ff33ff}7} {\color{grey}e_2} + {\color{#66ffaa}0}\cdot {\color{#ff9900}6} {\color{grey}e_1} {\color{#ffff99}\ -\ 1}\cdot {\color{#ff9900}6} {\color{grey}e_2}\\[2mm]
&= ({\color{#ff00aa}1}\cdot {\color{#ff33ff}7} + {\color{#ff9900}6} \cdot {\color{#66ffaa}0}) {\color{grey}e_1} + ({\color{#00aaff}2}\cdot {\color{#ff33ff}7} {\color{#ffff99}\ -\ 1}\cdot {\color{#ff9900}6}) {\color{grey}e_2}\\[2mm]
&= 7 {\color{grey}e_1} + 8 {\color{grey}e_2}
\end{align*}$$


---
layout: two-cols-header
---

# Basis-notatie: Matrix-matrix

::left::

$$\begin{align*}\mathbf M &= {\color{#ff00aa} 1}{\color{grey}e_1\otimes\epsilon^1} \\&+ {\color{#66ffaa}0}{\color{grey}e_1\otimes\epsilon^2} \\&+ {\color{#00aaff}2}{\color{grey}e_2\otimes\epsilon^1} \\&{\color{#ffff99}\ -\ 1} {\color{grey}e_2\otimes\epsilon^2}\end{align*}$$
$$\begin{align*}\mathbf N &= {\color{#ff33ff} 3}{\color{grey}e_1\otimes\epsilon^1} \\&+ {\color{#cc99dd}4}{\color{grey}e_1\otimes\epsilon^2} \\&+ {\color{#ff9900}5}{\color{grey}e_2\otimes\epsilon^1} \\&+ {\color{#33ffff}0} {\color{grey}e_2\otimes\epsilon^2}\end{align*}$$

$$\epsilon^i e_j = \begin{cases} 1 \text{ if }  i = j \\ 0 \text{ if } i\ne j \end{cases}$$

::right::

<div style="font-size:0.95rem">

$$\begin{align*}\mathbf M \mathbf N &= \left({\color{#ff00aa}1}{\color{grey}e_1\otimes\epsilon^1} + {\color{#66ffaa}0}{\color{grey}e_1\otimes\epsilon^2} + {\color{#00aaff}2}{\color{grey}e_2\otimes\epsilon^1} {\color{#ffff99}\ -\ 1}{\color{grey}e_2\otimes\epsilon^2}\right) \cdot \left( {\color{#ff33ff} 3}{\color{grey}e_1\otimes\epsilon^1} + {\color{#cc99dd}4}{\color{grey}e_1\otimes\epsilon^2} + {\color{#ff9900}5}{\color{grey}e_2\otimes\epsilon^1} + {\color{#33ffff}0} {\color{grey}e_2\otimes\epsilon^2}\right) \\[2mm]

&= {\color{#ff00aa}1}{\color{grey}e_1\otimes\epsilon^1} \cdot {\color{#ff33ff}3}{\color{grey}e_1\otimes\epsilon^1} + {\color{#66ffaa}0}{\color{grey}e_1\otimes\epsilon^2} \cdot {\color{#ff33ff}3}{\color{grey}e_1\otimes\epsilon^1} + {\color{#00aaff}2}{\color{grey}e_2\otimes\epsilon^1} \cdot {\color{#ff33ff}3}{\color{grey}e_1\otimes\epsilon^1} {\color{#ffff99}\ -\ 1}{\color{grey}e_2\otimes\epsilon^2} \cdot {\color{#ff33ff}3}{\color{grey}e_1\otimes\epsilon^1} \\
&+ {\color{#ff00aa}1}{\color{grey}e_1\otimes\epsilon^1} \cdot {\color{#ff9900}5}{\color{grey}e_2\otimes\epsilon^1} + {\color{#66ffaa}0}{\color{grey}e_1\otimes\epsilon^2} \cdot {\color{#ff9900}5}{\color{grey}e_2\otimes\epsilon^1} + {\color{#00aaff}2}{\color{grey}e_2\otimes\epsilon^1} \cdot {\color{#ff9900}5}{\color{grey}e_2\otimes\epsilon^1} {\color{#ffff99}\ -\ 1}{\color{grey}e_2\otimes\epsilon^2} \cdot {\color{#ff9900}5}{\color{grey}e_2\otimes\epsilon^1}\\
&+ {\color{#ff00aa}1}{\color{grey}e_1\otimes\epsilon^1} \cdot {\color{#cc99dd}4}{\color{grey}e_1\otimes\epsilon^2} + {\color{#66ffaa}0}{\color{grey}e_1\otimes\epsilon^2} \cdot {\color{#cc99dd}4}{\color{grey}e_1\otimes\epsilon^2} + {\color{#00aaff}2}{\color{grey}e_2\otimes\epsilon^1} \cdot {\color{#cc99dd}4}{\color{grey}e_1\otimes\epsilon^2} {\color{#ffff99}\ -\ 1}{\color{grey}e_2\otimes\epsilon^2} \cdot {\color{#cc99dd}4}{\color{grey}e_1\otimes\epsilon^2}\\
&+ {\color{#ff00aa}1}{\color{grey}e_1\otimes\epsilon^1} \cdot {\color{#33ffff}0}{\color{grey}e_2\otimes\epsilon^2} + {\color{#66ffaa}0}{\color{grey}e_1\otimes\epsilon^2} \cdot {\color{#33ffff}0}{\color{grey}e_2\otimes\epsilon^2} + {\color{#00aaff}2}{\color{grey}e_2\otimes\epsilon^1} \cdot {\color{#33ffff}0}{\color{grey}e_2\otimes\epsilon^2} {\color{#ffff99}\ -\ 1}{\color{grey}e_2\otimes\epsilon^2} \cdot {\color{#33ffff}0}{\color{grey}e_2\otimes\epsilon^2}\\[2mm]

&= {\color{#ff00aa}1}\cdot {\color{#ff33ff}3}{\color{darkgrey}e_1\otimes\epsilon^1e_1\otimes\epsilon^1} + {\color{#66ffaa}0}\cdot {\color{#ff33ff}3}{\color{#333333}e_1\otimes\epsilon^2e_1\otimes\epsilon^1} + {\color{#00aaff}2}\cdot {\color{#ff33ff}3}{\color{darkgrey}e_2\otimes\epsilon^1e_1\otimes\epsilon^1} {\color{#ffff99}\ -\ 1}\cdot {\color{#ff33ff}3}{\color{#333333}e_2\otimes\epsilon^2e_1\otimes\epsilon^1} \\
&+ {\color{#ff00aa}1}\cdot {\color{#ff9900}5}{\color{#333333}e_1\otimes\epsilon^1e_2\otimes\epsilon^1} + {\color{#66ffaa}0}\cdot {\color{#ff9900}5}{\color{darkgrey}e_1\otimes\epsilon^2e_2\otimes\epsilon^1} + {\color{#00aaff}2}\cdot {\color{#ff9900}5}{\color{#333333}e_2\otimes\epsilon^1e_2\otimes\epsilon^1} {\color{#ffff99}\ -\ 1}\cdot {\color{#ff9900}5}{\color{darkgrey}e_2\otimes\epsilon^2e_2\otimes\epsilon^1}\\
&+ {\color{#ff00aa}1}\cdot {\color{#cc99dd}4}{\color{darkgrey}e_1\otimes\epsilon^1e_1\otimes\epsilon^2} + {\color{#66ffaa}0}\cdot {\color{#cc99dd}4}{\color{#333333}e_1\otimes\epsilon^2e_1\otimes\epsilon^2} + {\color{#00aaff}2}\cdot {\color{#cc99dd}4}{\color{darkgrey}e_2\otimes\epsilon^1e_1\otimes\epsilon^2} {\color{#ffff99}\ -\ 1}\cdot {\color{#cc99dd}4}{\color{#333333}e_2\otimes\epsilon^2e_1\otimes\epsilon^2}\\
&+ {\color{#ff00aa}1}\cdot {\color{#33ffff}0}{\color{#333333}e_1\otimes\epsilon^1e_2\otimes\epsilon^2} + {\color{#66ffaa}0}\cdot {\color{#33ffff}0}{\color{darkgrey}e_1\otimes\epsilon^2e_2\otimes\epsilon^2} + {\color{#00aaff}2}\cdot {\color{#33ffff}0}{\color{#333333}e_2\otimes\epsilon^1e_2\otimes\epsilon^2} {\color{#ffff99}\ -\ 1}\cdot {\color{#33ffff}0}{\color{darkgrey}e_2\otimes\epsilon^2e_2\otimes\epsilon^2}\\[2mm]

&= {\color{#ff00aa}1}\cdot {\color{#ff33ff}3}{\color{grey}e_1\otimes\epsilon^1} + {\color{#00aaff}2}\cdot {\color{#ff33ff}3}{\color{grey}e_2\otimes\epsilon^1}
+ {\color{#66ffaa}0}\cdot {\color{#ff9900}5}{\color{grey}e_1\otimes\epsilon^1} +  {\color{#ffff99}\ -\ 1}\cdot {\color{#ff9900}5}{\color{grey}e_2\otimes\epsilon^1}\\
&+ {\color{#ff00aa}1}\cdot {\color{#cc99dd}4}{\color{grey}e_1\otimes\epsilon^2} + {\color{#00aaff}2}\cdot {\color{#cc99dd}4}{\color{grey}e_2\otimes\epsilon^2}
+ {\color{#66ffaa}0}\cdot {\color{#33ffff}0}{\color{grey}e_1\otimes\epsilon^2} + {\color{#ffff99}\ -\ 1}\cdot {\color{#33ffff}0}{\color{grey}e_2\otimes\epsilon^2}\\[2mm]

&= 3 {\color{grey}e_1\otimes\epsilon^1} + 1{\color{grey}e_2\otimes\epsilon^1}
+ 4{\color{grey}e_1\otimes\epsilon^2} + 8{\color{grey}e_2\otimes\epsilon^2}

\end{align*}$$
</div>

---
layout: image
image: wtf.jpg
---

---
layout: two-cols-header
---

# Basis-notatie: Matrix-matrix (redux)

We kunnen de berekening opschonen door alvast vooruit te kijken, en alle termen die later weg vallen niet over te nemen:

<div style="font-size:0.95rem">

$$\begin{align*}
\mathbf M &= {\color{#ff00aa} 1}{\color{grey}e_1\otimes\epsilon^1} + {\color{#66ffaa}0}{\color{grey}e_1\otimes\epsilon^2} + {\color{#00aaff}2}{\color{grey}e_2\otimes\epsilon^1} {\color{#ffff99}\ -\ 1} {\color{grey}e_2\otimes\epsilon^2},\qquad
\mathbf N = {\color{#ff33ff} 3}{\color{grey}e_1\otimes\epsilon^1} + {\color{#cc99dd}4}{\color{grey}e_1\otimes\epsilon^2} + {\color{#ff9900}5}{\color{grey}e_2\otimes\epsilon^1} + {\color{#33ffff}0} {\color{grey}e_2\otimes\epsilon^2}\\[5mm]
\mathbf M \mathbf N &= \left({\color{#ff00aa}1}{\color{grey}e_1\otimes\epsilon^1} + {\color{#66ffaa}0}{\color{grey}e_1\otimes\epsilon^2} + {\color{#00aaff}2}{\color{grey}e_2\otimes\epsilon^1} {\color{#ffff99}\ -\ 1}{\color{grey}e_2\otimes\epsilon^2}\right) \cdot \left( {\color{#ff33ff} 3}{\color{grey}e_1\otimes\epsilon^1} + {\color{#cc99dd}4}{\color{grey}e_1\otimes\epsilon^2} + {\color{#ff9900}5}{\color{grey}e_2\otimes\epsilon^1} + {\color{#33ffff}0} {\color{grey}e_2\otimes\epsilon^2}\right) \\[2mm]

&= {\color{#ff00aa}1}{\color{grey}e_1\otimes\epsilon^1} \cdot {\color{#ff33ff}3}{\color{grey}e_1\otimes\epsilon^1} + {\color{#00aaff}2}{\color{grey}e_2\otimes\epsilon^1} \cdot {\color{#ff33ff}3}{\color{grey}e_1\otimes\epsilon^1}
+ {\color{#66ffaa}0}{\color{grey}e_1\otimes\epsilon^2} \cdot {\color{#ff9900}5}{\color{grey}e_2\otimes\epsilon^1} {\color{#ffff99}\ -\ 1}{\color{grey}e_2\otimes\epsilon^2} \cdot {\color{#ff9900}5}{\color{grey}e_2\otimes\epsilon^1}\\
&+ {\color{#ff00aa}1}{\color{grey}e_1\otimes\epsilon^1} \cdot {\color{#cc99dd}4}{\color{grey}e_1\otimes\epsilon^2} + {\color{#00aaff}2}{\color{grey}e_2\otimes\epsilon^1} \cdot {\color{#cc99dd}4}{\color{grey}e_1\otimes\epsilon^2} 
+ {\color{#66ffaa}0}{\color{grey}e_1\otimes\epsilon^2} \cdot {\color{#33ffff}0}{\color{grey}e_2\otimes\epsilon^2} {\color{#ffff99}\ -\ 1}{\color{grey}e_2\otimes\epsilon^2} \cdot {\color{#33ffff}0}{\color{grey}e_2\otimes\epsilon^2}\\[2mm]


&= {\color{#ff00aa}1}\cdot {\color{#ff33ff}3}{\color{grey}e_1\otimes\epsilon^1} + {\color{#00aaff}2}\cdot {\color{#ff33ff}3}{\color{grey}e_2\otimes\epsilon^1}
+ {\color{#66ffaa}0}\cdot {\color{#ff9900}5}{\color{grey}e_1\otimes\epsilon^1} +  {\color{#ffff99}\ -\ 1}\cdot {\color{#ff9900}5}{\color{grey}e_2\otimes\epsilon^1}\\
&+ {\color{#ff00aa}1}\cdot {\color{#cc99dd}4}{\color{grey}e_1\otimes\epsilon^2} + {\color{#00aaff}2}\cdot {\color{#cc99dd}4}{\color{grey}e_2\otimes\epsilon^2}
+ {\color{#66ffaa}0}\cdot {\color{#33ffff}0}{\color{grey}e_1\otimes\epsilon^2} + {\color{#ffff99}\ -\ 1}\cdot {\color{#33ffff}0}{\color{grey}e_2\otimes\epsilon^2}\\[2mm]

&= 3 {\color{grey}e_1\otimes\epsilon^1} + 1{\color{grey}e_2\otimes\epsilon^1}
+ 4{\color{grey}e_1\otimes\epsilon^2} + 8{\color{grey}e_2\otimes\epsilon^2}

\end{align*}$$

$$\epsilon^i e_j = \begin{cases} 1 \text{ if }  i = j \\ 0 \text{ if } i\ne j \end{cases}$$

</div>

---

# Sommatie en Einstein Notatie

Als we de getallen in de vector / matrix indexeren, kunnen we het systematisch over individuele getallen hebben.

- $v^3$ staat voor het derde element van $\ket v$ 
$$\ket v = v^1{\color{grey}e_1} + v^2{\color{grey}e_2}$$
- $M^1_2$ staat voor het eerste element van de tweede kolom van $\mathbf M$
$$\mathbf M = M^1_1{\color{grey}e_1\otimes\epsilon^1} + M^1_2{\color{grey}e_1\otimes\epsilon^2} + M^2_1{\color{grey}e_2\otimes\epsilon^1} + M^2_2 {\color{grey}e_2\otimes\epsilon^2}$$
*Merk op dat een hoge index in de elementen overeen komt met een lage in de basis-vector, en vice versa!*
(FIXME: dit is conventie en klopt qua (co) variantie, maar is misschien simpeler om juist te matchen?)

De berekeningen voor de elementen van $\ket w = \mathbf M \ket v$ en $\mathbf O = \mathbf{MN}$ zien er nu als volgt uit:
$$w^i = \sum_{j = 1}^n M^i_j v^j = M^i_{\color{#00aaff}j} v^{\color{#00aaff}j}, \qquad O^i_k = \sum_{j = 1}^n M^i_j N^j_k = M^i_{\color{#00aaff}j} N^{\color{#00aaff}j}_k$$

Vaak laten we de $\Sigma$ en sommatie index $j$ weg, omdat die eigenlijk al duidelijk is: het is de enige index die twee keer voor komt, boven en beneden.

---

# Matrices als bilineaire vormen

We gaan nu een matrix gebruiken om 2 vectoren te combineren, met als resultaat een getal. Dit lijkt op het eerste gezicht vreemd, maar als we met transpositie een van beide vectoren tot een rij maken kan dat prima:

$$\bra u : \mathbb R^{1 \times 2} = \begin{bmatrix}1 & 2\end{bmatrix} \qquad
\ket v : \mathbb R^{2 \times 1} = \begin{bmatrix}3 \\ -1\end{bmatrix} \qquad
\mathbf B : \mathbb R^{2 \times 2} = \begin{bmatrix} 0 & 1 \\ -1 & 0 \end{bmatrix}$$

&nbsp;

$$\begin{CD}
\bra u\ :\ \mathbb R^{1 \times 2} @. @. \ket v\ :\ \mathbb R^{2 \times 1} \\

@V{\cdot \mathbf B}VV @. @V{\mathbf B\cdot }VV\\

\langle u \mid \mathbf B\ :\ \mathbb R^{1 \times 2}
@>{\cdot \ket v}>>
\langle u \mid \mathbf B \mid v \rangle\ :\ \mathbb R
@<{\bra u\cdot }<<
\mathbf B \mid v \rangle\ :\ \mathbb R^{2 \times 1}
\end{CD}$$

**Oefening:** voer de berekeningen uit. Maakt het uit welk pad je kiest?


---

# Bilineaire vormen (bilinear forms)

Eigenlijk hebben we hier een truc gedaan: als we een functie willen van 2 vectoren naar een getal, dan is dit geen matrix (rij van kolommen) maar een rij van rijen:

$$\mathbf B = \begin{bmatrix} \begin{bmatrix}0 & 1\end{bmatrix} & \begin{bmatrix}-1 & 0\end{bmatrix} \end{bmatrix} = 1\textcolor{grey}{\epsilon^2\otimes\epsilon^1} -1\textcolor{grey}{\epsilon^1\otimes\epsilon^2}$$

Dit is een lineaire functies van twee vectoren naar een getal. We kunnen de vorm $\mathbf{B}$ twee (kolom-)vectoren geven:

$$\ket u = 1\textcolor{grey}{e_1} + 2\textcolor{grey}{e_2} \qquad
\ket v = 3\textcolor{grey}{e_1} -1\textcolor{grey}{e_2}$$

$$\begin{align*}B(u,v) = \mathbf B \ket u \ket v &= \left(1\textcolor{grey}{\epsilon^2\otimes\epsilon^1} -1\textcolor{grey}{\epsilon^1\otimes\epsilon^2}\right)\left(1\textcolor{grey}{e_1}+2\textcolor{grey}{e_2}\right)\left(3\textcolor{grey}{e_1} - 1\textcolor{grey}{e_2}\right)\\
&= \left(1\textcolor{grey}{\epsilon^2\otimes\epsilon^1e_1} \textcolor{#333333}{+ 2\epsilon^2\otimes\epsilon^1e_2-1\epsilon^1\otimes\epsilon^2e_1} - 2\textcolor{grey}{\epsilon^1\otimes\epsilon^2e_2}\right)\left(3\textcolor{grey}{e_1} - \textcolor{grey}{e_2}\right)\\
&= \left(1\textcolor{grey}{\epsilon^2} - 2\textcolor{grey}{\epsilon^1}\right)\left(3\textcolor{grey}{e_1} - 1\textcolor{grey}{e_2}\right)\\
&= \textcolor{#333333}{3\epsilon^2e_1} - 1\textcolor{grey}{\epsilon^2e_2} - 6\textcolor{grey}{\epsilon^1e_1} \textcolor{#333333}{+ 2\epsilon^1e_2}\\
&= -7
\end{align*}$$

---

# Tensoren

- Vectoren, covectoren, matrices, bilineaire vormen lijken erg op elkaar.
    - Het zijn verschijningsvormen van een algemeen concept: de **tensor**.
    - Tensoren hebben een aantal dimensies, opgebouwd uit vector en covector basis:

|Object||Vector-bases|Covector-bases|Basis|Voorbeeld index|
|---|---|---|---|---|---|
|Vector|*(1,0)-tensor*|1|0|$e_1, e_2, \dots$|$v^i e_1$
|Covector|*(0,1)-tensor*|0|1|$\epsilon^1, \epsilon^2, \dots$|$c_i \epsilon^i$
|Matrix|*(1,1)-tensor*|1|1|$e_1\epsilon^1, e_1\epsilon^2, e_2\epsilon^1, \dots$|$M_j^ie_i\epsilon^j$
|Bilineaire vorm|*(0,2)-tensor*|0|2|$\epsilon^1\epsilon^1, \epsilon^1\epsilon^2, \epsilon^2\epsilon^1, \dots$|$B_{ij}\epsilon^i\epsilon^j$

*Met deze bouwstenen kunnen we arbitraire multi-lineaire functies bouwen, bijvoorbeeld van twee vectoren naar een nieuwe vector. Als we later vectoren gaan gebruiken voor de betekenis van woorden en zinnen, kan dit bijvoorbeeld een werkwoord zijn dat een onderwerp en leidend voorwerp nodig heeft.*

---

# Tensor / Kronecker Product

- Hogere-orde tensoren worden gevormd op basis van coefficienten en basis-tensoren.
- Soms willen we een hogere-orde tensor maken op basis van vectoren.
  - Dit kan met het Kronecker product, $\otimes$.

$$\begin{bmatrix}v^1 \\ v^2\end{bmatrix} \otimes \begin{bmatrix}\alpha_1 & \alpha_2\end{bmatrix} = \begin{bmatrix} \begin{bmatrix}v^1\alpha_1 \\ v^1\alpha_2\end{bmatrix} & \begin{bmatrix}v^2\alpha_1 \\ v^2\alpha_2\end{bmatrix} \end{bmatrix}$$

Hier maken we een matrix met behulp van een vector en een covector.

*Niet alle matrices zijn op deze manier te maken, e.g. $\begin{bmatrix}1 & 2 \\ 3 & 4\end{bmatrix}$ kan niet op deze manier worden opgebouwd.*

Vaak kom je de notatie notatie $\ket u \bra v$ tegen voor de vector-covector naar matrix vermenigvuldiging. Ook zonder het $\otimes$ symbool is het Kronecker product hier impliciet.

**Het symbool $\otimes$ wordt zowel voor het Kronecker product gebruikt (op lijsten en kolommen van getallen), als voor het tensor-product (dat wij vooral voor basis-vectoren gebruiken).**


---

# Index-notatie

Des te complexer tensoren worden, des te lastiger wordt het om deze te overzien.
- Hebben we te maken met een rij van kolommen van rijen? Of een rij van rijen van kolommen?
- Welke "assen" willen we verwisselen bij een transpositie?
- Op welke manier wordt een vermenigvuldiging uitgevoerd?

**In dit geval is het handiger om met index-notatie te werken, en de basis expliciet te benoemen.**

###  Voorbeeld

$T_{ij}^k\textcolor{grey}{e_k\otimes\epsilon^i\otimes\epsilon^j}$ staat voor *"[y] ziet [x]"*. We willen dit combineren met vectoren $m^a \textcolor{grey}{e_a}$ (*"man"*) en $h^b \textcolor{grey}{e_b}$ (*"hond"*).

- Voor *"(De) man ziet (de) hond"* zetten we de index van *"hond"* gelijk aan de eerste index van *"zien"*, en die van *"man"* aan de tweede: 
$$S = \mathbf T \ket h \ket m = T_{ij}^kh_im_j = T_{ij}^km_jh_i \mapsto S^k e_k$$
- Voor *"(De) hond ziet (de) man"* zetten we de index van *"man"* gelijk aan de eerste index van *"zien"*, en die van *"hond"* aan de tweede: 
$$S = \mathbf T \ket m \ket h = T_{ij}^km_ih_j = T_{ij}^kh_jm_i \mapsto S^k e_k$$

---
layout: image-right
image: python.jpg
---

# In Python

De meeste producten die we deze les gezien hebben, zitten in Numpy als `dot()` of `@`.
- Python houdt geen informatie bij over het vector-vs-covector aspect van elementen.
- Het kan dus zijn dat je bij een matrix product een "verkeerd" antwoord krijgt.
  - In dit geval mis je meestal een transpositie om rijen/kolommen te verwisselen.
- Dit probleem is gelukkig minder aanwezig bij niet-vierkante matrices, omdat deze op minder manieren op elkaar passen
  - Een niet passende operatie leidt tot een error
  - Vectoren (mits opgeslagen als $n$-D arrays en niet $n\times 1$ of $1 \times n$) worden vanzelf in de juiste vorm gezet voor een geldig product*.

**Volgende les gaan we toewerken naar toepassing in neurale netwerken, en gebruik van Numpy in deze context.**

---

# Portfolio-item LA-I

---
layout: chaptertitle
---

# [LA-4] Lineaire Algebra voor (deep) learning

---

# Koppeling NN

---

# Affine transformaties / Homogene Coordinaten

tbv bias term

---
layout: chaptertitle
---

# [LA-5] Dimensionaliteits-reductie met PCA

---

# Dimensionaliteits-reductie

- Wat willen we bereiken?
- Terugblik colour space les 1

---

# Coordinaatstelsels en basis-vectoren

---

# Covariantie-matrix

---

# Eigenvectoren

---

# Eigenbasis

---

# Symmetrische Matrices

- Geometrische vorm
- Eigenstuff orthonormaal
- Quadratic forms?

---

# Lagrange

---

# Principal Component Analysis

---

# Factor Analysis

---
layout: chaptertitle
---

# [LA-6] Data-embedding

---

# Nadelen PCA

---

# T-SNE

- Wat doet het?

---

# T-SNE

High leven overview stappen

---

# Gelijkenissen in hogere dimensies

---

# Gelijkenissen in lagere dimensies

---

# Student's T-distribution

---

# Verplaatsen van datapunten

---

# Voorbeelden data

- Eerste intro images / word embeddings?

---

# Portfolio-item LA-II

---
layout: chaptertitle
---

# [LA-7] Calculus met Vectoren en Matrices

---

# Terugblik S3

https://github.com/AI-S3-2025/S3_AI_lesmateriaal/blob/main/WiskundigeTechnieken/wiskunde_les3.ipynb
https://github.com/AI-S3-2025/S3_AI_lesmateriaal/blob/main/WiskundigeTechnieken/wiskunde_les4.ipynb

---

# Afgeleide van een getal-wise functie -> sigmoid?

tbv NN

---

# Afgeleide van een functie met 2 args

- Partieel
- Gradient

---

# Afgeleides van matrix-producten / tensoren etc

---

# Gradient Descent

- Simpele 2D functie (2D Gauss?) maar in termen van matrix/vector

---

# Matrices en grafen?

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
