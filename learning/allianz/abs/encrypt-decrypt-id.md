## Encrypting and decrypting Porposal/Contract ID

Applications are using encrypted IDs for communication between each other. 
To encrypt such id it is required to use below http request:

`GET https://abs-adapter-210.allianzdirect-k8s-test.ec1.aws.aztec.cloud.allianz/at.allianz.abs.edp.adapter/services/crypt/<ID>/encrypt`

where `<ID>` is UUID of the contract

ie:

`GET https://abs-adapter-210.allianzdirect-k8s-test.ec1.aws.aztec.cloud.allianz/at.allianz.abs.edp.adapter/services/crypt/c78914f4-ebce-11e8-8d89-00059a3c7a00/encrypt`

That should return such response:

```
{
     "link": "V27CE4066FDBE9DC66F300922EBC28A9326EDA92FF291027623C0198432A648E9294950C7F5B742CF61EF33FB3159E808F"
}
 ```
 
The decryption uses such URL:
`GET https://abs-adapter-210.allianzdirect-k8s-test.ec1.aws.aztec.cloud.allianz/at.allianz.abs.edp.adapter/services/crypt/<ID>/decrypt`


where `<ID>` is encryted UUID

ie.
`GET https://abs-adapter-210.allianzdirect-k8s-test.ec1.aws.aztec.cloud.allianz/at.allianz.abs.edp.adapter/services/crypt/V225FDFB27BDCBF885681829F010B7B24679215C362DC5C3CF5E0472313CF420CD8681724AD5CEAFA4AE548AEA0B8697AA/decrypt`

That should return:
```
05a55627-5d02-11e9-9e32-0a5801e1223a
```