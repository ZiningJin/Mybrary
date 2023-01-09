LibraryProject

[course ref](https://www.bilibili.com/video/BV1DA411W7j8?p=5&vd_source=bf262231a7575d1e66e605a6e643b9cb)

### Project Setup

1. NPM: 

   - npm init -y

     open `package.json`: change "main":"index.js" to "main":"server.js"

   - npm i express ejs express-ejs-layouts

   - npm i --save-dev nodemon

     open `package.json` and write down:

       "scripts": {

     ​    "start": "node server.js",

     ​    "devStart":"nodemon server.js"

       },

2. /server.js

   ```javascript
   const express = require('express')
   const app = express()
   const expressLayouts = require('express-ejs-layouts')
   
   app.set('view engine','ejs') #use ejs as view engine
   app.set('views',__dirname + '/views') #create views directory
   app.set('layout','layouts/layout') 
   app.use(expressLayouts)
   app.use(express.static('public'))#create public folder
   
   app.listen(process.env.PORT || 3000)
   ```

   - Npm run devStart 
   - open http://localhost:3000/, you will see nothing
   - Create routes folders
   - create models folder

3. /router/index.js THIS iS CONTROLLERS in MVC

   ```javascript
   const express = require('express')
   const router = express.Router()
   
   router.get('/', (req, res) => {
       res.send('Hello Charlie')
   })
   
   module.exports = router
   ```

   also in server.js, add the below line:

   ```javascript
   const indexRouter = require('./routes/index')
   app.use('/', indexRouter)
   ```

   - Npm run devStart and open localhost:3000 you shall see 'Hello Charlie'

4. /views/layouts/layout.ejs

   /views/index.ejs

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Mybrary</title>
   </head>
   <body>
       Before
       <br>
       <%- body %> //here will take contents from index.ejs
       <br>
       After
   </body>
   </html>
   ```

   change index.js into:

   ```javascript
   router.get('/', (req, res) => {
       res.render('index') # here is index.ejs
   })
   ```

   Now, when you open localhost:3000, you shall see Before Middle After

5. Mongodb installation on MacOS

   [ref](https://blog.csdn.net/weixin_40654622/article/details/127569053)

   - Go to https://www.mongodb.com/try/download/community download 4.2.23 version

   - drag unzipped package into /usr/local, rename it as `mongodb`

   - open terminal, `open -e .bash_profile`

     `export PATH=${PATH}:/usr/local/mongodb/bin`

     command+s save it and close bash_profile

   - `source .bash_profile`让文件生效, type in `mongod -version`查看配置是否生效

   - 在mongodb根目录下新建data和log文件夹，在data目录下新建db文件夹

   - cd /usr/local/mongodb, `mongod --fork -dbpath data --logpath log/mongo.log --logappend`

     type in `mongo`, `show dbs`则成功

6. npm i mongoose

   Server.js

   ```javascript
   const mongoose = require('mongoose')
   mongoose.connect(process.env.DATABASE_URL, {
       useNewUrlParser: true
   })
   const db = mongoose.connection
   db.on('error', error => console.error(error))
   db.once('open', () => console.log('Connected to Mongoose'))
   ```

7. npm i --save-dev dotenv

   .env

   ```javascript
   DATABASE_URL=mongodb://localhost/mybrary
   ```

   Server.js

   ```javascript
   if (process.env.NODE_END !== 'production') {
       require('dotenv').config() # here, change .load() to .config()
   }
   ```

8. git init

   .gitignore

   ```javascript
   .env
   node_modules
   ```

   

9. xxx

10. Xxx

