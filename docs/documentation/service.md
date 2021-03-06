
# AccountOwnedMosaicsService

Definition

```typescript
/**
 * Service to get account owned mosaics
 */
export declare class AccountOwnedMosaicsService {
    
    /**
     * accountHttp
     */
    accountHttp: AccountHttp;
    
    /**
     * mosaicHttp
     */
    mosaicHttp: MosaicHttp;
    
    /**
     * constructor
     * @param accountHttp
     * @param mosaicHttp
     */
    constructor(accountHttp: AccountHttp, mosaicHttp: MosaicHttp);
    
    /**
     * Account owned mosaics definitions
     * @param address
     * @returns {Observable<MosaicDefinition[]>}
     */
    fromAddress(address: Address): Observable<MosaicDefinition[]>;
}

```

Usage

```typescript
import {NEMLibrary, NetworkTypes, Address, AccountOwnedMosaicsService, AccountHttp, MosaicHttp} from "nem-library";

// Initialize NEMLibrary for TEST_NET Network
NEMLibrary.bootstrap(NetworkTypes.TEST_NET);

let address = new Address("");
let accountOwnedMosaics = new AccountOwnedMosaicsService(new AccountHttp(), new MosaicHttp());
accountOwnedMosaics.fromAddress(address).subscribe(mosaics => {
    console.log(mosaics);
});
```

Output:

```
[ MosaicDefinition {
    creator: 
     PublicAccount {
       address: [Object],
       publicKey: '34f510bc0173a1b65a0531e2fbb65b6db764234842d89b905e3071c4732ca3fd' },
    id: MosaicId { namespaceId: 'country.cat', name: 'patufet' },
    description: 'patufet coin',
    properties: 
     MosaicProperties {
       initialSupply: 7000000,
       supplyMutable: true,
       transferable: true,
       divisibility: 0 },
    levy: undefined,
    metaId: 319 },
  MosaicDefinition {
    creator: 
     PublicAccount {
       address: [Object],
       publicKey: '0e4573c386c5f891d2e61bfb5a96144fbd9881980b885751dba471ae1807dc34' },
    id: MosaicId { namespaceId: 'server', name: 'masteroftheworld' },
    description: 'description',
    properties: 
     MosaicProperties {
       initialSupply: 100000000,
       supplyMutable: true,
       transferable: true,
       divisibility: 0 },
    levy: MosaicLevy { type: 1, recipient: [Object], mosaicId: [Object], fee: 5 },
    metaId: 386 }]
```

[Run the code](https://github.com/aleixmorgadas/nem-library-examples/blob/master/concepts/service/AccountOwnedMosaicsService.ts)


# MosaicService

Definition

```typescript
/**
 * Mosaic service
 */
export declare class MosaicService {
    /**
     * mosaicHttp
     */
    private mosaicHttp;
    /**
     * constructor
     * @param mosaicHttp
     */
    constructor(mosaicHttp: MosaicHttp);
    /**
     * Calculate levy for a given mosaicTransferable
     * @param mosaicTransferable
     * @returns {any}
     */
    calculateLevy(mosaicTransferable: MosaicTransferable): Observable<number>;
}
```

Usage

```typescript
import {NEMLibrary, NetworkTypes, MosaicId, MosaicLevy, MosaicLevyType, Address, MosaicTransferable, MosaicHttp, MosaicProperties, MosaicService} from "nem-library";

// Initialize NEMLibrary for TEST_NET Network
NEMLibrary.bootstrap(NetworkTypes.TEST_NET);

let levyMosaicId = new MosaicId("server", "testmosaic");
let levy = new MosaicLevy(MosaicLevyType.Percentil, new Address(""), levyMosaicId, 5);
let mosaicTransferable = new MosaicTransferable(new MosaicId("server", "mosaic"), new MosaicProperties(0, 10000000, true, false), 100000, levy);

let mosaicService = new MosaicService(new MosaicHttp());
mosaicService.calculateLevy(mosaicTransferable).subscribe(levy => {
    console.log(levy);
});
```

Output:

```
5
```

[Run the code](https://github.com/aleixmorgadas/nem-library-examples/blob/master/concepts/service/MosaicService.ts)

# QRService

Definition

```typescript
export declare class QRService {
    /**
     * Generates the QR text from the wallet
     * @returns {string}
     */
    generateWalletQRText(password: Password, wallet: Wallet): string;
    /**
     * Decrypt the private key from the QR text
     * @param password password
     * @param qrWalletText Object generated by generateWalletQRText method
     * @return Decrypted private key
     */
    decryptWalletQRText(password: Password, qrWalletText: QRWalletText): string;
    /**
     * Generates the QR text from an address
     * @returns {string}
     */
    generateAddressQRText(address: Address): string;
    /**
     * Decrypt the address from the QR text
     * @param qrAddressText Object generated by generateAddressQRText method
     * @return Address
     */
    decryptAddressQRText(qrAddressText: QRAddressText): Address;
    /**
     * Generates the QR text from a transaction
     * @returns {string}
     */
    generateTransactionQRText(recipientAddress: Address, amount: number, msg: string): string;
    /**
     * Decrypt the transaction from the QR text
     * @param qrTransactionText Object generated by generateTransactionQRText method
     * @return TransferTransaction
     */
    decryptTrasactionQRText(qrTransactionText: QRTransactionText): TransferTransaction;
}
```