---
title: "Vue with low-code GraphQL"
sub_title: "using Hasura, Apollo, and Auth0"
<!-- excerpt: -->
categories:
  - Technology
  - Guides
last_modified_at: 2020-05-29
published: true
---

## Using Hasura and Auth0 with Vue

If you're not familiar with [Hasura](https://hasura.io/), it's a low-code offering that provides a full GraphQL endpoint with an easy-to-use UI for defining data models, relationships, and permissions. Combined with [Auth0](https://auth0.com/), a managed authentication offering, Hasura can provide full authentication and authorization models with JWT tokens. With these two offerings we have everything we need for backend management. Creating a simple frontend with Vue means we can spin up full-stack applications in record time. This setup has let me spend more time focusing on features for users.

Both Hasura and Auth0 have stellar basic walkthough documentation so much of this will defer to those guides. The point of this post will be to cover specific issues I hit in this stack model and how to use the provided template to overcome these problems.

## Template example for this guide

Code references and setup can be found [in the example template repo](https://github.com/MasonSchneider/Vue-GraphQL-Template). This is a great source for starting out a new Vue+GraphQL project. The rest of this post will cover getting to this setup and the configuration required to make it work.

## Hasura Setup

### Hasura Instance

The easiest setup is [launching Hasura on Heroku](https://hasura.io/docs/1.0/graphql/manual/getting-started/heroku-simple.html). Once you have the instance up, be sure to create [an Admin secret](https://hasura.io/docs/1.0/graphql/manual/deployment/heroku/securing-graphql-endpoint.html) for security (you'll need this later).

### Users Table

In order to track users to grant users permissions to their data we need to create a table that tracks registered users from Auth0. To do this, we'll need to [create a 'users' table](https://hasura.io/docs/1.0/graphql/manual/getting-started/first-graphql-query.html#create-a-table) with at least an 'id' field that is text and a Primary Key of the table.

![Create Users snapshot](/assets/images/screenshotUsersTable.png)

## Auth0 Setup

### Hasura Integration

Hasura provides [an excellent guide](https://hasura.io/docs/1.0/graphql/manual/guides/integrations/auth0-jwt.html#guides-auth0-jwt) for getting started with Auth0 JWT tokens for authentication. Once you've completed the steps here some minor QoL tweaks are needed to have full integration.

### Hasura Permissions

Once your Auth0 rule is inserting User IDs into your users table and attaching the X-Hasura-User-ID, authorization can be configured. The [authorization guide](https://hasura.io/docs/1.0/graphql/manual/auth/authorization/index.html) is straightforward but it's important to note the columns field needs to be set as well as the row access.

### Auth0 Vue Integration

Auth0 gives a good [initial setup guide](https://auth0.com/docs/quickstart/spa/vuejs/01-login) but [I've made tweaks](https://github.com/MasonSchneider/Vue-GraphQL-Template/tree/master/src/auth) to better support Apollo.

The main difference is that rather than creating the auth client on the side, my app creates it as [a blocking step in main](https://github.com/MasonSchneider/Vue-GraphQL-Template/blob/master/src/main.js). It also sets the response_type to token_id so that ```getTokenSilently()``` returns a JWT token that can be sent to Hasura. With this, Apollo can create a function link without using a local storage of the JWT which is a security risk noted by Auth0.

## Apollo Configuration

As mentioned above, the entire [Apollo provider creation](https://github.com/MasonSchneider/Vue-GraphQL-Template/blob/master/src/main.js#L78) is blocked on Auth0 initializing. Without this I saw race conditions where the first Apollo call would fail from bad tokens but following calls would succeed because the tokens were then loaded and ready.

### Apollo GraphQL query to Hasura

Now that your user is authorized, identified, and tokens are loaded you can use Apollo to query your Hasura endpoint. This leads to a [super simple data model](https://github.com/MasonSchneider/Vue-GraphQL-Template/blob/master/src/views/Home.vue). With this pattern I've found myself spending a lot less time on wiring and more time on building.

## Common Mistakes

### Hasura permissions not including columns

If you're seeing ```field 'x' not found in type: 'y'``` and you're certain the field does exist it's likely permissions.

1. Go to the Hasura permisisons page for the table of the failing type
  ![Permissions snapshot](/assets/images/permissionsScreenshot.png)

2. Expand the role of the failing call and view allowed columns
  ![Column snapshot](/assets/images/screenshotColumns.png)
  
3. Enable the columns your query needs access to in that role

### Auth0 login on page refresh

If you custom rolled your auth0 client initialization you'll need to directly check for a current user session. However, if you're using the built in auth0 initializer then your client already pulls some cached login values for you so this isn't the issue.

My fix was [using a personal Google API token](https://auth0.com/docs/connections/social/google) rather than the Auth0 provided token for logins.

### First Apollo query fails with bad credentials

The Apollo Configuration section explains the need for wrapping the Apollo link header code in a wait on the Auth0 client. Essentially, Apollo and Auth0 examples usually load side-by-side using localstorage tokens that can time out. My fix was to wait until we've done an initial population of the user session before configuring Apollo and doing our first query.
