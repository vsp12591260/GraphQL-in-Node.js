# GraphQL-in-Node.js

GraphQL and Apollo Server
GraphQL is a query language for APIs that allows you to request only the data you need, unlike REST, which often requires multiple endpoints. While REST typically requires multiple endpoints for different resources (e.g., /users, /users/:id/orders), GraphQL consolidates everything into a single endpoint (e.g., /graphql). Clients interact with the server through this single endpoint, providing queries that define what data to retrieve, which solves the issue of over-fetching (too much data) or under-fetching (too little data).
Apollo Server is a popular, GraphQL-compliant server known for its simplicity and active support. Other tools available include:
Express-GraphQL: A flexible GraphQL server for Express applications.
Relay: A JavaScript framework for efficient data fetching with GraphQL.
Basic Structure of a GraphQL Server
The key components of a GraphQL server are:
Schema: Defines data types and the shape of queries. For example, a Query type with a hello field that returns a String.
Resolvers: Functions that fetch data as per the schema. For example, the resolver for hello returns "Hello, GraphQL!".
When handling a query, the server:
Validates the query.
Resolves fields using resolvers.
Returns the resulting data.
Creating the Basic GraphQL Server
In this section, we'll set up a step-by-step basic GraphQL server using Apollo Server 4.
Import Apollo Server and GraphQL types:
TypeScript
Copy to clipboard
1import { ApolloServer } from '@apollo/server';
2import { startStandaloneServer } from '@apollo/server/standalone';
Load necessary modules to create and define the GraphQL server.
Define Schema:
TypeScript
Copy to clipboard
1const typeDefs = `#graphql
2  type Query {
3    hello: String
4  }
5`;
The typeDefs (short for "type definitions") define the schema of a GraphQL API using the GraphQL Schema Definition Language (SDL). It acts as the contract between the client and server, describing the types of data the server can return and the operations (queries and mutations) it supports. Here, we define a simple schema with a Query type that has a single field hello, returning a String.
Define Resolvers:
TypeScript
Copy to clipboard
1const resolvers = {
2  Query: {
3    hello: () => 'Hello, GraphQL!',
4  },
5};
The resolver for the hello field returns the string 'Hello, GraphQL!'.
Initialize and Configure Apollo Server:
TypeScript
Copy to clipboard
1const server = new ApolloServer({
2  typeDefs,
3  resolvers,
4});
Start the Server:
TypeScript
Copy to clipboard
1const { url } = await startStandaloneServer(server, {
2  listen: { port: 4000 },
3});
4
5console.log(`🚀 Server ready at ${url}`);
When you run the server file, it should print:
Plain text
Copy to clipboard
1🚀 Server ready at http://localhost:4000/
Querying the Server
Now that your server is running, let's query it to test if everything works correctly. This involves making a GraphQL request programmatically.
Import Fetch Module:
Ensure your environment allows HTTP requests. If you're using Node.js, consider using the built-in fetch module available in the latest Node.js versions, or you can enable it through package managers like node-fetch if you are using older versions.
TypeScript
Copy to clipboard
1import fetch from 'node-fetch'; // Node.js < v18; otherwise, use built-in fetch
Define URL and Query:
TypeScript
Copy to clipboard
1const url = 'http://localhost:4000/';
2const query = `
3  query {
4    hello
5  }
6`;
Specify the URL of your GraphQL server and the query you want to run.
Create a Function to Execute the Query:
TypeScript
Copy to clipboard
1async function fetchGraphQLData() {
2  try {
3    const response = await fetch(url, {
4      method: 'POST',
5      headers: {
6        'Content-Type': 'application/json',
7      },
8      body: JSON.stringify({ query }),
9    });
10
11    const data = await response.json();
12    console.log(JSON.stringify(data, null, 2));
13  } catch (error) {
14    console.error('Error:', error);
15  }
16}
17
18fetchGraphQLData();
Running this function should give you the output:
JSON
Copy to clipboard
1{
2  "data": {
3    "hello": "Hello, GraphQL!"
4  }
5}
Note: In GraphQL, all operations (queries and mutations, we'll learn both later in the course) are sent as POST requests with a JSON body containing the query. GET request cannot have a body, which means the query, variables, and operation name all have to be sent through query parameters. This can be problematic since larger queries can easily cause certain servers to return HTTP 414 (URI Too Long). POST ensures that the query payload is encapsulated within the request body, making it easier to send complex queries with variables.
Running the above code confirms the server correctly handles your query and provides the expected response.
