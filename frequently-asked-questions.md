# Frequently Asked Questions

## About the LNS Registry

### Why are names registered as hashes?

Hashes provide a fixed length identifier that can easily be passed around between contracts with fixed overhead and no issues passing around variable-length strings.

### Which wallets and dapps support LNS so far?

A partial list can be seen on [our homepage](https://bch.domains).

### Once I own a name, can I create my own subdomains?

Yes. You can create whatever subdomains you wish and assign ownership of them to other people if you desire. You can even set up your own registrar for your domain.

### Can I change the address my name points to after I’ve bought it?

Yes, you can update the addresses and other resources pointed to by your name at any time.

### Can I register a TLD of my own in the LNS?

No. We consider LNS to be part of the 'global namespace' inhabited by DNS, and so we do our best not to pollute that namespace. LNS-specific TLDs are restricted to only .bch (on mainnet), or .bch and .test (on Ropsten), plus any special purpose TLDs such as those required to permit reverse lookups.

In addition to that, we are deploying support for importing DNS domains from the majority of DNS top-level domains using an integration that relies on DNSSEC. For details on those plans, please read [this post](https://medium.com/the-ethereum-name-service/upcoming-changes-to-the-ens-root-a1b78fd52b38).

### Who owns the LNS rootnode? What powers does that grant them?

Since the owner of a node can change ownership of a subnode (unless they have otherwise locked it from their control), the owner of the root can change any node in the LNS tree. This means that the keyholders can replace the contracts that govern issuing and managing domains, giving them ultimate control over the structure of the LNS system and the names registered in it. However, the root key holders have locked control of the .bch registrar contract, which means that even keyholders cannot affect the ownership of .bch domains.

The keyholders are still capable of doing the followings:

* Control allocation and replacement of TLDs other than .bch - this is required to implement DNSSEC integration.
* Enable and disable controllers for the .bch registrar, which affect registration and renewal policies for .bch names.
* Update the pricing for .bch names.
* Receive and manage registration revenue.

Over time, we plan to reduce and decentralise human control over the system. Powers still held by the LNS root, such as those to set pricing and renewal conditions for domains, will be decentralised as robust systems become available to permit doing so.

### What about foreign characters? What about upper case letters? Is any unicode character valid?

Since the LNS contracts only deal with hashes, they have no direct way to enforce limits on what can be registered; character length restrictions are implemented by allowing users to challenge a short name by providing its preimage to prove it’s too short.

This means that you can in theory register both ‘foo.bch’ and ‘FOO.bch’, or even \<picture of my cat>.bch. However, resolvers such as browsers and wallets should apply the nameprep algorithm to any names users enter before resolving; as a result, names that are not valid outputs of nameprep will not be resolvable by standard resolvers, making them effectively useless. Dapps that assist users with registering names should prevent users from registering unresolvable names by using nameprep to preprocess names being requested for registration.

### Nameprep isn’t enforced in the LNS system. Is this a security/spoofing/phishing concern?

It’s not enforced by the LNS contracts, but, as described above, resolvers are expected to use it before resolving names. This means that non-nameprep names will not be resolvable.

### What are the differences between LNS and other naming services such as Namecoin and Handshake?

LNS complements and extends the usefulness of DNS with decentralised, trustworthy name resolution for web3 resources such as blockchain addresses and distributed content, while Namecoin and Handshake are efforts to replace all or part of DNS with a blockchain-based alternative.

## About the .bch Permanent Registrar

### How do the LNS Manager App and the Twitter bot know what names people are buying?

The LNS Manager App and the Twitter bot have built-in lists of common names, drawn from an English dictionary and Alexa’s list of top 1 million Internet domain names. They use these lists to show you when common names are bought or renewed. We do this because if the app didn’t reveal these names, anyone with a little technical skill could find them out anyway, giving them an advantage over those who don’t have the capacity to build their own list and code to check names against it.

### What does it cost to register a .bch domain?

Currently, registration costs are set at the following prices:

* 5+ character .bch names: 0.01BCH per year.
* 4 character .bch names: 0.1BCH per year.
* 3 character .bch names 1BCH per year.
* 2 character .bch names 10BCH per year.
* 1 character .bch names 100BCH per year.

1, 2, 3 and 4 character names have higher pricing to reflect the small number of these names available.

### What happens if I forget to extend the registration of a name?

After your name expires, there is a 90 day grace period in which the owner can't edit the records but can still re-register the name. After the grace period, the name is released for registration by anyone with a temporary premium which decreases over a 28 days period. The released name continues to resolve your ETH address until the new owner overwrites it.

### What kinds of behaviours are likely to result in losing ownership of a name?

The .bch registrar is structured such that names, once issued, cannot be revoked so long as an active registration is maintained.
