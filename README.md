# Desenvolupa una aplicació web per repartir un compte de restaurant

Actua com un desenvolupador front-end sènior especialitzat en HTML, CSS i JavaScript, amb criteri de UX/UI.

Vull que desenvolupis una aplicació web senzilla per calcular quant ha de pagar cada persona quan diverses persones comparteixen un àpat i tenen un únic tiquet amb un import total.

L'aplicació s'ha de dir provisionalment **"Compte Fàcil"**.

## 1. REQUISIT TÈCNIC PRINCIPAL

L'aplicació ha de ser un **únic fitxer HTML autocontingut**.

Tot ha d'estar dins del mateix fitxer:

* HTML
* CSS
* JavaScript

No utilitzis frameworks ni llibreries externes.

No utilitzis React, Vue, Angular, Bootstrap, Tailwind ni cap altra dependència.

L'HTML ha de funcionar obrint-lo directament en un navegador, sense servidor, compilació ni instal·lació.

No ha de requerir connexió a Internet.

No hi ha d'haver backend ni base de dades.

Tots els càlculs s'han de fer localment amb JavaScript.

## 2. OBJECTIU DE L'APLICACIÓ

L'usuari té un únic tiquet de restaurant i vol repartir-ne el cost entre diverses persones.

L'aplicació tindrà només **dos modes**:

1. **RÀPID**
2. **GRUPS**

No afegeixis altres modes o funcionalitats que no s'especifiquen aquí.

---

# 3. MODE RÀPID

El mode ràpid serveix per dividir un compte a parts iguals.

## Inputs

### Total del tiquet

Camp numèric:

> Total del tiquet

Exemple:

> 127,50 €

### Nombre de persones

Camp numèric:

> Nombre de persones

Exemple:

> 5

Utilitza controls `-` i `+` per facilitar l'increment i decrement del nombre de persones.

## Càlcul

Fes:

`total / nombre de persones`

Exemple:

127,50 € / 5 = 25,50 €

## Resultat

Mostra una targeta de resultat destacada:

**25,50 €**

> per persona

I mostra també:

> 127,50 € ÷ 5 persones

Al final mostra:

> Total repartit: 127,50 €

El resultat s'ha d'actualitzar automàticament quan l'usuari modifica les dades.

No és necessari obligar l'usuari a prémer un botó "Calcular".

---

# 4. MODE GRUPS

El mode Grups serveix per repartir el compte entre diferents grups de persones.

Un grup pot representar:

* una persona
* una parella
* una família
* un grup d'amics
* qualsevol combinació d'adults i nens

Per tant, no creïs una funcionalitat específica anomenada "Parelles".

Una parella és simplement un grup amb 2 adults.

## Input principal

### Total del tiquet

Camp:

> Total del tiquet

Exemple:

> 180,00 €

---

# 5. CREACIÓ DE GRUPS

L'usuari ha de poder prémer:

**+ AFEGIR GRUP**

Cada grup ha de tenir:

### Nom del grup

Camp de text.

Exemples:

* Esteve
* Joan + Maria
* Família Pérez
* Marc + Anna + Pol

### Adults

Control numèric amb:

`-   2   +`

Valor mínim: 0.

### Nens

Control numèric amb:

`-   1   +`

Valor mínim: 0.

El nombre total d'adults i nens d'un grup no pot ser 0.

---

# 6. COEFICIENT DELS NENS

Cada adult té sempre un coeficient de:

**1,0**

Cada nen té per defecte:

**0,5**

Aquest valor ha de ser configurable a nivell global del mode Grups.

Per exemple:

> Coeficient del nen: 0,5

L'usuari ha de poder modificar-lo.

Opcions ràpides:

* 0,25
* 0,5
* 0,75
* Personalitzat

També ha de ser possible introduir manualment un valor decimal.

El coeficient dels adults no és configurable i sempre és 1,0.

---

# 7. LÒGICA DE CÀLCUL DEL MODE GRUPS

Per a cada grup calcula:

`unitats = adults × 1 + nens × coeficient_nen`

Exemple:

Família Pérez:

* 2 adults
* 2 nens
* coeficient nen = 0,5

Per tant:

`2 × 1 + 2 × 0,5 = 3 unitats`

---

## Valor d'una unitat

Calcula:

`total del tiquet / suma de totes les unitats`

Exemple:

Total:

180 €

Grups:

