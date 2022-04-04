# **-|- Restful APIs**

---

### **In general**

===================================================================

APIs are application programming interfaces. Allows different programs to talk to each other.

Restful apis are a common standard of structuring them.

### **Restful Standard**

===================================================================

Restful short for "representational state transfer".

In short it means that it organizes data into URIs. Like a URL.

```
https://api.com/v2/datapath
```

**Stateless**

Another key aspect is that the whole interaction should be "stateless". client and server shouldn't be tracking each other. only requesting and serving data.

### **Request Structure**

===================================================================

**Start Line**

```
POST/uriPath
```

Starts with the verb. the kind of action you are doing. Usually one of the CRUDs

then the uriPath linking to the specific resource you need.

* **Verbs**

Corresponding to all the different CRUD operations are

* POST | Create
* GET | Read
* PATCH | Update
* DELETE | delete

**Headers**

optional flags about the request.

like auth-tokens and in what format do you want to return the request

**Data**

Payload of data

* [ ] what the hell does this mean.

### **Response Structure**

===================================================================

**Status Code**

verify if you had an error, or the server had an error or the request was successful

* status codes in:
  * \~200: all a-okay
  * \~300: Client error
  * \~500: server error

**Headers**

Information about the server

**Data**

the actual data