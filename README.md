# PROJECT-4
MEAN STACK IMPLEMENTATION

## PROJECT-4 : MEAN STACK IMPLEMENTATION

- It is time to get myself familiar with **MEAN stack** and deploy it to Ubuntu server after deploying **LAMP, LEMP and MERN Web stacks** in previous project.

- **MEAN Stack** is a combination of following components:
  - [MONGODB](https://www.mongodb.com) (Document database) – Stores and allows to retrieve data.
  - [Express](https://expressjs.com) (Back-end application framework) – Makes requests to Database for Reads and Writes.
  - [Angular](https://angular.io) (Front-end application framework) – Handles Client and Server Requests.
  - [Node.js](https://nodejs.org/en/) (JavaScript runtime environment) – Accepts requests and displays results to end user.

- **Side Self Study**

  - Refresh my knowledge of [OSI model](https://en.wikipedia.org/wiki/OSI_model)
  - Read about [Load Balancing](https://en.wikipedia.org/wiki/Load_balancing_(computing)), get myself familiar with different types and techniques of traffic       load balancing.
  - Practice in editing simple web forms with [HTML + CSS + JS](https://html-css-js.com)

- In previous projects I used different tools to connect to an EC2 instance, but if I do not want to install or launch anything outside of AWS, I can open my  CLI straight from Web Console in AWS, like this: [WebConsole](https://www.darey.io/wp-content/uploads/2021/02/WebConsole.gif)

- **TASK**
- In this assignment I implemented a simple **Book Register web form** using MEAN stack.


**STEP 1: Install NodeJs**

- **Node.js** is a JavaScript runtime built on Chrome’s V8 JavaScript engine. Node.js is used in this tutorial to set up the Express routes and AngularJS      controllers.

- Update ubuntu using `sudo apt update`

- Upgrade ubuntu using `sudo apt upgrade`

- I added certificates

```
`sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates

curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -`
```

- I installed **NodeJs** using `sudo apt install -y nodejs`


**STEP 2: INSTALL MONGODB**

- MongoDB stores data in flexible, JSON-like documents. Fields in a database can vary from document to document and data structure can be changed over time. For our example application, we are adding book records to MongoDB that contain book name, isbn number, author, and number of pages.
mages/WebConsole.gif

`sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6`

`echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list`

- I installed **MongoDB** using `sudo apt install -y mongodb`

- I started the **server** using `sudo service mongodb start`

- I verified that the service is up and running using `sudo systemctl status mongodb`

<img width="571" alt="MONGO IS UP AND RUNNING" src="https://user-images.githubusercontent.com/115954100/211838970-428bc8c6-3f37-48fb-bd98-665ad23a353a.png">

- I installed [npm](https://www.npmjs.com) – Node package manager using `sudo apt install -y npm`

- I installed [body-parser](https://www.npmjs.com/package/body-parser) package

- This ‘body-parser’ package helps to process **JSON files** passed in requests to the server. Body-parser installed using `sudo npm install body-parser`

- I created a folder named **Books** `mkdir Books && cd Books`

- In the Books directory, I initialized npm project using `npm init`

- Add a file to it named **server.js** and opened the file `vi server.js` 

- I copied and pasted the web server code below into the **server.js** file.

```
var express = require('express');
var bodyParser = require('body-parser');
var app = express();
app.use(express.static(__dirname + '/public'));
app.use(bodyParser.json());
require('./apps/routes')(app);
app.set('port', 3300);
app.listen(app.get('port'), function() {
    console.log('Server up: http://localhost:' + app.get('port'));
});
```


**STEP 3: Install [Express](https://expressjs.com) and set up routes to the server**  

- Express is a minimal and flexible **Node.js** web application framework that provides features for web and mobile applications. I used Express to pass book information to and from the MongoDB database.

- I used [Mongoose](https://mongoosejs.com) package which provides a straight-forward, schema-based solution to model the application data. I used Mongoose to establish a schema for the database to store data of my book register.

`sudo npm install express mongoose`

- In ‘Books’ folder, I created a folder named **apps** `mkdir apps && cd apps`

- I created a file named **routes.js** `touch routes.js` and opened the file `vi routes.js`

- I copied and pasted the code below into **routes.js*

```
var Book = require('./models/book');
module.exports = function(app) {
  app.get('/book', function(req, res) {
    Book.find({}, function(err, result) {
      if ( err ) throw err;
      res.json(result);
    });
  }); 
  app.post('/book', function(req, res) {
    var book = new Book( {
      name:req.body.name,
      isbn:req.body.isbn,
      author:req.body.author,
      pages:req.body.pages
    });
    book.save(function(err, result) {
      if ( err ) throw err;
      res.json( {
        message:"Successfully added book",
        book:result
      });
    });
  });
  app.delete("/book/:isbn", function(req, res) {
    Book.findOneAndRemove(req.query, function(err, result) {
      if ( err ) throw err;
      res.json( {
        message: "Successfully deleted the book",
        book: result
      });
    });
  });
  var path = require('path');
  app.get('*', function(req, res) {
    res.sendfile(path.join(__dirname + '/public', 'index.html'));
  });
};
```

- In the ‘**apps**’ folder, I created a folder named **models** and changed directory to this folder `mkdir models && cd models`

- I created a file named **book.js** and opened it `touch book.js && vi book.js`

- I copied and pasted the code below into ‘**book.js**’ 

```
var mongoose = require('mongoose');
var dbHost = 'mongodb://localhost:27017/test';
mongoose.connect(dbHost);
mongoose.connection;
mongoose.set('debug', true);
var bookSchema = mongoose.Schema( {
  name: String,
  isbn: {type: String, index: true},
  author: String,
  pages: Number
});
var Book = mongoose.model('Book', bookSchema);
module.exports = mongoose.model('Book', bookSchema);
```


**Step 4 – Access the routes with [AngularJS](https://angularjs.org/)**

- AngularJS provides a web framework for creating dynamic views in your web applications. In this tutorial, I used **AngularJS** to connect our web page with Express and perform actions on our book register.

- Change the directory back to ‘Books’ `cd ../..`

- I created a folder named **public** and changed directory to this folder `mkdir public && cd public`

- I added a file named **script.js** and opened it `touch script.js && vi script.js`

- I copied and pasted the Code below (controller configuration defined) into the script.js file.

```
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $http) {
  $http( {
    method: 'GET',
    url: '/book'
  }).then(function successCallback(response) {
    $scope.books = response.data;
  }, function errorCallback(response) {
    console.log('Error: ' + response);
  });
  $scope.del_book = function(book) {
    $http( {
      method: 'DELETE',
      url: '/book/:isbn',
      params: {'isbn': book.isbn}
    }).then(function successCallback(response) {
      console.log(response);
    }, function errorCallback(response) {
      console.log('Error: ' + response);
    });
  };
  $scope.add_book = function() {
    var body = '{ "name": "' + $scope.Name + 
    '", "isbn": "' + $scope.Isbn +
    '", "author": "' + $scope.Author + 
    '", "pages": "' + $scope.Pages + '" }';
    $http({
      method: 'POST',
      url: '/book',
      data: body
    }).then(function successCallback(response) {
      console.log(response);
    }, function errorCallback(response) {
      console.log('Error: ' + response);
    });
  };
});
```

- In public folder, I created a file named **index.html**; and opened it `touch index.html && vi index.html`

- I copied and pasted the code below into index.html file.

```
<!doctype html>
<html ng-app="myApp" ng-controller="myCtrl">
  <head>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
    <script src="script.js"></script>
  </head>
  <body>
    <div>
      <table>
        <tr>
          <td>Name:</td>
          <td><input type="text" ng-model="Name"></td>
        </tr>
        <tr>
          <td>Isbn:</td>
          <td><input type="text" ng-model="Isbn"></td>
        </tr>
        <tr>
          <td>Author:</td>
          <td><input type="text" ng-model="Author"></td>
        </tr>
        <tr>
          <td>Pages:</td>
          <td><input type="number" ng-model="Pages"></td>
        </tr>
      </table>
      <button ng-click="add_book()">Add</button>
    </div>
    <hr>
    <div>
      <table>
        <tr>
          <th>Name</th>
          <th>Isbn</th>
          <th>Author</th>
          <th>Pages</th>

        </tr>
        <tr ng-repeat="book in books">
          <td>{{book.name}}</td>
          <td>{{book.isbn}}</td>
          <td>{{book.author}}</td>
          <td>{{book.pages}}</td>

          <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
        </tr>
      </table>
    </div>
  </body>
</html>
```

- I changed the directory back up to **Books** `cd ..`

- I started the server by running this command `node server.js`

<img width="949" alt="NODE SERVER" src="https://user-images.githubusercontent.com/115954100/211865453-27279e2b-f87a-4f1f-b517-71911f29dc5b.png">

- The server is now up and running, I connected it via port 3300. One can launch a separate Putty or SSH console to test what curl command returns locally.

`curl -s http://localhost:3300`

- It shall return an HTML page, it is hardly readable in the CLI, but one can also try and access it from the Internet

<img width="774" alt="localhost3300" src="https://user-images.githubusercontent.com/115954100/211865281-bec43501-6826-48ca-b97a-a2c9ef5a30fe.png">

- For this –  I opened TCP port 3300 in my AWS Web Console for your EC2 Instance.

- Now you can access our Book Register web application from the Internet with a browser using Public IP address or Public DNS name.

- Quick reminder how to get your server’s Public IP and public DNS name:
- You can find it in your AWS web console in EC2 details
- Run `curl -s http://169.254.169.254/latest/meta-data/public-ipv4` for Public IP address or `curl -s http://169.254.169.254/latest/meta-data/public-hostname` for Public DNS name.

- With this, MEAN STACK HAS BEEN IMPLEMENTED
