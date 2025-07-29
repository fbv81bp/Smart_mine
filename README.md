# Okos akna deaktiváló vevő kriptográfiai protokoll motorja

Egy okos taposóakna nem árulhatja el, hogy hol van, és keveset kell fogyasszon, mindkettő miatt egyirányú, sugárzott rádió adás vételére épülő egyirányú protokoll kell: az aknában csak rádió vevő lehet. Ezzel kell tudni esetileg deaktiválni ill. a teljes aknamezőt néha ákódolni.

Az aknáknak időosztásos ugrókóddal kell működniük a visszajátszhatóság ellen, a személyi deaktiváló adók pedig oldaltámadás védelemmel kell, hogy rendelkezzenek, hogy ne legyenek másolhatóak - de ha másolnák, vagy tömegesen ellopnák, az akna mező központilag átkódolandó.

Ha egy hash sorozat preimage-eit alkalmazzuk az átkódolások során, az egyszerre egy oldaltámadás védett protokoll, és kvantum biztos kriptográfia. Az időosztásos ugrókód pedig lehet az ilyen mesterkulcsból eredő hash-lánc vége.

A hash-lánc jelenthet 64 egymás utáni hash-t, melyeknek egy monoton növekvő, 64 bites számláló bitjeit használjuk a sózásához. Ha ez a számlaló telítődik, az akna deaktiválódik. Ha új mesterkulcsot kap, az pedig lenullázza. Az alacsony fogyasztás érdekében másodpercenként elég kódokat váltani, de annyira kell sűrűn, hogy az üldöző ne tudhassa visszajátszani. A kódoknak továbbá egykét lépés áfedéssel kell dolgozniuk: nehogy valaki felrobbanjon, mert pár másodperccel eltér, hogy az adójában, vagy épp az aknában a számláló mikor lett lenullázva.

Biztonsági szempontból nem tűnik hülyeségnek rövidebb számlálót használni, többféle mesterkulcsos aknával védeni egy területet, és csak azoknak és akkor frissíteni a mesterkulcsát, amelyek és amikor már deaktiválódtak. Így elkerülhetőbbek az eltérő mesterkulcs miatti balesetek.

Nyilván ebben az esetben a számlálók is eltérő fázisokban kell, hogy járjanak le, hogy valamennyi védettség mindig maradjon a területen. Túl rövid idő alatt sem jáhat le a számláló, nehogy egy támadás közbeni rádió zavarás miatt ne lehessen újra aktiválni az aknamezőt...(!)

Irányérzékeny antenna, ami kifejezetten függőleges irányból vesz, oldalról nehezebb legyen bezavarni a kikapcsolási adót. Viszont átkódoláshoz pont, hogy oldalról jön a jel, így kétféle antenna kell, de utóbbi is lehet irányérzékeny feltanítás után. Avagy drónnal fölé kell repülni az újrakódoláshoz (hülyeség, de megoldható, és oldalról a földből nem is biztos, hogy képes máshogy venni).
