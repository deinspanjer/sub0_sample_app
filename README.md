This repo contains a sample app that demonstrates the capabilities of Sub0 platform.
To run this you need to have docker installed on your system and logged in with your dockerhub id.
At the moment, the images are private so you need to also request access (my email in github profile) for your dockerhub id.

```shellscript
git clone https://github.com/ruslantalpa/sub0_sample_app.git
cd sub0_sample_app
docker-compose up
```

In your browser navigate to `http://your.docker.machine.ip:8080/graphiql/`
Toggle the `Docs` panel (top right corner) to explore the types/endpoints

Use this JWT to run queries `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJyb2xlIjoiYWRtaW5pc3RyYXRvciIsInVzZXJfaWQiOjEsImNvbXBhbnlfaWQiOjF9.ate5mETtGRu-mfGF4jFt7pP1b4W85r2uEXt603D7obc`

You can also use `rpc/signup` and `rpc/login` to get your own jwt

Try these queries
```graphql
{
  projects {
    id
    name
    client {
      id
      name
    }
    tasks {
      id
      name
    }
  }
}
```

```graphql
mutation {
  insert {
    project(payload:{name: "New Project", client_id:1}){
      id
      name
      client {
        id
        name
      }
    }
  }
}
```

```graphql
mutation {
  update {
    project(id: 1, payload:{name: "Updated Name"}){
      id
      name
      client {
        id
        name
      }
    }
  }
}
```

Sub0 Platfrom
-------------
This is a collection of docker containers working together to provide an automated REST/GraphQL API over an existing PostgreSQL database.
The platform is built on top of PostgREST and OpenResty.
In addition to "stock PostgREST" this system provides

 - Eeverything is in docker for easy install/extension
 - PostgREST runs behind the nginx proxy to provide security/ssl/flexibility
 - Built-in cache capabilities
 - Ability to manipulate/validate request inflight before they reaches PostgREST using a precomputed AST (eg. enforce at least one filter on the endpoint)
 - GraphQL schema (soon to be Relay compatible)
 - An in-browser IDE for exploring your GraphQL schema (complete with documentation generated based on comments you add to the tables/views/columns in PostgreSQL)

 