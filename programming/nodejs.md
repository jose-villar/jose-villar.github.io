# NodeJS

## Parameters

- There are query string parameters (after /?) and route parameters (after
  ':'). Considering the following server
  `localhost:3000/api/items/:id/?sortBy=nam`:

        app.get('/api/items/:id', (req, res) => res.send(req.params.id));
        app.get('/api/items/:id', (req, res) => res.send(req.query.id));

## Dependencies

- Mongoose
- Express
- Nodemon
- Dotenv: make a `.env` file and run `node --require dotenv/config index.js`
- Underscore: provides support for the usual functional suspects (each, map,
  reduce, filter...) without extending any core JavaScript objects.
- Joi: validations

        import Joi from 'joi';

        const schema = {
          name: Joi.string().min(3).required()
        }

        const result = Joi.validate(req.body, schema)

        if(result.error) {
          res.status(400).send(result.error.details[0].message);
        }

- Debug:

        import createDebug from 'debug';
        const startupDebug = createDebug('app:startup');
        startupDebug("Use this instead of console log")

- Fawn: Transactions

        import mongoose from 'mongoose';
        import Fawn from 'fawn';
        Fawn.init(mongoose)

        try {
          new Fawn.task()
            .save('rentals', rental) // rentals is the name of the collection
            .update('movies', { _id: movie._id }, {
              $inc: { numberInStock: -1 }
            })
            .run(); // mandatory for all the opearations to be performed

          res.send(rental);
        }
        catch(ex) {
          res.status(500); // Internal server error
        }

- Joi-objectid: validating object ids in joi

        import Joi from 'joi';
        import createObjectId from 'joi-objectid';

        Joi.objectId = createObjectId(Joi);

        function validateRental(rental) {
          const schema = {
            customerId: Joi.objectId().required
          }
          return Joi.validate(rental, schema);
        }

- Lodash: Utilities for working with arrays, numbers, objects, etc.
- joi-password-complexity
- bcrypt: Hash passwords
- jsonwebtoken:
- express-async-errors: All you have to do is import it: `import
  'express-async-errors';`
- winston: logging
- winston-mongodb: logging to mongodb: `import 'winston-mongodb';`
- jest: `npm i jest --save-dev`. To make jest ES6 compatible, you need to do
  the following: run `npm i --save-dev babel-jest @babel/preset-env`. Then,
  create a file called `.babelrc` with the following content:

          {
            "presets": ["@babel/preset-env"]
          }

  Use `jest --coverage` to get more statistics about your tests

- jest-vim-reporter: `npm i --save-dev jest-vim-reporter`. Then, in the
  `package.json` file, you have to add the following content:

        "jest": {
          "reporters": ["./node_modules/jest-vim-reporter"]
        }

  To set a test with mongoose (not recommended), you should change the testing
  environment to node:

        "jest": {
          "testEnvironment": "node"
        }



- To install a development dependency, use: `npm i <package name> --save-dev`
- To uninstall a dependency, use: `npm un <package name>`

## Status Codes

- 404: Not found
- 400: Bad request: use when the client input is invalid
- 401: Unauthorized
- 403: Forbidden
- A 401 Unauthorized response should be used for missing or bad authentication,
  and a 403 Forbidden response should be used afterwards, when the user is
  authenticated but isn’t authorized to perform the requested operation on the
  given resource.

## Middleware

### Built-in Middleware Functions

        // parse json objects in the body of a request
        app.use(express.json());
        // Parse key-value pairs into json
        app.use(urlencoded({ extended:true }));
        // public is a folder where to put static stuff, like a txt file
        app.use(express.static('public'));

### Third-Party Middleware Functions

- Helmet: Help secure application by setting various http headers. It's better
  to use it early in the middleware stack.
- Morgan: Log http requests
- Cors: Improve security according to youtube video

### Custom Middleware Functions

- Middleware functions take a request object and either return the control to
  the client or call another middleware function.

        app.use( function(req, res, next) {
          console.log("Logging...");
          next()
        } )

## Environments

        console.log(`process.env.NODE_ENV`); //returns null if not set
        console.log(app.get('env')); // returns development by default

        if(app.get('env') === 'development') {
          app.use(morgan('tiny'));
          console.log("Morgan enabled...");
        }

- You can set an environment variable and run the program in the same line like
  this:

        PORT=4000 node index.js

- You can set 2 values for an environment variable like this:

        DEBUG=app:db,app:startup

## Templating Engines

- They are used for returning html markup to the client, instead of json
  objects. For example, you can use pug
