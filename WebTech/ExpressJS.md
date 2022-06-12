New tree

* express textbook def
* intuition on how to use
  * just a public object with a list of fucntions to call. these fucntions are called end points
* background info
  * rest apis
  * http 
* installation and setup
* usage

---

* express js
* npm init y
* npm install express
* install and setup nodemon
* create server.js
* import express
* start express server
* adding endpoints
  * to create one. chain a verb to an endpoint
  * callback func to handle to request. with request and response arguments
  * return with res.status(200).send({object}).
    * need to send json with response code
* get request
  * handling req and sending res
  * sending status codes
  * sending files to download
* rendering html
* Creating routes
  * creating a router (a mini, sub express server)
  * export and import routers to main folder and attach to main server
* create post endpoint
  * handle post
* middlewares for json
* 
* node js
* installation
* nodemon
* restful actions
  * put
  * get
  * post
  * patch

# new tree

* install
* setup
  * devtools nodemon
* basic gettting route
* nesting routes
  * shortened routing definiton code. the dot chain
* url parameters

---

# An even newer tree

* http
  * a common protocol to send data via networks
  * a client will send an http request. server will respond with http response
  * components of a http request
    * method: indicate what method you are trying to access... one of the CRUDs
    * address: address of receiver shows/end points
      * first is the base url
    * headers:
    * body:
* what the hell is a rest api
  * representational state transfer
  * resource is just data