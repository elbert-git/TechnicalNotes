# ***-|-* NFTs**

<https://www.youtube.com/playlist?list=PLlr2FnHljEjH7zmcE7PZfLJTLw5XogqQg>

===================================================================

An nft is just a token in a contract that abides by the ERC-721 standard.

Basically picture a smart contract. that contract has a mapping of tokens to users.

when you mint an nft. the smart contract stores your ownership status.

It can also have other functionalities like transferring ownerships to others.

Tokens can be associated with:

* wallet address, to indicate ownership
* uri(universal resource indicator), to point to other forms of data

# **ERC-721**

===================================================================

Is a smart contract standardization that generates and store tokens. has functions to for other wallets to manage these tokens.

**[Open Zeppelin ERC-721 doc Link](https://docs.openzeppelin.com/contracts/2.x/api/token/erc721)**

**[ERC-721 official specifications](https://eips.ethereum.org/EIPS/eip-721)**

### Functions

* balanceOf(owner)
  * find out how many tokens a wallet has
* ownerOf(tokenId)
  * returns token's owner address
* safeTransferFrom(from, to, tokenId) \*
* transferFrom(from, to, tokenId)
* approve(to, tokenId)
* getApproved(tokenId)
* setApprovalForAll(operator, _approved)
* isApprovedForAll(owner, operator)
* safeTransferFrom(from, to, tokenId, data)

### Events

* Transfer(from, to, tokenId)
* Approval(owner, approved, tokenId)
* ApprovalForAll(owner, operator, approved)

### URI JSON Metadata Standards

URIs should return Jsons structured as so

```
{
  "name": ""
  "description": "" 
  "image": ""
}
```

* json
  * title: "Object title"
  * type: object type
  * properties: traits and other fluff go here

# **Creating NFT smart contract**

===================================================================

### The open zeppelin Wizard

Simplest way is to use the [open zeppelin wizard](https://docs.openzeppelin.com/contracts/4.x/wizard).

You can customize a boiler plate to create your smart contracts

# **Token URIs**

===================================================================

How to map other data to tokens.

It's just the using the \`\``_setTokenURI()`\`\` method in erc-721.

```
_setTokenURI(tokenID, {uri link});
```

you can put this function in the safeMint function to associate the uri during minting. 

# **Money Matters**

===================================================================

### Paying to smart contract

to add payment requirements to the different nft functions

* add payable modifier to function
* add \`\``require((msg.value >= {priceAmount}), "error message")`\`\`\`

This will make the function require ether to be sent to the smart contract.

### Withdrawing Ether from smart contract

you can put an operation to send ether automatically on paid function calls.

or create a withdraw() function that requires owner