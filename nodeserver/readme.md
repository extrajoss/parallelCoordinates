# PlasticGui Node server

The PlasticGui back-end server is a Node Express server, that is designed to server JSON-based API requests, serve files, and handle a database.

Communication between web-client and the back-end server is done through a JSON-based API. In particular, this is achieved through an RPC-JSON api, where both the web-client and backend-server implements a uniform API so that new handlers can be added in a simple and transparent manner.

## Database

The server talks to the database through the Sequelize ORM. The default database is a simple single-file Sqlite3 database and writes to the file `nodeserver/database.sqlite`.

The database schema only uses database fields that can work with other databases in Sequelize, such as Postgres and MySQL.. The database can be changed in the server config file `client/src/config.js`. If you do use another database, you will have to set it up yourself. For instance to setup Postgres on Linux, here's an [installation guide](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-16-04).

## User authentication

The base user class in the database is implemented, which hooks into the the authentication library `passport`, which connects the datatabase to the session manager. It uses local strategy that saves user details into the local database.

## Files

- `app.js` - entry point of server, loads all other modules
- `config.js` - configuration of the IP, and database
- `router.js` - this defines the key http handlers. In the RPC-JSON approach, there are only 3 handlers, a generic run handler, an upload handler, and a download handler. As well, there is a bridge to uploaded files, which are publically accessible.
- `models/index.js` - defines the database models, and all database access functions - these only accepts and returns Javascript object literals
- `handlers/index.js` - this defines all the javascript functions that are automatically accessible via the RPC-JSON api. These functions interface the database to the web-client.




