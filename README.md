# vage-docs-voor-taglets
slechte attempt at documentatie voor taglets van een vak dat ik niet ga noemen om niet gevonden te worden via google

Alle definities en uitleg hier is mijn persoonlijke interpretatie, neem dus zeker niet aan dat alles correct is.
Als iemand een fout ziet gelieve een PR te doen om het te verbeteren want ik gebruik dit zelf dus zou wel handig zijn als het allemaal juist was :p

Legende:
* A moet B bevatten -> tag B moet vlak boven de definitie van A staan
* A moet B omvatten -> tag B moet binnen de definitie van A staan
* O -> Object
* B -> Boolean Expression
* E -> Error

- [vage-docs-voor-taglets](#vage-docs-voor-taglets)
  * [`@basic`](#basic)
  * [`@creates`](#creates)
  * [`@immutable`](#immutable)
  * [`@invar`](#invar)
  * [`@mutates` & `@inspects`](#mutates--inspects)
    + [`@mutates`](#mutates)
    + [`@inspects`](#inspects)
  * [`@pre` & `@post`](#pre--post)
    + [`@pre`](#pre)
    + [`@post`](#post)
  * [`@representationObject(s)`](#representationobjects)
    + [`@representationObject`](#representationobject)
    + [`@representationObjects`](#representationobjects-1)
  * [`@throws`](#throws)
  * [`@peerobject(s)`](#peerobjects)
    + [`@peerObject`](#peerobject)
    + [`@peerObjects`](#peerobjects-1)
  * [`@mutates_properties`](#mutates-properties)
  * [`@may_throw`](#may-throw)

## `@basic`

**Een method moet `@basic` bevatten als en slechts als de method niet gedocumenteerd kan worden adhv `@basic` methods of methods die gedocumenteerd zijn adhv `@basic`, etc..**

## `@creates`

**Een method moet `@creates` bevatten als en slechts als de method een object maakt dat los staat van elk object dat al bestond, dus geen `@representationObject` of `@peerObject` is van een al bestaand object, en waar de klant dus volledige controle over heeft en mag aannemen dat dat object nooit gaat geinspecteerd of gemuteerd worden behalve als hij dat zelf doet.**

## `@immutable`

**Een class moet `@immutable` bevatten als en slechts als geen enkele instantie van die class na construction nog aangepast kan worden.**

**Een method moet `@immutable` bevatten als en slechts als de class waarin die method zich bevindt geen `@immutable` heeft, en heft veld dat returned wordt final/immutable is.**

deze laatste definitie ben ik heel onzeker van aangezien daar niks van in de cursus staat, maar 2 keren wordt deze tag op deze manier gebruikt dus ik vermoed dat dit bestaat.

## `@invar`

**Een class moet `@invar | B` bevatten of omvatten als en slechts als de conditie B altijd waar moet zijn.**

`@invar` buiten de definitie is publieke documentatie en mag dus enkel gebruik maken van publieke methods en fields.
`@invar` binnen de definitie is interne documentatie en mag dus gebruik maken van fields.

In vele gevallen moet elke `@invar` binnen een definitie ook buiten de definitie geschreven worden adhv public methods, aangezien binnenste `@invar`s enkel voor de programmeur zijn.

## `@mutates` & `@inspects`

### `@mutates`

**Een method moet `@mutates | O` bevatten als en slechts als het object O al bestond, en het object O aangepast wordt, een @representationObject van O wordt aangepast, of een @representationObject van een @representationObject, etc..**

### `@inspects`

**Een method moet `@inspects | O`  bevatten als en slechts als het object O al bestond, de method het object O inspecteert, een @representationObject van O inspecteert , een @representationObject van een @representationObject van O inspecteert, etc. EN als het geen `@mutates | O` tag bevat. Als object O al gemuteerd wordt moet er dus geen `@inspects | O` staan, maar dit is natuurlijk niet fout.**

O kan ook `this` zijn indien het zichzelf aanpast of inspecteert, respectievelijk zoals setters en getters (alhoewel dit bij getters al by default is, maar bij setters niet).

`@mutates` en `@inspects` zijn enkel nodig als O mutable is. Als O immutable is kan het dus niet gemuteerd worden en is het altijd `@inspects`, dus dit moet niet geschreven worden.

By default als er geen`@mutates` of `@inspects` staat mag een method elk mutable object muteren en inspecteren, maar dit lijkt mij counter-intuitive aangezien men dan nooit `@inspects` of `@mutates` moet toevoegen, dus ik werk persoonlijk altijd onder de assumptie dat de default is dat niks mag geïnspecteerd of gemuteerd worden zonder dat de tags er staan. (als iemand mij hier een tegenvoorbeeld kan leveren waarom dit wel logisch is, please do, mijn mentale gezondheid is er onder aan het lijden)
Een constructor mag by default zichzelf muteren 
Als een method name begint met ‘get’ of ‘is’ is de default dat het niks mag muteren en `this` inspecteert. De symmetrische default voor setters bestaat niet voor zover ik kan vinden, dus daar moet altijd een `@mutates | this` gezet worden.

## `@pre` & `@post`

### `@pre`

**Een method moet `@pre | B` bevatten als en slechts als de method enkel werkt onder de assumptie dat de boolean expression B waar is voor het beginnen van de method.**

`@pre` is enkel van toepassing voor contractueel programmeren, waar men mag aannemen dat de klant de documentatie duidelijk heeft gelezen en zich daar altijd aan houdt.
Zie `@throws` voor de tegenhanger van `@pre` bij defensief programmeren.

### `@post`

**Een method moet `@post | B` bevatten als en slechts als de boolean expression B waar moet zijn op het einde van de method.**

`@post` maakt aan de klant duidelijk dat bepaalde condities waar zijn na het uitvoeren van een method, bijvoorbeeld dat na een setter op te roepen, de getter gelijk is aan de doorgegeven waarde. In de postconditie kan naar het resultaat (de return waarde) van de method gerefereerd worden adhv `result` en kan men `old(value)` gebruiken om te verwijzen naar wat `value` was voor de methode. Dit kan bvb ook old(getHeight()) zijn, aangezien deze expressies gewoon geëvalueerd worden voor het uitvoeren van de method.

## `@representationObject(s)`

### `@representationObject`

**Een field moet `@representationObject` bevatten als en slechts als de field:**
* **een collection is, meestal.**
* **zelf geen betekenis heeft, maar een hoop elementen bevat die samen 1 property vormen.**

Deze definitie is minder duidelijk dan anderen, simpelweg omdat ik nergens in de cursus een duidelijke, objectieve uitleg van representation Objects vond, ik kan natuurlijk iets gemist hebben of fout geïnterpreteerd hebben.

### `@representationObjects`

**Een field moet `@respresentationObjects` bevatten als en slechts als de field zelf een `@representationObject` is, en daarboven opgebouwd is uit representation objects**

Deze definitie is nog vager aangezien deze tag maar 2 keer gebruikt is in het hele boek en nergens een uitleg heeft voor zover ik kan zien.

## `@throws`

**Een method moet `@throws E | B` bevatten als en slechts als de method een error van type E gooit wanneer conditie B waar is.**

Bij defensief programmeren wordt dit bvb gebruikt voor input validation ipv `@pre` bij contractual programming. Merk op: `@throws` is enkel documentatie en gaat dus niet zelf throwen, de effectieve check op de conditie en daarna de throw moeten nog apart geïmplementeerd worden door de programmeur.


## `@peerObject(s)`

nog niet gezien

### `@peerObject`

### `@peerObjects`

## `@mutates_properties`

nog niet gezien

## `@may_throw`

nog niet gezien
