MERN STACK IMPLEMENTATION

SIMPLE TO-DO APPLICATION ON MERN WEB STACK

MERN Web stack consists of following components:

MongoDB: A document-based, No-SQL database used to store application data in a form of documents.

ExpressJS: A server side Web Application framework for Node.js.

ReactJS: A frontend framework developed by Facebook. It is based on JavaScript, used to build User Interface (UI) components.

Node.js: A JavaScript runtime environment. It is used to run JavaScript on a machine rather than in a browser


TO GET THE LOCATION OF NODEJS SOFTWARE FROM ubuntu REPOSITORIES
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

INSTALL NODEJS

sudo apt-get install -y nodejs (to install nodejs why apt-get instead of just apt)

-y is to answer yes automatically for any questions the installation asks for

check if nodejs and npm are both installed 
node -v and npm -v
if npm isnt installed 
type sudo apt install npm

make a dir mkdir Todo
then move into the directory or folder
cd Todo

You now need to make this folder a nodejs project by typing npm init which would generate you a package.json file which contains all information about this project
append -y to npm init -y to answer yes for all questions the initialization may ask for or not
type the ls command to list everything in the directory to show the package.json which means the npm init command worked

NEXT we install ExpressJS npm install express

installing express creates a new folder named node_modules and a file named package-lock.json
the node_modules holds the expressjs files while the package-lock.json holds the specific versions of expressjs versions and other packages or libraries you have installed in your project

craete a file named index.js

Install the dotenv module
npm install dotenv

paste the following code into the index.js file using vim terminal text editor
const express = require('express');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use((req, res, next) => {
res.send('Welcome to Express');
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});

now run your app by tying node index.js or node [your_file_name]

you shoulde see [Server running on port 5000]

now go to aws ec2 instance security group to add inboud rules for tcp port 5000 to access your app from the outside world

now get your ec2 intance public ip then append :5000 to it to access your app via the browser
if all goes well you should see [Welcome to Express]

NOW we craete a directory named routes to hold our application routes
mkdir routes
then 
cd routes
then 
touch api.js

open api.js with vim
then paste the below code

const express = require ('express');
const router = express.Router();

router.get('/todos', (req, res, next) => {

});

router.post('/todos', (req, res, next) => {

});

router.delete('/todos/:id', (req, res, next) => {

})

module.exports = router;

MODELS
We use models in javascript applications to define database schemas means we use models to describe how our databases would and should look like

[
    In essence, the Schema is a blueprint of how the database will be constructed, including other data fields that may not be required to be stored in the database.
]

To create a Schema and a model, install mongoose which is a Node.js package that makes working with mongodb easier.

create a folder named models the cd into models

Inside the models folder, create a file and name it todo.js

NOW OPEN todo.js
then paste the following code 
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

//create schema for todo
const TodoSchema = new Schema({
action: {
type: String,
required: [true, 'The todo text field is required']
}
})

//create model for todo
const Todo = mongoose.model('todo', TodoSchema);

module.exports = Todo;

lets go edit our route file
by deleting wats there and pasting the following
const express = require ('express');
const router = express.Router();
const Todo = require('../models/todo');

router.get('/todos', (req, res, next) => {

//this will return all the data, exposing only the id and action field to the client
Todo.find({}, 'action')
.then(data => res.json(data))
.catch(next)
});

router.post('/todos', (req, res, next) => {
if(req.body.action){
Todo.create(req.body)
.then(data => res.json(data))
.catch(next)
}else {
res.json({
error: "The input field is empty"
})
}
});

router.delete('/todos/:id', (req, res, next) => {
Todo.findOneAndDelete({"_id": req.params.id})
.then(data => res.json(data))
.catch(next)
})

module.exports = router;

NOW TO THE DATABSE SEQMENT WE WOULD USE MLAB OR ATLAS

so go to [https://www.mongodb.com/atlas-signup-from-mlab] to sign up for a free account
go thru the onboarding process and create your cluster and choose AWS as cloud provider

mongodb+srv://taofik:<password>@cluster0.kvsbm.mongodb.net/myFirstDatabase?retryWrites=true&w=majority

paste ur connection string in [.env file]

then update ur index.js file with the following code
const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const routes = require('./routes/api');
const path = require('path');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

//connect to the database
mongoose.connect(process.env.DB, { useNewUrlParser: true, useUnifiedTopology: true })
.then(() => console.log(`Database connected successfully`))
.catch(err => console.log(err));

//since mongoose promise is depreciated, we overide it with node's promise
mongoose.Promise = global.Promise;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use(bodyParser.json());

app.use('/api', routes);

app.use((err, req, res, next) => {
console.log(err);
next();
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});

NOW START YOUR SERVER with node index.js
Simple TO-DO Web Application on MERN STACK

BACKEND CONFIGURATION

INSTALLING EXPRESSJS

MODELS

MONGODB DATABASE

FRONTEND CREATION

npx create-react-app client init a react app in the same root directory

Install concurrently. It is used to run more than one command simultaneously from the same terminal window.
npm install concurrently --save-dev
npm install nodemon --save-dev

change the script in the todo folder to 
"start": "node index.js",
"start-watch": "nodemon index.js",
"dev": "concurrently \"npm run start-watch\" \"cd client && npm start\""

CONTINUATION ON CREATING FRONTEND