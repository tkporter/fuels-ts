---
title: "Conversion"
parent: "Types"
grand_parent: "Guide"
---

[info]: this file is autogenerated
# Converting native types

You might want to convert between the native types (`Bytes32`, `Address`, `ContractId`, and `AssetId`). Because these types are wrappers on `Bytes` converting is a matter of using helpers. Here's an example:


```typescript
  import { arrayify, hexlify, randomBytes, Address, addressify, Contract, Wallet, WalletLocked } from 'fuels';

  const assetId: string = ZeroBytes32;
  const randomB256Bytes: Bytes = randomBytes(32);
  const hexedB256: string = hexlify(randomB256Bytes);
  const address = Address.fromB256(hexedB256);
  const arrayB256: Uint8Array = arrayify(randomB256Bytes);
  const walletLike: WalletLocked = Wallet.fromAddress(address);
  const provider = new Provider('http://localhost:4000/graphql');
  const contractLike: Contract = new Contract(address, abiJSON, provider);

  expect(address.equals(addressify(walletLike) as Address)).toBeTruthy();
  expect(address.equals(contractLike.id as Address)).toBeTruthy();
  expect(address.toBytes()).toEqual(arrayB256);
  expect(address.toB256()).toEqual(hexedB256);
  expect(arrayify(address.toB256())).toEqual(arrayB256);

  // it's bytes all the way down
  expect(arrayify(assetId)).toEqual(arrayify(Address.fromB256(assetId).toB256()));
```
###### [see code in context](https://github.com/FuelLabs/fuels-ts/blob/master/packages/fuel-gauge/src/doc-examples.test.ts#L131-L151)

---

