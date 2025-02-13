# Noble Multi-Sig Testnet Participants
During the noble testnet, we will be testing several multi-sig activities.  One of the first activities will be to manually send stake to a new validator. We have identified strangelove, noble, and everstake to be the multi-sig members for the testnet.  For mainnet additional organiztions will be included.

## How to create a multi-sig
Create a new key to be used in the testnet multi-sig. We recommend you use a ledger.

### Install noble
```
git clone https://github.com/strangelove-ventures/noble.git
cd noble
git checkout v0.3.0
make install
```
### Create the key
This is an example of how strangelove will create their noble key for multi-sig
```
nobled keys add strangelove --ledger

- name: strangelove
type: ledger
address: noble1v8m2aysw48a4w079t9kxj45pw28ga4ww6td0g8
pubkey: '{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"A24Ms1KsY/WVrg6j+pleIfvnFdjrU0/eB0ha1FRE6hD+"}'
mnemonic: ""
```
### Publish your public key
The public key is used to verify that you are who you say you are.  This should be known to the world, so anyone can easily verify if an action taken on the blockchain is from the real you or an impersonator. 

_Note: You must have a github account for this._

* Goto https://github.com/strangelove-ventures/noble-networks
* Click Fork in the top right.  
* Keep all the default values and click `Create fork`
* Click testnet/grand-1
* Click multi-sig
* Click `Add file` , then 'Create new file'
* In `Name your file` use your company name, example `company-pub.json`  
* in the box bellow, paste only your public key, EG
```
{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"A8SEPSEXxUno6j+wZb679d2QreuA+pQXURG8LAPqTPRP"}
```
* Under Commit new file add a title of `Company public key`. No description is needed. Click `commit new file` at the bottom. This will take you back to your fork.
* Click `Contribute` , then `Open Pull Request`, then `Create pull request`.
* At this point strangelove will review the PR and accept it into the multi-sig


## Strangelove will initiate all multi-sig transactions

### Import trusted participants
Strangelove will import all multi-sig public keys
```
nobled keys add strangelove-pub --keyring-backend test --pubkey='{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"A24Ms1KsY/WVrg6j+pleIfvnFdjrU0/eB0ha1FRE6hD+"}'

- name: noble-pub
type: offline
address: noble1v8m2aysw48a4w079t9kxj45pw28ga4ww6td0g8
pubkey: '{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"A24Ms1KsY/WVrg6j+pleIfvnFdjrU0/eB0ha1FRE6hD+"}'
```
repeated for all participants.

### Create new multi-sig wallet from trusted participants.
Strangelove will create the multi-sig wallet.
```
nobled keys add noble-multisig \
--multisig-threshold=2 \
--multisig=strangelove-pub,noble-pub,everstake-pub

- name: noble-multisig
type: multi
address: noble1553j0zdxvnfty72t4vkrm72afrvk33unxdgy9g
pubkey: '{"@type":"/cosmos.crypto.multisig.LegacyAminoPubKey","threshold":2,"public_keys":[{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"A24Ms1KsY/WVrg6j+pleIfvnFdjrU0/eB0ha1FRE6hD+"},{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"AlRjzl11UtfHJUMTf/IatbiUxOGxnk+E7J9DMFTIb0Uf"},{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"A2AC4WxQQZxeuSRrI1ey+kyGSgpbeV0dKcFzWbTcjeYy"}]}'
```