* Esteve: 1 adult = 1 unitat
* Joan + Maria: 2 adults = 2 unitats
* Família Pérez: 2 adults + 2 nens = 3 unitats
* Marc + Anna + Pol: 2 adults + 1 nen = 2,5 unitats

Total:

`1 + 2 + 3 + 2,5 = 8,5 unitats`

Valor d'una unitat:

`180 / 8,5 = 21,176470...`

---

# 8. IMPORT DE CADA GRUP

Calcula:

`unitats del grup × valor de la unitat`

Per exemple:

Esteve:

1 × 21,176470 = 21,176470 €

Joan + Maria:

2 × 21,176470 = 42,352941 €

Família Pérez:

3 × 21,176470 = 63,529411 €

Marc + Anna + Pol:

2,5 × 21,176470 = 52,941176 €

Els imports mostrats a l'usuari han d'estar arrodonits a dos decimals.

---

# 9. ARRODONIMENT

Aquesta part és molt important.

La suma dels imports mostrats sempre ha de coincidir exactament amb el total del tiquet.

Per exemple:

100 € dividits entre 3 persones no pot mostrar:

33,33 €
33,33 €
33,33 €

perquè sumarien 99,99 €.

Ha de mostrar:

33,33 €
33,33 €
33,34 €

La diferència d'arrodoniment s'ha d'assignar automàticament a un dels participants/grups perquè:

**SUMA DELS PAGAMENTS = TOTAL DEL TIQUET**

Implementa aquesta lògica de manera robusta tant en mode Ràpid com en mode Grups.

No mostris errors de cèntims causats per aritmètica de coma flotant de JavaScript.

---

# 10. RESULTAT DEL MODE GRUPS

La targeta principal de resultats ha de mostrar:

### Valor per adult / unitat

Per exemple:

**21,18 €**

> per unitat

Després mostra el repartiment:

### REPARTIMENT

**Esteve**

1 adult

**21,18 €**

---

**Joan + Maria**

2 adults

**42,35 €**

---

**Família Pérez**

2 adults + 2 nens

**63,53 €**

---

**Marc + Anna + Pol**

2 adults + 1 nen

**52,94 €**

---

Al final:

**TOTAL REPARTIT**

**180,00 €**

---

# 11. INFORMACIÓ DELS NENS

A cada grup, si hi ha nens, mostra clarament la composició.

Exemple:

> 2 adults · 2 nens

No cal mostrar permanentment la fórmula matemàtica.

L'usuari ha d'entendre simplement:

> Aquest grup té 2 adults i 2 nens i paga X €.

---

# 12. EDICIÓ DELS GRUPS

Cada grup ha de permetre:

* editar
* eliminar

Quan s'edita un grup, s'han de poder modificar:

* nom
* nombre d'adults
* nombre de nens

Els resultats s'han d'actualitzar automàticament.

---

# 13. ESTAT INICIAL

Quan s'obre l'aplicació:

El mode seleccionat per defecte ha de ser:

**RÀPID**

El total ha d'estar buit.

El nombre de persones pot començar en:

**2**

perquè és el cas més habitual, però l'usuari l'ha de poder modificar.

No hi ha d'haver cap resultat fins que existeixin dades vàlides.

---

# 14. VALIDACIÓ

Gestiona correctament aquests casos:

* total buit
* total igual a 0
* nombre de persones inferior a 1
* grup sense adults ni nens
* cap grup creat
* coeficient de nen inferior o igual a 0
* valors no numèrics

No permetis càlculs incorrectes.

Mostra missatges d'error curts i clars sota el camp corresponent.

---

# 15. BOTÓ PER COMENÇAR UN NOU COMPTE

Inclou un botó:

**↻ NOU COMPTE**

Quan l'usuari el prem, ha d'aparèixer una confirmació abans d'esborrar les dades.

Per exemple:

> Vols començar un compte nou? Esborraràs les dades actuals.

Botons:

**Cancel·lar**

**Nou compte**

---

# 16. DISSENY UX/UI

Vull una interfície moderna, neta i molt fàcil d'utilitzar.

Prioritza:

* simplicitat
* llegibilitat
* rapidesa
* jerarquia visual clara
* números grans
* formularis fàcils d'utilitzar
* botons tàctils grans
* bona experiència en mòbil

L'aplicació s'ha de veure bé tant en:

* smartphone
* tablet
* ordinador

Utilitza un disseny responsive.

No facis una interfície carregada.

