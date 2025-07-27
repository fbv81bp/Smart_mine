# Smart Mine Deactivation Receiver Cryptographic Protocol Engine

A smart landmine cannot reveal its location and must consume little power - both requirements necessitate a unidirectional protocol based on receiving unidirectional, broadcast radio transmissions: the mine can only contain a radio receiver. This must be capable of occasionally deactivating or sometimes recoding the entire minefield.

The mines must operate with time-division hopping codes against replay attacks, while personal deactivation transmitters must have side-channel attack protection to prevent copying - but if they were copied or stolen en masse, the minefield would need to be centrally recoded.

If we apply preimages of a hash sequence during recodings, this is simultaneously a side-channel attack protected protocol and quantum-secure cryptography. The time-division hopping code can be the end of such a hash chain derived from the master key.

The hash chain can represent 64 consecutive hashes, using bits of a monotonically increasing 64-bit counter for salting. When this counter saturates, the mine deactivates. Receiving a new master key resets it to zero. For low power consumption, codes need to be changed every few seconds...

...but frequently enough that pursuers cannot replay them. The codes must also work with one or two steps of overlap: so that no one gets blown up because their transmitter or the mine's counter was reset a few seconds apart.

From a security perspective, it doesn't seem foolish to use shorter counters, protect an area with multiple types of master-keyed mines, and only update the master keys of those that have already deactivated, and only when needed. This makes accidents due to different master keys more avoidable.

Obviously, in this case the counters must also expire in different phases so that some protection always remains in the area. The counter shouldn't expire too quickly either, lest radio jamming during an attack prevent reactivation of the minefield...!

A directional antenna that specifically receives from vertical directions would make it harder to jam the deactivation transmitter from the side. However, for recoding, the signal comes from the side, so two types of antennas are needed - though the latter can also be directional after training. Alternatively, one must fly a drone overhead for recoding (silly, but solvable, and from the side it might not be able to receive from the ground anyway).
