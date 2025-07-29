## Cracking a master key of just one mine
1) If the master key ever gets compromised, it is easy to decrypt the new key when the central broadcast is sent to re-key the mine field with a pre-image of the contemporary master key.
2) Replacing master keys faster than they may be cracked doesn't work here either, for the enemy may record the radio transmissions of the new keys, and decide them once they find the very first master key.

### Patches
1) A possible patch may be to use multiple master keys, and only refresh one at a time, while taking the hash of all these master keys for the generation of the hopping keys. This way sets of mines can be deployed, whose master key sets partially overlap. Then if a few are stolen and their master key may be successfully read by tampering and side channels, the full mine field still won't be compromised.
