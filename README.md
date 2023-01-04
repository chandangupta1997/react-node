We see how our requests are being handled by our Node API, so we need to write some code that will display our React app when it is requested by our user (for example, when we go to the home page of our app).

We can do this back in server/index.js by adding the following code:

// server/index.js
const path = require('path');
const express = require('express');

...

// Have Node serve the files for our built React app
app.use(express.static(path.resolve(__dirname, '../client/build')));

// Handle GET requests to /api route
app.get("/api", (req, res) => {
  res.json({ message: "Hello from server!" });
});

// All other GET requests not handled before will return our React app
app.get('*', (req, res) => {
  res.sendFile(path.resolve(__dirname, '../client/build', 'index.html'));
});
This code will first allow Node to access our built React project using the express.static function for static files.

And if a GET request comes in that is not handled by our /api route, our server will respond with our React app.

This code allows our React and Node app to be deployed together on the same domain.