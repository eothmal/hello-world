>npm init (once time, just enter accep default)
>npm i express express-graphql graphql
update package.json :
 "main": "server.js",
>npm install --save-dev nodemon
update package.json :
 "scripts": {
    "devStart": "nodemon server.js"
  },
>npm run devStart

server.js
const express = require('express')
const expressGraphQL = require('express-graphql')
const {
  GraphQLSchema,
  GraphQLObjectType,
  GraphQLString
} = require('graphql')
const app = express()

const schema = new GraphQLSchema({
  query: new GraphQLObjectType({
   name: 'HelloWorld',
   fields: () => ({
    message: {
      type: GraphQLString,
      resolve: () => 'Hello World'
    }
   })
 })
})

app.use('/graphql', expressGraphQL({
  schema: schema,
  graphiql: true
}))
app.listen(5000, () => console.log('Server Running'))
