# **Web3js**

===================================================================

Simplified api to interact with the blockchain. whether it's interacting with smart contracts or other wallets

# **Installation**

===================================================================

```
npm install web3
```

### Dealing with Webpack issues

Don't understand the issue but it's just that you can transpile web3 with the new webpack normally. you need to import a front-end build.

use the code below to use the Web3 object

```
import Web3 from "web3/dist/web3.min";
```

# **Setup**

===================================================================

```
const Web3Module = require('web3'); // import module
const web3 = new Web3Module('{link to node'}); // create instance
```

The node link is most like the link you get from infura ethereum node

# **Interacting with Contracts**

===================================================================

### Creating a contract instance

```
const Web3Module = require('web3'); // import module
const myContractJson = require('..path/to/json');

// this is the whole initialization function
const init = async () => {
  // create web 3 instance 
  const web3 = new Web3Module('{link to node}'); 
  
  // get network id
  const id = await web3.eth.net.getId();
  // get network 
  const deployedNetwork = myContractJson.networks[id];
   
  //create contract instance
  contract = new web3.eth.Contract(
    myContractJson.abi,
    deployedNetwork.address
  );
};
```

Looks complicated but too put simply. You just need a contract abi and address to create a new contract instance.

The contract abi is simple. just get from the compiled and deployed truffle build folder. There should be a json there somewhere.

The contract address is a bit complicated. just look at the code above.

### Calling Contract functions (read-only)

Put this in a async function. or follow the code above. you can put in the same async func.

usually read only function calls don't need gas

```
const result = await contact.methods.{MethodName}(arg1, arg2).call();
```

### Transacting with contracts (read&write)

use the send method to call fucntions with gas. meaning that it can modify data and call operations on the smart contract.

```
contract.methods.{MethodName}(arg1, arg2).send({
  from: {
    address, // from which wallet?
    value // the price of transaction
  }
});
```

##### Getting at transaction receipt

```
contract.methods.{MethodName}(arg1, arg2).send({
  from: {
    address, // from which wallet?
    value // the price of transaction
  }
});
```

it's returned from the send function call

# **Getting Metamask Wallets**

===================================================================

```
import Web3 from 'web3';

//create account variable
let selectedAccount;

// get account from metamask
export const init = () => {
  let provider = window.ethereum;
   
  // check if metamask provider exists
  if (typeof provider !== 'undefined'){
    // get account from metamask
    provider
    .request({method: eth_requestAccounts});
    .then((accounts) => {
      selectedAccount = accounts[0]
    })
    .catch((err) => {
      console.log(err)
    });
    
    //subscribe to account change events
    window.ethereum.on('accountsChanged', functions (account) {
      selected accounts = account[0];
    })
  }
};
```

# **Calculating gas fees**

===================================================================

<https://www.youtube.com/watch?v=C4F3Qo6qvGI>