No afegeixis animacions innecessàries.

---

# 17. ESTRUCTURA VISUAL

La pantalla principal hauria de tenir aquesta estructura:

### Capçalera

**COMPTE FÀCIL**

Text secundari:

> Divideix el compte fàcilment

### Selector de mode

`RÀPID | GRUPS`

El mode actiu ha d'estar clarament ressaltat.

### Contingut del mode seleccionat

Els camps corresponents.

### Resultat

Una targeta visualment destacada.

### Botó

**NOU COMPTE**

---

# 18. TARGETA DE RESULTAT

La resposta principal ha de destacar visualment.

Per exemple:

```text
┌──────────────────────────────┐
│       PER PERSONA            │
│                              │
│          25,50 €             │
│                              │
│     127,50 € ÷ 5             │
└──────────────────────────────┘
```

En mode Grups:

```text
┌──────────────────────────────┐
│       PER UNITAT             │
│                              │
│          21,18 €             │
│                              │
│        8,5 unitats           │
└──────────────────────────────┘
```

Després, la llista detallada dels grups.

---

# 19. FORMAT DELS IMPORTS

Tots els imports han de mostrar:

* dos decimals
* coma decimal
* símbol €

Exemples:

`25,50 €`

`100,00 €`

`7,25 €`

Internament pots utilitzar punts decimals de JavaScript, però la presentació a l'usuari ha de seguir el format habitual espanyol.

---

# 20. ACCESSIBILITAT

Utilitza:

* etiquetes HTML correctes
* `label` associats als inputs
* contrast suficient
* focus visible
* botons accessibles
* navegació amb teclat
* textos que no depenguin exclusivament del color

Els controls `+` i `-` han de tenir també `aria-label`.

---

# 21. ICONES

Si necessites icones, prefereixo utilitzar caràcters simples o SVG inline.

No carreguis llibreries externes d'icones.

---

# 22. NO AFEGIR FUNCIONALITATS

No implementis:

* propines
* IVA
* plats individuals
* pagaments parcials
* qui paga físicament
* comptes d'usuari
* login
* historial
* base de dades
* compartir per WhatsApp
* backend
* conversió de moneda
* altres modes de repartiment

Aquest projecte ha de centrar-se exclusivament en els dos modes definits:

**RÀPID**

i

**GRUPS**

---

# 23. PROVES QUE HAS DE VERIFICAR

Abans de donar-me el resultat final, comprova manualment la lògica amb aquests casos.

### Prova 1

100 €
4 persones

Resultat:

25 € per persona.

### Prova 2

127,50 €
5 persones

Resultat:

25,50 € per persona.

### Prova 3

180 €

Grups:

* 1 adult
* 2 adults
* 2 adults
* 3 adults

Total:

8 persones.

Resultat:

22,50 € per persona.

Els grups han de pagar:

22,50 €
45,00 €
45,00 €
67,50 €

### Prova 4

150 €

Grups:

* 4 adults
* 2 nens

Coeficient nen:

0,5

Total d'unitats:

5

Adult:

30 €

Nen:

15 €

### Prova 5

180 €

Grups:

* 1 adult
* 2 adults
* 2 adults + 2 nens
* 2 adults + 1 nen

Coeficient nen:

0,5

Total d'unitats:

8,5

Comprova especialment l'arrodoniment i que la suma final sigui exactament:

**180,00 €**

### Prova 6

100 €

3 persones.

Comprova que els resultats siguin:

33,33 €
33,33 €
33,34 €

i que la suma sigui exactament:

100,00 €.

---

# 24. CÒDIc I ENTREGA

Genera el fitxer HTML complet.

No em donis pseudocodi.

No em donis fragments.

No em donis només l'estructura.

Vull el **codi HTML complet i funcional**, preparat per guardar-lo com:

`compte-facil.html`

i obrir-lo directament en qualsevol navegador modern.

Comenta breument les parts principals del JavaScript perquè el codi sigui fàcil de mantenir.

Prioritza codi net, modular i fàcil de modificar.

Abans de finalitzar, revisa especialment:

1. Els càlculs.
2. L'arrodoniment.
3. La suma exacta del total.
4. El comportament dels grups.
5. El càlcul dels nens mitjançant coeficients.
6. La visualització en mòbil.
7. La validació dels camps.
8. Que no existeixin dependències externes.

L'objectiu és obtenir una aplicació petita, ràpida, clara i funcional.
