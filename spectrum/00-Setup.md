## Project Setup

- RethinkDB
- Redis
- Yarn

Run the `install-dependencies` script to go through each worker and install all dependencies.

```sh
node shared/install-dependencies.js
```

> If using Docker, simply copy the docker-compose file to the root of the project and run the following command to download and run RethinkDB and Redis

```sh
docker compose -f docker-compose.dev.yml up -d
```

## Migrating the database

When you first download the code and want to run it locally you have to migrate the database and seed it with test data. First, start rethinkdb in its own terminal tab:

```sh
rethinkdb
```

Then, in a new tab, run these commands:

```sh
yarn run db:migrate
yarn run db:seed
# ⚠️ To empty the database (e.g. if there's faulty data) run yarn run db:drop
```

There's a shortcut for dropping, migrating and seeding the database too:

```sh
yarn run db:reset
```

The `testing` database used in end to end tests is managed separately. It is built, migrated, and seeded when you run:

```sh
yarn run start:api:test
```

To drop the `testing` database, go to http://localhost:8080/#tables while `rethinkdb` is running, and click Delete Database on the appropriate database.

## Getting the secrets

While the app will run without any secrets set up, you won't be able to sign in locally. To get that set up, copy the provided example secrets file to the real location:

```
cp now-secrets.example.json now-secrets.json
```

Now you're ready to run the app locally and sign into your local instance!


## Start the servers

Depending on what you're trying to work on you'll need to start different servers. Generally, all servers run in development mode by doing `yarn run dev:<workername>`, e.g. `yarn run dev:hermes` to start the email worker.

No matter what you're trying to do though, you'll want to have the API running, so start that in a background tab:

```
yarn run dev:api
```

## Develop the web UI

To develop the frontend and web UI run

```
yarn run dev:web
```
