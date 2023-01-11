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


  
