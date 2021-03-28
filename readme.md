# Kanban Writeup

## Overall architecture

**FrontEnd**
- **Package.json** serves to hold the relevant metadata to the frontend, including dependencies, scripts, etc.
- **src** is a folder which holds all of our main components and important files.
- Within src, we have **index.js**, which renders **App.js**, and **index.css** (this is styling I used mainly from a template, with some of my own changes), which styles index.js , as well as App.js. We also have a **Components** folder, which holds our important components
- **App.js** is the main app component.
- **Todos.js** in Components represents a board in the kanban.
- **Task.js** represents a task in a board. 
- **AddTask.js** represents a button to add a task to a board.


**BackEnd**
- **Package.json**serves to hold the relevant metadata to the backend, including dependencies, scripts, etc.
- **Done.json** is the datatbase for the board of 'done' taks.
- **Todos.json** is the datatbase for the board of 'to do' taks.
- **InProgress.json** is the datatbase for the board of 'in progress' taks.
- **server.js** is the main file which holds all of the routes and handles backend tasks such as receiving and sending data to the frontend, and reading and writing to the json files reperesenting the database.


--- 

## Approach

**FrontEnd**
>I created the frontend using create-react-app, which automatically sets up some files and creates a React App, which I modified.
- **App.js** calls 3 Todos components: To Dos, In Progres, and Done.
- **Todos.js** in Components represents a board; the name of the board (toods, in progress, done, etc.) gets passed down from App.js, and is stored in the state and used to communicate with the backend using a 'GET' request to get task data. Task data from the backend gets convereted to Task components in componentDidMount. These task components are stored as an array of Task components called 'todos' in Task.js. When Todos.js is rendered, the title of the board is rendered as a header, the tasks (in todos) rendered as a list, and AddTask.js is rendered as a way for the user to add a task to that board.
- **Task.js** is called once by Todos.js for each task that exists in the backend for that board. The data that is given includes title, description, etc.
- **AddTask.js** is called once by Todos.js and implements an 'add task' button. The states include all the states the user would input to add a task, such as 'title', 'description', 'user', 'points', etc. as well as the name of the board it is a part of, which is passed down by Todos.js. It renders input boxes for each user input, and an 'add task' button, which upon being clicked, calls 'toDoSubmit'. toDoSubmit sends all of the current states of the AddTask component to the backend using a 'POST' request, so that the backend can update the database.


**BackEnd**
>I created the backend using json files as in-memory databases.
- **Done.json** is a json file. In this file, there is an array of json data items with the attributes 'title', description', 'points', 'user', which are all set to whatever data the frontend sends (user inputs) and 'board', which is set to 'Done'.
- **Todos.json** is a json file. In this file, there is an array of json data items with the attributes 'title', description', 'points', 'user', which are all set to whatever data the frontend sends (user inputs) and 'board', which is set to 'Todos'.
- **InProgress.json** is a json file. In this file, there is an array of json data items with the attributes 'title', description', 'points', 'user', which are all set to whatever data the frontend sends (user inputs) and 'board', which is set to 'In Progress'.
- **server.js** is a javascript file where all backend requests go to. In this file, I mainly use express to communicate with the frontend. All the json files are read using fs and parsed using JSON.parse(), so that when any of the 'GET' routes are called with 'board' as a parameter, the correct json data is returned (for example, if the board parameter is 'in progress', the data from InProgress.json will be sent). The other two important functions include 'deleteTask', which is called by a Task component; in deleteTask, the proper json file is chosen (based on the input parameter) and the task in the input parameter is deleted from the json file via writing to it. In addToDo, which is called by Todos.json, I insert a new task based on the parameters given in the input from the frontend by writing to the correct json file (based on input parameter 'board').

--- 

## How to get software running locally
> To get the software running locally, go to the backend github and download all files to a 'server' folder, and go to the frontend github and download all files to a 'client' folder. Put both of these folders intto one larger 'KanBan' folder. 

> Make sure you have both node.js and npm installed on your system, and if not, install. Make sure all dependencies from package.json are also installed.

> cd into client, and enter 'npm start'.

> cd into server, and enter 'npm start'.

> If you have any problems, email me at mayaio@sas.upenn.edu.

---

## Github repositories
- Backend: https://github.com/mayaaio/kanban-api
- Frontend: https://github.com/mayaaio/kanban-ui
- Link to video description: https://drive.google.com/file/d/1EJzuJWx11NFs7JAoRfpy1TAeUHvlJC7Q/view?usp=sharing
