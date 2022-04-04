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

### Connecting with Infura API

```
const Web3Module = require('web3'); // import module
const web3 = new Web3Module('{link to node'}); // create instance
```

The node link is most like the link you get from infura ethereum node

### Connecting with Metamask Walllet

```
const Web3Module = require('web3'); // import module

async function init() {
  let web3 = new Web3Module(window.ethereum); // create instance
  await ethereum.enable(); //enable ethereum

  // ... more init function below
}

init();
```

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
const result = await contract.methods.{MethodName}(arg1, arg2).call();
```

### Transacting with contracts (read&write)

use the send method to call fucntions with gas. meaning that it can modify data and call operations on the smart contract.

```
await contract.methods.SetOwner(nameInput.value)
  .send(
    {
      from: selectedAccount,
      value: 394924431210087
	}
  );
```

##### Getting at transaction receipt

```
const receipt = await contract.methods.SetOwner(nameInput.value)
  .send(
    {
      from: selectedAccount,
      value: 394924431210087
	}
  );
```

it's returned from the send function call

### Converting to wei

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
    .request({method: 'eth_requestAccounts'})
    .then((accounts) => {
      selectedAccount = accounts[0]
    })
    .catch((err) => {
      console.log(err)
    });
  }
    
    //subscribe to account change events
    window.ethereum.on('accountsChanged', function (account) {
      selectedAccounts = account[0];
    })
  }
};
```

# **Calculating gas fees**

===================================================================

<https://www.youtube.com/watch?v=C4F3Qo6qvGI>