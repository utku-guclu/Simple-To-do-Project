# Motoko - Web3 - DFINITY - Internet Computer
### ex:
```
// importlar

import Nat "mo:base/Nat";
import Nat64 "mo:base/Nat64";
import Cycles "mo:base/ExperimentalCycles";


// canister
// gas fee (cycle)

actor HelloCycles {
  // değişkenler

  // let -> immutable
  // var -> mutable

  let limit = 10_000_000;

  // fonksiyonlar (query, update)

  public func wallet_balance() : async Nat {
    // return -> return ... ;
    // return -> ...
    Cycles.balance()
    // return Cycles.balance();
  };

  public func wallet_receive() : async { accepted: Nat64 } {
    let available = Cycles.available();
    let accepted = Cycles.accept(Nat.min(available, limit));
    { accepted = Nat64.fromNat(accepted) };
  };

  public func transfer(
    receiver: shared() -> async (),
    amount: Nat) : async { refunded : Nat } {
      Cycles.add(amount);
      await receiver();
      { refunded = Cycles.refunded() };
    }

};

```


[smart contract address](https://a4gq6-oaaaa-aaaab-qaa4q-cai.raw.icp0.io/?id=zdg5y-iqaaa-aaaab-qacdq-cai&tag=2&did=c2VydmljZSA6IHsKICB0cmFuc2ZlcjogKGZ1bmMgKCkgLT4gKCksIG5hdCkgLT4gKHJlY29yZCB7cmVmdW5kZWQ6IG5hdDt9KTsKICB3YWxsZXRfYmFsYW5jZTogKCkgLT4gKG5hdCk7CiAgd2FsbGV0X3JlY2VpdmU6ICgpIC0%2BIChyZWNvcmQge2FjY2VwdGVkOiBuYXQ2NDt9KTsKfQo%3D#transfer)
