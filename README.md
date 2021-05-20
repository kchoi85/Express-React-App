
# Express-React-app
**MongoDB + Express + React + NodeJS Application**  
Connecting Frontend with Backend

## Folder Structure
![image](https://user-images.githubusercontent.com/52897657/118906450-d4af0f80-b8eb-11eb-9a35-9143f8a20e1b.png)

## Create Root Dir
```
mkdir express-react-app
cd express-react-app
```
## Create Express App (api)
```
npx express-generator api
cd api
npm install
```
## Configure a new route in Express API
```javascript
// On api/routes, create testAPI.js
var express = require(“express”);
var router = express.Router();

router.get(“/”, function(req, res, next) {
    res.send({ express: 'YOUR EXPRESS BACKEND IS CONNECTED TO REACT' });
});

module.exports = router;
```
## Create React App (Client)
```
npx create-react-app client
```  
## Setting up the proxy
```
cd client
> vi package.json
"proxy": "http://localhost:5000/"
```
## Calling Express backend from React
```javascript
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
state = {
    data: null
  };

  componentDidMount() {
      // Call our fetch function below once the component mounts
    this.callBackendAPI()
      .then(res => this.setState({ data: res.express }))
      .catch(err => console.log(err));
  }
    // Fetches our GET route from the Express server. (Note the route we are fetching matches the GET route from server.js
  callBackendAPI = async () => {
    const response = await fetch('/testAPI');
    const body = await response.json();

    if (response.status !== 200) {
      throw Error(body.message) 
    }
    return body;
  };

  render() {
    return (
      <div className="App">
        <header className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h1 className="App-title">Welcome to React</h1>
        </header>
        // Render the newly fetched data inside of this.state.data 
        <p className="App-intro">{this.state.data}</p>
      </div>
    );
  }
}

export default App;
```
## Start backend & frontend servers
```
// /api/
npm start
// /client/
npm start
```
## http://dev-r01edge.kihoon.lab.com:3000/
