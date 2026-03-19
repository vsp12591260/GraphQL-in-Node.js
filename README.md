🚀 Step 1: Install Dependencies
Run this in your project folder:
npm init -y
npm install @apollo/server graphql
📁 Step 2: Create index.js
const { ApolloServer } = require('@apollo/server');
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
▶️ Step 3: Run Server
node index.js
🌐 Step 4: Open in Browser
Go to:
http://localhost:4000
🧪 Example Queries
✅ Query 1
query {
  hello
}
✅ Query 2
query {
  add(a: 5, b: 3)
}
🎯 Output
{
  "data": {
    "hello": "Hello Vivek 🚀"
  }
}
{
  "data": {
    "add": 8
  }
}
