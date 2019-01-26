# Work in progress :)

## Architecture /Event Loop
Node.js in the runtime environment for executing javascript code
Node.js can be used  to build highly scalable apis.
Node.js uses chrome’s V8 engine to execute javascript code.
Node.js is nonblocking and asynchronous  
Node.js is ideal for I/O intensive applications
Node.js is not ideal for cpu intensive applications like video encoding and image manipulation applications
All Javascript, V8 and the event loop run in one thread called the main thread.
Node.js uses a pre-allocated sets of threads called the Thread Pool, The default is 4
Libuv provides an Event Loop and a Thread Pool to achieve all of that. Libuv creates a pool with four threads that is only used if no asynchronous api is available
Event loop is a set of phases with dedicated data structures for each phase.

One thread === one call stack






Node.js :-
Global objects
Every file created in the node js system is a module and every function and variable declared in that file is scoped to that file.
console.log(module); 



## REST :-
Every object has some state(data) and behaviour(methods).In order to transfer state of object on server at particular instance of time to client, some sort of representation is needed like JSON or xml or any other format.
So REST is about creating representation of object's current state and transferring that representation over network.
It is not a protocol , it is an architectural design. It uses http verbs and maps it with the application request handlers.




Route parameters are used for essential and required values 
Query parameters are used to provide  additional data to backend servers, any data which is optional
Input validation, joi package can be used to validate the input
Brcypt for password hashing

## Middleware:-
A middle ware function is a function that takes a request object from client and either returns  the response  to the client or passes the control to another middleware function .
Request processin pipeline. Request from client ===> middleware1 ===> middleware 2 ===> middleware n ===> response to client
Request-response lifecycle
Express Middleware used in request processing pipeline
urlencoded middleware for parsing encoded parameters in the body of the  request and converting into json object
Use helmet middleware for headers
Morgan middleware :- for logging http request

Setting different environment test/dev, pre prod, production

## Common Http status codes:-
200:- success 
204:- if request was successful but no response needed to be sent in the body from server then we can use 204
207:- if there are multiple operations to be performed in the request , some of them were successful and some of them not then server can respond with 207 status.
404:- not found
400:- bad request, input validation error i.e. whatever the client sent in the request was not the right data.
401
403:- forbidden , missing api key in header
500
501
502
503

## Javascript:
Three asynchronous apis
Callback
Promises
Async Await :- use try catch with this api 

Promise states:- pending, fulfilled, rejected


Factory function :- it is a function which when called returns another function

## Mongodb 
Collection === table in db
Document === row in db
Port no:27017
Modelling relationships:-
  Using References(Normalization) separate collections ==> consistency 
  Using Embedded documents (Denormalization) one document embedded within another ==> query performance is better
  Hybrid approach :- use some document not complete document  in another document 

Which technique to choose between the above two depends upon your application 
Need to do Trade-off between query performance vs consistency 

Transactions === two phase commit
Fawn package can be used for transaction in mongodb 

Mongoose:-
Mongoose has schemas which defines the shape of the document
Schemas are compiled into models 


Objectids in mongodb:-
__id: it have 24 characters and 2characters represent a byte so it has 12 bytes to uniqually identify an object in mongodb
 4 bytes: timestamp
 3 bytes: machine identifier
 2 bytes: process identifier
 3 bytes: counter

## Authentication and Authorization
* Authentication:- it is the process of identifying if the user who claim they are.
* Authorization:- it is the process of determining if the user has the right to perform an operation or not.
* JSON Web Token:- When the user logins into the server , server returns a jwt to client , for every request client will pass jwt along with request to server
* JWT has three parts:- Header(Algorithm + Type) + Payload(json object) + Digital Signature()
* Only server can create a jwt as only it has a private/secret key to generate signature, if a hacker tries to modify a jwt , and sends the request to server , his request will not be authorised and he won’t be able to perform any action.
* JWT token can be sent to client in response header also. Client should send the token to server in request header.
* Always protect the operation that can modify the data and make them available only to authenticated users.
* Do not store the jwt on to the server in db , jwt will be present in client side only , delete it from client if you want the user to log out. Use https to encrypt the connection so that man in the middle cannot access tokens.
* Role based authorisation :-


## Microservices:-
A microservice architecture is for big projects with lot of people


## Webpack:-
Web pack is a bundler and optimises your files also traspiles the js files into different versions
(entry point )app.js. ===> Loaders(applied on per file basis e.g.:- babel loader, css-loader) ===> Plugins(applied on concatenated bundled file before writing to output/dist folder, e.g. :- uglify) ===> output(e.g.:- dist/bundle.js)

Why is it needed
If you want to put all the dependencies and files into one file in order to avoid import statement (also we do not have import statement in front end javascript ) then we need to use webpack
How do you import and export things in JavaScript? How do you make functions of your code visible to the outer world and how do you import functions from other people’s code? The only way has always been through global variables. For example if you want to use jQuery:
<script src="//code.jquery.com/jquery-1.12.0.min.js"></script>
<script>
// `$` global variable available here
</script>
And what if you want to split your own code in comprehensive small files? You will end up with something like this:
<script src="//code.jquery.com/jquery-1.12.0.min.js"></script>
<script src="/js/foo.js"></script>
<script src="/js/bar.js"></script>
<script src="/js/foobar.js"></script>
<script>
// Here goes some code
</script>
Now in the script tag you can use all those dependencies. But what if foo.js depends on bar.js? You must change the order of the scripts. Hmm this is becoming a mess:



## Node.js unit testing
* Testing a unit without its external dependencies is unit testing.
* For a given function the number of unit test should be equal to or greater then the execution path in that function. 
* Make a assertion within test case.
* Grouping the tests using describe function in jest.
* Whenever you change the implementation of your function or code the test cases should pass as Refactoring a function or a piece of code means changing the structure of the code without changing its external behaviour.
* Test case should not be too specific or too general, when testing for strings don’t test for too specific string , instead  try to match or check if the string contains a particular substring.
* Different false values => Null, undefined, NaN, ‘’, 0, false
* Parameterized testing allow a developer to run the same test over and over again using different values
* Single assertion principle.:- There should only be a single assertion in a test case.
* General rule of thumb:- use unit test for testing functions with algorithms that have zero or minimal dependency on external resources., Try to avoid to create too many mocks.


## Node.js integration testing
Testing a unit with its external dependencies

## Node.js End to End testing
Testing an application from an UI e.g.:- selenium

## Node.js Test Driven Development 




Provide env variables from cli
export  PORT=5000


## Configuration and environment:-
 


## Debug:-


## Logs handling 
Winston  provides three transport method:-
Console, file, http





## REST api folder structure:-
app/	
	|---models/
	|---controller/
	|---helpers/
	|---middlewares/
	|---tests/
	|---models/
	|---controllers/
	|---middlewares/
	|---node_modules/
	|---app.js
	|---package.json
	
	
	models/ – represents data, implements business logic and handles storage
	controllers/ – defines your app routes and their logic
	helpers/ – code and functionality to be shared by different parts of the project
	middlewares/ – Express middlewares which process the incoming requests before handling them down to the routes
	tests/ – tests everything which is in the other folders
	node_modules/ - all npm requried for app
	app.js – initializes the app and glues everything together
	package.json – remembers all packages that your app depends on and their versions


## Node.js design pattern:-
Information expert principle
Repository design pattern
