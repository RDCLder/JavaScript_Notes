# Sequelize

## General

- [Sequelize](http://docs.sequelizejs.com/)
  - Promise-based ORM for Node.js v4 and up
  - Features solid transaction support, relations, read replication and more
  - Supports the dialects PostgreSQL, MySQL, SQLite and MSSQL
  
- [Sequelize-cli](https://www.npmjs.com/package/sequelize-cli) Commands
  - db:migrate Run pending migrations
  - db:migrate:schema:timestamps:add Update migration table to have timestamps
  - db:migrate:status List the status of all migrations
  - db:migrate:undo Reverts a migration
  - db:migrate:undo:all Revert all migrations ran
  - db:create Create database specified by configuration
  - db:drop Drop database specified by configuration
  - init Initializes project
  - init:config Initializes configuration
  - init:migrations Initializes migrations
  - init:models Initializes models
  - init:seeders Initializes seeders
  - migration:generate Generates a new migration file [aliases: migration:create]
  - model:generate Generates a model and its migration [aliases: model:create]
  
- [pg pg-hstore](https://www.npmjs.com/package/pg-hstore)
  - node package for serializing and deserializing JSON data to hstore format
  
- Initialize Project
  - Initialize sequelize
    ```js
    sequelize init
    ```
  - Modify Config File
    ```js
    {
      "development": {
       "username": "postgres", // Change username
        "password": null,
         "database": "database_name", // Change to database name
        "host": "127.0.0.1",
         "dialect": "postgres" // Change to db language of project
      },
      "production": {
        "use_env_variable": "DATABASE_URL"
      }
    }
    ```
    
- Generate Models
  ```js
  sequelize model:generate --name user \
    --attributes firstName:string,lastName:string,email:string
  ```
  
- Run the Migration
  ```js
  sequelize db:migrate
  ```
  
## CRUD Operations

- Model.findAll()
  - Search for multiple elements in the database
  - e.g.
    ```js
    db.user.findAll()
      .then((results) => {
        results.forEach(function(index){
        console.log(index.id, index.firstName);
    })
      });
    ```
    
- Model.findById(id)
  - Search for a single instance by its primary key
  - eg.
    ```js
    models.post.findById(1).then(function(post){
     console.log(post);
    })
    ```
    
- Model.create({key:'value'})
  ```js
  db.user.create({firstName:'Eric', lastName: 'Fisher', email: 'me@me.com'})
    .then(function(user){
        console.log(user);
    });
  ```
  
- Model.findAll({where: {key: 'value'}})
  ```js
  db.user.findAll({where: {lastName: 'Fisher'}})
    .then((results) => {
      results.forEach(function(index){
              console.log(index.id, index.firstName);
          })
    });
  ```
  
- Model.destroy({where: {id:num}})
  ```js
  Model.destroy({
    where: {
       id: 123 //this will be your id that you want to delete
    }
  }).then(function(rowDeleted){ // rowDeleted will return number of rows deleted
   if(rowDeleted === 1){
      console.log('Deleted successfully');
    }
  }, function(err){
     console.log(err); 
  });
  ```
  
- db.sequelize.query(SQL, {model: modelName})
  ```js
    db.sequelize.query('SELECT * FROM users', { type: sequelize.QueryTypes.SELECT}).then(results => {
    results.forEach(function(record){
        console.log(record.firstName);
    })
  });
  ```

- Saving Data
  ```js
  var db = require('./models');
  var me;
  // create a user
  db.user.create({nickname: "PDiddy"})
    .then(function (user) {
      console.log(user);
      me = user;
      // update a user
      me.firstName = 'Veronica';
      me.save().then(() => {
        console.log('done saving');
      });
    });
  ```
  
  - Querying
  ```js
  // Full table
  db.user.findAll()
    .then((results) => {
      var r = results[0];
      console.log(r.id, r.nickname);
    });
  // Where clause  
  db.user.findAll({where: {nickname: 'PDiddy'}})
    .then((results) => {
      var r = results[0];
      
## Associations

- belongsTo
  - BelongsTo associations are associations where the foreign key for the one-to-one relation exists on the source model.
  - e.g.
    - A simple example would be a Player being part of a Team with the foreign key on the player.
    ```js
    const Player = this.sequelize.define('player', {/* attributes */});
    const Team  = this.sequelize.define('team', {/* attributes */});
    
    Player.belongsTo(Team); 
    // Will add a teamId attribute to Player to hold the primary key value for Team
    ```
      console.log(r.id, r.nickname);
    });
  ```
