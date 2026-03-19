# GraphQL and Apollo Server

GraphQL is a query language for APIs that allows you to request only the data you need, unlike REST, which often requires multiple endpoints. While REST typically requires multiple endpoints for different resources (e.g., /users, /users/:id/orders), GraphQL consolidates everything into a single endpoint (e.g., /graphql). Clients interact with the server through this single endpoint, providing queries that define what data to retrieve, which solves the issue of over-fetching (too much data) or under-fetching (too little data).

# Apollo Server is a popular, GraphQL-compliant server known for its simplicity and active support. Other tools available include:
# Express-GraphQL: A flexible GraphQL server for Express applications.
# Relay: A JavaScript framework for efficient data fetching with GraphQL.

# Basic Structure of a GraphQL Server

The key components of a GraphQL server are:

Schema: Defines data types and the shape of queries. For example, a Query type with a hello field that returns a String.
Resolvers: Functions that fetch data as per the schema. For example, the resolver for hello returns "Hello, GraphQL!".

When handling a query, the server:
Validates the query.
Resolves fields using resolvers.
Returns the resulting data.

# Creating the Basic GraphQL Server
In this section, we'll set up a step-by-step basic GraphQL server using Apollo Server 4.
Import Apollo Server and GraphQL types:

import { ApolloServer } from '@apollo/server';
import { startStandaloneServer } from '@apollo/server/standalone';
