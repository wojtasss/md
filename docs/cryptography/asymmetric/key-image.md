# Monero private key image

!!! danger
    Author is nowhere close to being a cryptographer. Be sceptical on accuracy.

Private key image serves to detect double spending attempts.

In Monero funds are always sent to a one-time public key `P`.
Related one-time private key `x` is specific to unspent output.

As output can be spent only once (in whole), the related private key can be used only once.

Thus, specific private key image `I` being present on the blockchain means
that related output was already spent, and subsequent attempts must not be allowed.

This whole scheme is necessary because Monero uses Ring Signatures
which make it impossible to know whom exactly signed the transaction.
This is why a simple Bitcoin-like double spending check wouldn't work here. 

## Definition

    I = x*Hp(P)

Where:

* `I` - private key image (or "key image" for short)
* `x` - one-time private key used to unlock an unspent output
* `P` - one-time public key of an unspent output
* `Hp()` - hash function accepting an EC point as an argument 

The `P` comes from this:

    P = xG
    
Where `G` is the [Ed25519](/cryptography/asymmetric/ed25519) base point. 

Substitute `P` with `xG` and we get:

    I = x*Hp(xG)
    
The key image `I` is a one-way function of the private key `x`.

## Reference

* [StackExchange answer](https://monero.stackexchange.com/questions/2883/what-is-a-key-image)
* [Another SE answer](https://monero.stackexchange.com/questions/2158/what-is-moneros-mechanism-for-defending-against-a-double-spend-attack)