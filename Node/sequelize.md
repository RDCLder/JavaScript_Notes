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
  
- Dependencies
  - [pg](https://www.npmjs.com/package/pg)
    - Installs postgres
  - [pg-hstore](https://www.npmjs.com/package/pg-hstore)
    - For serializing and deserializing postgres JSON data to hstore format
  
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

- [Associations Tutorial](http://docs.sequelizejs.com/manual/tutorial/associations.html)

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

- hasMany
  - One-To-Many associations are connecting one source with multiple targets. The targets however are again connected to exactly one specific source.
  - e.g.
    ```js
    Project.hasMany(User, {as: 'Workers'})
    ```
    - This will add the attribute projectId or project_id to User. Instances of Project will get the accessors getWorkers and setWorkers.
    
- Edit Your Migration
  ```js
  up: (queryInterface, Sequelize) => {
    return queryInterface.addColumn(
      'users',
      'studentId',
      {
        type: Sequelize.INTEGER,
        references: {
          model: 'users',
          key: 'id'
        },
        allowNull: true
      }
    );
  }
  ```

- Edit Your Model: user.js
  ```js
  module.exports = (sequelize, DataTypes) => {
    const user = sequelize.define('user', {
      firstName: DataTypes.STRING,
      lastName: DataTypes.STRING,
      email: DataTypes.STRING
    }, {});
    //adds several userId to student table
    user.associate = function(models) {
      user.belongsTo(models.student);
    };
    return user;
  };
  ```
  
- Using Your Relation
  ```js
  db.user.create({
    firstName: 'Veronica', lastName: 'Lino', email: 'me@me.com', studentId: 2});
  //query with join
    db.user.findAll({include: [{model: db.student}]})
      .then((results) => {
        console.log(results[5].student.firstName);
    });
  ```
  
### Joins

```js
SELECT * FROM posts, users WHERE posts.user_id = users.id

Posts.findAll({
  include: [{
    model: User,
    required: true
   }]
}).then(posts => {
  /* ... */
});
```
  - Setting required to true is the key to producing an inner join.
  - For a left outer join (where you get all Posts, regardless of whether there's a user linked), change required to false or leave it off since that's the default:
  
- If you want to find all Posts belonging to users whose birth year is in 1984
  ```js
  Posts.findAll({
    include: [{
      model: User,
      where: {year_birth: 1984}
     }]
  }).then(posts => {
    /* ... */
  });
  ```
  
- If you want all Posts, regardless of whether there's a user attached but if there is a user then only the ones born in 1984, then add the required field back in
  ```js
  Posts.findAll({
    include: [{
      model: User,
      where: {year_birth: 1984}
      required: false,
     }]
  }).then(posts => {
    /* ... */
  });
  
- If you want all Posts where the name is "Sunshine" and only if it belongs to a user that was born in 1984
  ```js
  Posts.findAll({
    where: {name: "Sunshine"},
    include: [{
      model: User,
      where: {year_birth: 1984}
     }]
  }).then(posts => {
    /* ... */
  });
  
- If you want all Posts where the name is "Sunshine" and only if it belongs to a user that was born in the same year that matches the post_year attribute on the post, you'd do this:
  ```js
  Posts.findAll({
    where: {name: "Sunshine"},
    include: [{
      model: User,
      where: ["year_birth = post_year"]
     }]
  }).then(posts => {
    /* ... */
  });
  ```
  ```
  ```
  
## Migrations

- [Migrations Tutorial](http://docs.sequelizejs.com/manual/tutorial/migrations.html)

- General
  - Just like you use Git to manage changes in your source code, you can use migrations to keep track of changes to the database.
  - With migrations you can transfer your existing database into another state and vice versa.
  - Those state transitions are saved in migration files
    - Describe how to get to the new state and how to revert the changes in order to get back to the old state
    
- Change Models
  - Add your model: nickname: DataTypes.STRING
    ```js
    sequelize migration:create --name add-nickname
    ```

- Migration
  ```js
  module.exports = {
    up: (queryInterface, Sequelize) => {
      return queryInterface.addColumn(
        'users',
        'nickname',
        {
          type: Sequelize.STRING
        }
      );
    },
    down: (queryInterface, Sequelize) => {
      return queryInterface.removeColumn(
                'Users', 'nickname');
    }
  };
  ```
  
- Run Migration
  ```js
  sequelize db:migrate
  ```
  
- Skeleton
  - All migrations are expected to be located in a **migrations** folder at the top of the project
  - Sequelize binary can generate a migration skeleton
  - e.g.
    ```js
    module.exports = {
      up: function(queryInterface, Sequelize) {
        // logic for transforming into the new state
      },
      
      down: function(queryInterface, Sequelize) {
        // logic for reverting the changes
      }
    }
    ```
    
- queryInterface
  - The passed queryInterface object can be used to modify the database.
    - The Sequelize object stores the available data types such as STRING or INTEGER.
    - Function up or down should return a Promise.
  - e.g.
    ```js
    module.exports = {
      up: function(queryInterface, Sequelize) {
        return queryInterface.dropAllTables();
      }
    }
    ```
    
## Functions

- General
  - Using the queryInterface object described before, you will have access to most of already introduced functions.
  - There are other methods including some designed to change the database schema
  
### Common Methods

- dropTable
  ```js
  queryInterface.dropTable('nameOfTheExistingTable')
  ```
  
- dropAllTables
  ```js
  queryInterface.dropAllTables()
  ```
  
- renameTable
  ```js
  queryInterface.renameTable('Person', 'User')
  ```
  
- showAllTables()
  ```js
  queryInterface.showAllTables().then(function(tableNames) {})
  ```
  
- addColumn
  ```js
  queryInterface.addColumn(
    'nameOfAnExistingTable',
    'nameOfTheNewAttribute',
    Sequelize.STRING
  )
  ```
  
- removeColumn
  ```js
  queryInterface.removeColumn('Person', 'signature')

  // or with an explicit schema:

  queryInterface.removeColumn({
    tableName: 'Person',
    schema: 'public'
  }, 'signature');
  ```
  
- changeColumn
  ```js
  queryInterface.changeColumn(
    'nameOfAnExistingTable',
    'nameOfAnExistingAttribute',
    {
      type: Sequelize.FLOAT,
      allowNull: false,
      defaultValue: 0.0
    }
  )
  ```
