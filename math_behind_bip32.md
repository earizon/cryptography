## Maths behind BIP32 (Child Key Derivation)
* <https://medium.com/@robbiehanson15/the-math-behind-bip-32-child-key-derivation-7d85f61a6681>

The algorithm for generating child:

 ```
 ┌ extending parent PRIVATE key to create child PRI.key ──┐
 │                                                        │
 │ INPUT                                  OUTPUT          │
 │ =====                                  ======          │
 │ k=parent   ·························>  a=k+h,child[0]  │
 │ priv.key                        ┌···>  priv.key        │
 │ (256bits)                 h=left·      (256bits)       │
 │  ·                          256b·       ·              │
 │  v                              ·       v              │
 │ K=parent ······> HMAC-SHA512    ·      child[0]        │
 │ pub.key     ┌··> (512bits)    ··┤      pub.key         │
 │ (264bits)   · ┌> one-way func   ·      (264bits)       │
 │ K=G·k       · ·                 ·      A =G·(k+h)      │
 │             · ·          rigth  ·                      │
 │ Parent      · ·          256bits└···>  child[0]        │
 │ Chain Code ·┘ ·                       Chain Code       │
 │ (256bits)     ·                       (256bits)        │
 │               ·                                        │
 │ Idx Number    ·                                        │
 │ (32 bits)   ··┘                                        │
 │ e.g. [0])                                              │
 └────────────────────────────────────────────────────────┘
 ```

 ```
 ┌ extending parent PUBLIC  key to create child pub.key ──┐
 │                                                        │
 │ INPUT                                      OUTPUT      │
 │ =====                                      ======      │
 │ k = parent ← Not really needed!!!                      │
 │ priv.key                                               │
 │ (256bits)                                              │
 │   ·                             left                   │
 │   v                             256bits                │
 │ K=parent                          ┌···>  child[0]      │
 │ pub.key     ┌··> (512bits)    ····┤      pub.key       │
 │ (264bits)   · ┌> one-way func     │      (264bits)     │
 │ (K=G x k)   · ·                   │      A=  K + G·h   │
 │             · ·                   │       =G·k + G.h   │
 │             · ·                   │                    │
 │ Parent      · ·                   └···>  child[0]      │
 │ Chain Code ·┘ ·                 rigth    Chain Code    │
 │ (256bits)     ·                 256bits  (256bits)     │
 │               ·                                        │
 │               ·                                        │
 │ Index Number  ·                                        │
 │ (32 bits)   ··┘                                        │
 │ e.g. [0]                                               │
 └────────────────────────────────────────────────────────┘
 ```

* See also. Andrea Corbellini Online tools:
  ECC mul: <https://andrea.corbellini.name/ecc/interactive/modk-mul.html>
  ECC add: <https://andrea.corbellini.name/ecc/interactive/modk-add.html>

