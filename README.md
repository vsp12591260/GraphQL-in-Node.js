# Step 1: Install Dependencies
Run this in your project folder:

```npm init -y
npm install @apollo/server graphql
```

# Step 2 Create Index.js

```const { ApolloServer } = require('@apollo/server');
const { startStandaloneServer } = require('@apollo/server/standalone');

// 1. Define Schema (NO gql needed)
const typeDefs = `
  type Query {
    hello: String
    add(a: Int, b: Int): Int
  }
`;

// 2. Define Resolvers
const resolvers = {
  Query: {
    hello: () => "Hello Vivek 🚀",
    add: (_, args) => args.a + args.b,
  },
};

// 3. Create Server
const server = new ApolloServer({
  typeDefs,
  resolvers,
});

// 4. Start Server
async function startServer() {
  const { url } = await startStandaloneServer(server, {
    listen: { port: 4000 },
  });

  console.log(`🚀 Server ready at ${url}`);
}

startServer();


```

# Step 3 Run Server

Run the Server (using node index.js)

Server will be opened in the Port No. 


# Step 5 Running the Queries

query {

  hello
  
}



