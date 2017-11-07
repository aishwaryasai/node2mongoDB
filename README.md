Install Node, Express, MongoDB 
1) create express generator project (basic skeleton)
express testproject 

2) add dependencies- DB dependencies to package.json
"mongodb": "^2.2.25",
 "monk": "^4.0.0",

3) install dependencies
cd testproject
npm install

check node_modules of testproject , it'll have list of all dependencies installed

4) create directory to store DB data in the testproject (Database)
mkdir data

5) start the server
npm start

You are now running Node JS webserver, with the Express engine and Jade HTML preprocessor installed.

express.router is used in routes folder files. why?
Use the express.Router class to create modular, mountable route handlers. A Router instance is a complete middleware and routing system; 


Next,print something on webpage:

6) alter index.js from routes and create instance of express.Router call it router and use it when a http get request in made to display something on the webpage

Add to index.js in routes folder
/* GET Hello World page. */
router.get('/helloworld', function(req, res) {
    res.render('helloworld', { title: 'Hello, there!' });
});

so when you open localhost:3000/helloworld you get 

Hello world this is a new page

7) Open index.jade in views folder
This gives the template of your message say "hello there" is being viewed on webpage

SImilarly we can create a new file helloworld.jade which gives the view template when localhost:3000/helloworld  request is made

Next, create a DB

8) Start server
change db path
mongod --dbpath testproject/data/
Mongo server is set up


9) Open Mongo console
run >mongo. 

> use node2mongo
switched to db node2mongo appears

10)  Insert data into db

db.usercollection.insert({ "username" : "user1", "email" : "user1@domain.com" })

view data using:
db.usercollection.find().pretty() //display with line breaks


insert more data using json format
>newstuff = [
{ "username" : "user2", "email" : "user2@domain.com" },
 { "username" : "user3", "email" : "user3@domain.com" } 
]

db.usercollection.insert(newstuff);


Now link Mongo to Node

11) Add mongodb and monk to app.js to establish connection and connect
var mongo = require('mongodb'); 
var monk = require('monk'); 
var db = monk('localhost:port/testproject'); 

12) make db accesible to user in app.js
app.use(function(req,res,next){
 req.db = db; 
next(); 
});


Next, get data from DB to your webpage

13 ) change index.js from routes , add a get request to get list of data to be displayed from the collection saved in DB 

14) add userlist.jade file to views, wch contains the template of userlist webpage

Next post data to DB from your webpage

15) change index.js from routes, add a post request to add a person to userlist

16) add template in userlist.jade to support the view for adding new user - creating a form here

