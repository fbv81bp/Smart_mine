## Cracking a master key of just one single mine

The problem generally:
- having a system with a compromised state, that cannot be altered but is known to an adversary, and
- having a uni-directional communication channel, that may be eavesdropped, replicated, manipulated,
- is there a way to bring the system into a state unknown to the adversary, but known to its righteous owner?

1) If the master key ever gets compromised, it is easy to decrypt the new key when the central broadcast is sent to re-key the mine field with a pre-image of the contemporary master key.
2) Replacing master keys faster than they may be cracked doesn't work here either, for the enemy may record the radio transmissions of the new keys, and decipher them once they find the very first master key in an older mine.

#### Patches
1) A possible patch may be to use multiple master keys, and only refresh one at a time, while taking the hash of all these master keys for the generation of the hopping keys. This way sets of mines can be deployed, whose master key sets overlap only partially. Then if a few are stolen and their master key may be successfully read by tampering and side channels, the full mine field still won't be compromised. It is like having a Karnaugh table of mine sets: 4 indepent variables would create 2 ^ 4=16 different sets, each variable has two values 0 and 1, so we need 2 * 4=8 master keys to create 16 independent keying sets. For example with 16 variables, 2^16=65536 sets of mines can be created, with only 2 * 16=32 master keys.
2) Having a large hash value as the master key, like 384 bits, then comparing fewer, for example just the first 256 bits, and in a random order, of the new pre-image based key's hash against the contemporary master key should make the storage more SCA and tamper resistant against recovering the master key. This way some of the state stays secured abd the receiver channel's secrecy may stay safe.
3) Tampering sensors make the master key deleted.
4) Some heartbeat like, secured radio message is broadcast to the mines, of a mine looses that, it deletes its master key(?). Can be replayed though. Similar to having a GPS receiver to ban removal.
