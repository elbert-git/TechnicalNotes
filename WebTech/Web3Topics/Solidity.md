# Solidity

---

# In General

===================================================================

It's a high level language to code smart contracts on the ethereum blockchain. Not only for Ethereum but most commonly associated with it.

**Smart Contracts**

think of them as a public c# object in the blockchain(or the cloud). they can hold variables(state) and functions.

# Basic Structure

===================================================================

```
pragma solidity ^0.8.4;

contract BasicContract{
  address owner;

  constructor(){
    owner = msg.sender;
  }
}
```

* **Version number**: every solidity file needs a version number to tell what compiler to use
* **contract object:** the contract itself. behaves like a public and cloud c# object
* **constructor**: a fucntion that is called at the the deployment of the contract. and only then. effectively a fucntion that runs on start();

### Scoping

```
pragma solidity ^0.8.4;

contract BasicContract{
  address public owner;
  function SetOwner(address newOwner) public {
    owner = newOwner;
  }
}
```

by default variables and functions are private. used only in the class privately. but you can expose them by the **public** keyword.

# Variables

===================================================================

### Ints

**unsigned vs normal integers**

normal integers are normal. unsigned just mean they can't be negative. it is an always positive number.

```
uint alwaysPositive = 22254;
int canBeNegative = -902314;
```

**integer bits**

you can also set how many bits to hold the integer. This is most likely a cost saving measure.

by default it ints and uints are 256 bits

```
int8
int16
.
.
.
int256

uint8
uint16
.
.
.
uint256
```

### Strings

just a normal string.

```
string basicString = "hello world";
```

### Addresses

every ethereum wallet and smart contract has an address.

an address is just a hyperlink/reference to a wallet or smart contract in the blockchain

```
address smartContractOwner = 0xpowie0923sdfg23;
```

### Arrays

like c# arrays. just an array that can dynamically resize. but accepts one type of object

```
int[] numberArray = [1,2,3]
```

### Mapping

basically python dictionaries but weirder

```
mapping(address => uint) dictionaryOfBalances;
dictionaryOfBalances[johnAccount] = 222;
```

This dict doesn't only hold strings as keys. it can by any data type. just denote what is the key value data types to create a dictionary.

then use it like a python dictionary

### Structs

basically javascript objects

* [ ] not sure if this can hold functions

Though most likely not, it's a python dictionary of sorts.

```
struct Person {
        string name = "hello";
        string favouritWoreds[] = ["Fungi", "Moist"];
    }
```

### Memory Vs Storage

You can mark a variable as memory or storage. whether it only exists in the run time of the function or persists throughout the life time of the contract.

This helps you save on gas fees by denoting what to save and what to keep.

```
string memory tempString public = "temp";
string storage permanentString public = "permanent";
```

### MSG object

This is is how you identify who is interacting with the smart contract.

at the start it will always be the deployer.

but other people can also interact with this contract. so when they call the fucntion. the msg object will be associated with them.

```
address currentUser = msg.sender;
```

# Functions

===================================================================

### Basics

```
    function BasicFunction (string stringArgument){
        // do things
    }

    function BasicPublicFunction (string stringArgument) public {
        // do things
    }
```

### Structure

```
function FunctionName(datatype varName) [public, pure, view] returns(datatype, datatype) 
```

* declare the function keyword
* followed by arguments it requires
* then public, pure, view modfiers
* then declare the returning data type

### Error Handling

##### Revert

```
if({boolean statement}){
  revert('error message string');
}
```

basically a function that cancels the entire blockchain call while returning a message error

##### Require

```
require({bool statement}, 'error message string');
```

similar to revert. just more concise

##### Assert

don't bother

### Modifiers

are like attachable operations to functions at the

```
modifier onlyOwner() {
  require(msg.sender == owner, "not owner"); // throw error if not owner
  _; // <-- function runs here. 
  // code here runs after function.
}
```

then attach to a function like this

```
function ChangeOwner (address newOwner) public onlyOwner {
  //
}
```

##### Preventing re-occuring function calls

A common use case modifiers.

like preventing double overlapping functions getting called.

```
modifier preventOverlappingCalls (){
 require(!locked, "Locked");
 locked = true;
 _;
 locked = false;
}
```

# Events

===================================================================

A way to to set up a signal that other contracts, objects, fucntions etc. can subscribe to.

This allows one code to call an arbitrary amount of functions

like emitting signals on trades to track who owns who

##### Declaring an event

```
event newEvent(){
  uint data = value;
}
```

they look like structs. this is so that events can also carry data to further describe the event.

##### Emitting an event

```
emit newEvent(2);
```

just call emit, then event name followed by the variables to make up that data.