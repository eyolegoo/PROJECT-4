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

- In previous projects I used different tools to connect to an EC2 instance, but if I do not want to install or launch anything outside of AWS, I can open my     CLI straight from Web Console in AWS, like this: [WebConsole](https://www.darey.io/wp-content/uploads/2021/02/WebConsole.gif)

- **TASK**
- In this assignment I implemented a simple **Book Register web form** using MEAN stack.


**STEP 1: Install NodeJs**

- **Node.js** is a JavaScript runtime built on Chrome’s V8 JavaScript engine. Node.js is used in this tutorial to set up the Express routes and AngularJS         controllers.

- Update ubuntu using `sudo apt update`

- Upgrade ubuntu using `sudo apt upgrade`

- I added certificates

`sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates

curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -`
  
