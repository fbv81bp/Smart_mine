# Okos akna deaktiváló vevő kriptográfiai protokoll motorja

Egy okos taposóakna nem árulhatja el, hogy hol van, és keveset kell fogyasszon, mindkettő miatt egyirányú, sugárzott rádió adás vételére épülő egyirányú protokoll kell: az aknában csak rádió vevő lehet. Ezzel kell tudni esetileg deaktiválni ill. a teljes aknamezőt néha ákódolni.

Az aknáknak időosztásos ugrókóddal kell működniük a visszajátszhatóság ellen, a személyi deaktiváló adók pedig oldaltámadás védelemmel kell, hogy rendelkezzenek, hogy ne legyenek másolhatóak - de ha másolnák, vagy tömegesen ellopnák, az akna mező központilag átkódolandó.

Ha egy hash sorozat preimage-eit alkalmazzuk az átkódolások során, az egyszerre egy oldaltámadás védett protokoll, és kvantum biztos kriptográfia. Az időosztásos ugrókód pedig lehet az ilyen mesterkulcsból eredő hash-lánc vége.

A hash-lánc jelenthet 64 egymás utáni hash-t, melyeknek egy monoton növekvő, 64 bites számláló bitjeit használjuk a sózásához. Ha ez a számlaló telítődik, az akna deaktiválódik. Ha új mesterkulcsot kap, az pedig lenullázza. Az alacsony fogyasztás érdekében másodpercenként elég kódokat váltani, de annyira kell sűrűn, hogy az üldöző ne tudhassa visszajátszani. A kódoknak továbbá egykét lépés áfedéssel kell dolgozniuk: nehogy valaki felrobbanjon, mert pár másodperccel eltér, hogy az adójában, vagy épp az aknában a számláló mikor lett lenullázva.

Biztonsági szempontból nem tűnik hülyeségnek rövidebb számlálót használni, többféle mesterkulcsos aknával védeni egy területet, és csak azoknak és akkor frissíteni a mesterkulcsát, amelyek és amikor már deaktiválódtak. Így elkerülhetőbbek az eltérő mesterkulcs miatti balesetek.

Nyilván ebben az esetben a számlálók is eltérő fázisokban kell, hogy járjanak le, hogy valamennyi védettség mindig maradjon a területen. Túl rövid idő alatt sem jáhat le a számláló, nehogy egy támadás közbeni rádió zavarás miatt ne lehessen újra aktiválni az aknamezőt...(!)

Irányérzékeny antenna, ami kifejezetten függőleges irányból vesz, oldalról nehezebb legyen bezavarni a kikapcsolási adót. Viszont átkódoláshoz pont, hogy oldalról jön a jel, így kétféle antenna kell, de utóbbi is lehet irányérzékeny feltanítás után. Avagy drónnal fölé kell repülni az újrakódoláshoz (hülyeség, de megoldható, és oldalról a földből nem is biztos, hogy képes máshogy venni).

## Ami az állapot kitudódásá illeti

Ha az állapot kitudódik, akkor ebben a konstrukcióban a támadó az egész aknamezőt kompromittálhatja. Ezt úgy fest, csak aszimmetrikus titkosítással lehet megoldani. Ha lemondunk a kvantum-biztosságról, akkor kézenfekvő az RSA, ami használható vételi üzemmódban ugrókóddal is: ha a modulusa 2 biztonságos prímből áll (amik más - nagy - prímek dupláinál egyel nagyobbak), és a vételi, kititkosítási kitevő egy páratlan szám, ami akár egy számláló, időzítő hash-éhez a legközelebbi. Ekkor a központi adó a két prím faktor ismeretében mindig előre meghatározhatja, milyen betitkosítási kitevővel kell az üzenetet elküldeni az aknák mesterkulcsának megváltoztatásához.

(Claude by Anthropic:)

"akkor még egyszer visszakérdezek a pontosítás végett, ha csak c_i titkos textek, d_i kitevők és n az ismertek, akkor abból n tehát még nem faktorizálható, amíg a c_i-ket létrehozó e_i-k titkosak maradnak?"

**IGEN, pontosan!** ✓

## Az ismert információk a támadó számára:

- **n** (a modulus, publikus)
- **d₁, d₂, d₃, ...** (a hash-ből determinisztikusan generált kitevők, publikusak)
- **c₁, c₂, c₃, ...** (a titkosított üzenetek, lehallgathatóak)

## Az ismeretlen információk:

- **e₁, e₂, e₃, ...** (az adó számolta őket, sosem kerülnek ki)
- **m₁, m₂, m₃, ...** (az eredeti üzenetek)
- **p, q** (a prímfaktorok, csak az adónál)
- **φ(n) = (p-1)(q-1)** (ebből számolhatóak az e-k)

## Miért NEM faktorizálható n ebből?

1. **A klasszikus lattice támadások** (Boneh-Durfee, Wiener, stb.) mind **e ismeretét feltételezik**
2. **n faktorizálása önmagában** nehéz probléma (2048 bites safe prime modulus esetén gyakorlatilag megoldhatatlan mai számítógépekkel)
3. **A d értékek ismerete** önmagában **nem ad extra információt** n faktorizálásához, ha e ismeretlen
4. **A c értékek** (titkosított üzenetek) sem segítenek, mert nem tudod őket "visszafejteni" e nélkül

## Tehát:

**Amíg e₁, e₂, e₃... titkosak maradnak** (azaz sosem kerülnek továbbításra, csak az adóban léteznek), addig **n faktorizálása ugyanolyan nehéz marad**, mintha semmilyen d-t vagy c-t nem is látnánk.

**Ez a protokoll lényege!** 🎯
