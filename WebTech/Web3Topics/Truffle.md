# **-|- Truffle**

=========================================================

a framework for creating smart contracts

allows compilation, deployment and testing of smart contracts

testing uses ganache, a testing network

# **Installation**

=========================================================

```
npm install -g truffle
```

# **Project Setup**

=========================================================

```
truffle init
```

will create 3 folders, constracts, migration, tests and one truffle-config.js file

* Contract folder are where you store the contacts
* migrations folder are your deployment scripts
  * this is if you want to have some functions to be called on deployment. or inputting arguments to constructor
  * there is one file called migrations.sol by default. dont touch or delete. it's the deployment initializer
* tests are where you write your testing files in javascript.
* truffle config. are your deployment settings. you can control which network you deploy to here or which compiler you are using.

### Open zeppelin Contracts

you need to install them into node before you can import

```
npm install @openzeppelin/contracts
```

import by using the code below in you .sol contracts

```
import "@openzeppelin/contracts/path/to/contract";
```

# **Compilation**

===================================================================

```
truffle compile
```

This will create a /build/contracts/ folder. it will have a bunch of jsons.

ignore the first one, migration.json.

the rest are all of your compiled contacts. the json contains an abikey json inside; that's the pointer a web3js object will use to handle the contract

# **Testing**

=========================================================

usually you just write a js file that references the smart contract then interacts with it

below is an example test js file

```
const SimpleContract = artifacts.require('SimpleContract'); //in the require is the name of the smart contract object

contract('SimpleStorage' () => {
  it('Should Update Data', async () => {
    const storage = await SimpleStorage.new();
	await storage(10);
	const data = await storage.readData();
	assert(data.toString() === '10')
  })
});
```

* Import the contract

  use artifacts object(imported by truffle) to require import the contract text file.
* create a test contract function which takes the contract artifact and a call back func. the call back will run the tests.
* denote every test with an "it" which takes 2 arguments. a test name string and a fucntion that tests the contract.
* assert is the test. inside the bracket must be true to pass.

run tests by

```
truffle test
```

##### Common tests over the top of my head

* constructor runs well
* test all functions and result of all the functions.

# **Setting up for Deployment**

===================================================

### node init

do remember to start a node directory to run js script

```
npm init
```

### Install the wallet provider

This should just be the first step

```
npm install @truffle/hdwallet-provider
```

This allows our node js files to interact with wallets

### Infura Setup

Infura is a website to connect to a blockchain node, ethereum or a test net.

just create an account to access a hyperlink that points to a blockchain node.

you can paste the hyperlink/reference in the truffle-config.js.

just find the infuraKey variable. (it's commented by default). uncomment it.

* do remove the https link. just get the last url parameter. the long hash string

### Migrations Folder

you need migration files to instruct how to deploy the contract

in the migrations folder, the files are numbered. they are executed sequencially.

you can ignore the number 1. it's part of the project boiler plate.

second file onward are your contracts migration.

##### Samples Migration file

```
const contract = artifacts.require('{name of contract object}');

module.exports = function (deployer) {
  deployer.deploy(contract);
};
```

##### arguments for the constructor

are put in the deployer.deploy arguments. after the contract arterfact.

```
const contract = artifacts.require('{name of contract object}');

module.exports = function (deployer) {
  deployer.deploy(contract, constructorArg1, constructorArg2);
};
```

### truffle-config.js

most of the code is uncommented. just uncomment what you need.

like the:

* wallet provider stuff, l
  * wallet object
  * getting the seed phrase
* which network you are deploying to
  * you can paste the infura network reference in the object you uncommented as well.

### Rinkeby config

rinkeby config seems like our preferred test network,but for some reason it's not in the truffle default. below is the config object

```
rinkeby: {
      provider: function() { 
       return new HDWalletProvider(mnemonic, "https://rinkeby.infura.io/v3/<INFURA_Access_Token>");
      },
      network_id: 4,
      gas: 4500000,
      gasPrice: 10000000000,
  }
```

# **Deployment (locals, tests, for realsies)**

===================================================================

### Deploying to a local Blockchain (for testing)

##### Starting a local blockchain

below will start a local blockchain

```
truffle develop
```

it will also automatically connect to a truffle console

##### deploying contracts in local blockchain

```
migrate --reset
```

type the above in the truffle console.

### Deploying to a testnet

```
truffle migrate --network {network name}
```

match the network name to the uncommented network object in truffle-config.js