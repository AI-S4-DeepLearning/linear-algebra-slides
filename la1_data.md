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

hebben we de projectie $\text{proj}_p(v)$ van $\ket v$ op $\ket p$ berekend met
$$\frac{\langle p \mid v \rangle}{\langle p \mid p \rangle}\ket{p} = 2  \begin{bmatrix}2 \\ 1 \end{bmatrix} = \begin{bmatrix}4 \\ 2 \end{bmatrix}$$

Hiermee kunnen we de vector $\ket v$ in twee&euml;n splitsen:
- Het deel parallel aan $\ket p$, i.e. ${\color{magenta}\ket v_{\parallel p}} = \text{proj}_{\color{#0099ff}p}({\color{red}v})$
- Het deel haaks op $\ket p$, i.e. ${\color{orange}\ket v_{\perp p}} = \ket v - {\color{magenta}\ket v_{\parallel p}}$

---
layout: chaptertitle
---

# [LA-3] Matrices en Tensoren

---
layout: image-right
image: conformal.gif
---

# Transformaties

Functies werken op indivivuele vectoren, maar ook op hele ruimtes.

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

# Demo

 <iframe src="lin_trans.html" width="100%" height="90%"></iframe> 

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

## Calculatie
Om twee matrices te vermenigvuldigen, beschouwen we een matrix als een kolom van rijen, en een als een rij van kolommen:

$$\mathbf M = \begin{bmatrix}1 & 0 \\ 2 & -1\end{bmatrix} \qquad\mathbf N = \begin{bmatrix}3 & 4 \\ 5 & 0\end{bmatrix}$$
$$\Downarrow$$
$$\mathbf M = \begin{bmatrix}\begin{bmatrix}1 & 0 \end{bmatrix} \\[2mm] \begin{bmatrix}2 & -1 \end{bmatrix}\end{bmatrix} \qquad \mathbf N = \begin{bmatrix}\begin{bmatrix}3 \\ 5\end{bmatrix} & \begin{bmatrix} 4 \\ 0 \end{bmatrix} \end{bmatrix}
\\[5mm]

---

# Matrix-matrix multiplicatie

Om deze berekening uit te voeren gaan we een kolom-rij vermenigvuldiging uitvoeren - **dit is iets anders dan de rij-kolom vermenigvuldiging van het inwendig product!**

*Bij een kolom-rij product zetten we systematisch alle combinaties van elementen in een matrix:*

$$\begin{align*}\mathbf M \mathbf N &=
\begin{bmatrix}\begin{bmatrix}1 & 0 \end{bmatrix} \\[2mm] \begin{bmatrix}2 & -1 \end{bmatrix}\end{bmatrix}
\begin{bmatrix}\begin{bmatrix}3 \\ 5\end{bmatrix} & \begin{bmatrix} 4 \\ 0 \end{bmatrix} \end{bmatrix}
\\[5mm]
&= \begin{bmatrix}
\color{pink} \begin{bmatrix}1 & 0\end{bmatrix}  \begin{bmatrix}3 \\ 5 \end{bmatrix} &
\color{lightgreen} \begin{bmatrix} 2 & -1\end{bmatrix}  \begin{bmatrix}3 \\ 5 \end{bmatrix} \\[3mm]
\color{lightblue} \begin{bmatrix}1 & 0\end{bmatrix}  \begin{bmatrix}4 \\ 0 \end{bmatrix} &
\color{lightyellow}\begin{bmatrix} 2 & -1\end{bmatrix}  \begin{bmatrix}4 \\ 0 \end{bmatrix}
\end{bmatrix} \\[8mm]
&= \begin{bmatrix}\color{pink} 1 \cdot 3 + 0 \cdot 5 & \color{lightgreen} 2 \cdot 3  - 1 \cdot 5 \\ \color{lightblue} 1 \cdot 4 + 0 \cdot 0 & \color{lightyellow} 2 \cdot 4 -1 \cdot 0 \end{bmatrix} \\[5mm]
&= \begin{bmatrix}\color{pink} 3 & \color{lightgreen} 1 \\ \color{lightblue} 4 & \color{lightyellow} 8 \end{bmatrix} \\[5mm]
\end{align*}$$

---

# Op basis van index

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

# Systemen van vergelijkingen
- Ook te lezen als een systeem van drie vergelijkingen met 3 onbekenden:

$$1x + 2y + 3z$$
$$4x + 5y + 6z$$
$$7x + 8y + 9z$$

---

# Determinant

---

# Gauss-Jordan Eliminatie

---

# Transpositie

---

# Functies als data, data als functie

Rij/kolom elementen
- Mogelijk row/column/null?

---

# Covectoren

plots

---

# 2-forms

Lineaire functies van 2 vectoren naar een getal

---

# Currying

---

# Tensoren

- Generalisatie op matrices, 2-forms -> 3D arrays

Bijv: lineaire functie van 2 vectoren naar 1 vector

---

# Tensor Product

ketbra

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

## Calculus


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

# [LA-7] Denouement

---

# Overige onderwerpen
- Dit is na de toetsing, voor nu reserveren voor flow-over?

---

# Matrices en grafen

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
