---
title: "Vue with low-code GraphQL"
sub_title: "using Hasura, Apollo, and Auth0"
<!-- excerpt: -->
categories:
  - Technology
  - Guides
last_modified_at: 2020-05-29
published: false
---

## Using Hasura and Auth0 with Vue

If you're not familiar with [Hasura](https://hasura.io/), it's a low-code offering that provides a full GraphQL endpoint with an easy-to-use UI for defining data models, relationships, and permissions. Combined with [Auth0](https://auth0.com/), a managed authentication offering, Hasura can provide full authentication and authorization models with JWT tokens. With these two offerings we have everything we need for backend management. Creating a simple frontend with Vue means we can spin up full-stack applications in record time. This setup has let me spend more time focusing on features for users.

Both Hasura and Auth0 have stellar basic walkthough documentation so much of this will defer to those guides. The point of this post will be to cover specific issues I hit in this stack model and how to use the provided template to overcome these problems.

## Template example for this guide

Code references and setup can be found [in the example template repo](https://github.com/MasonSchneider/Vue-GraphQL-Template). This is a great source for starting out a new Vue+GraphQL project. The rest of this post will cover getting to this setup and the configuration required to make it work.

## Hasura Setup

## Auth0 Setup

## Apollo Configuration

## Common Mistakes

### Hasura permissions not including columns

If you're seeing ```field 'x' not found in type: 'y'``` and you're certain the field does exist it's likely permissions.

1. Go to the Hasura permisisons page for the table of the failing type
  ![Permissions snapshot](/assets/images/permissionsScreenshot.png)

2. Expand the role of the failing call and view allowed columns
  ![Column snapshot](/assets/images/screenshotColumns.png)
  
3. Enable the columns your query needs access to in that role

### Auth0 login on page refresh

