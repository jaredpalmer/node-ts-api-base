# Node-TS-Api-Base

This project includes the boilerplate for a basic rest-api made in Node.JS with Express + Typescript.

## Basic Requirements

1. Install Node.js (lts-version v12.18.3)
2. Install `yarn` if not present `curl -o- -L https://yarnpkg.com/install.sh | bash` (macOS and generic Unix environments)
3. Install required dependencies by `yarn`
4. `cp .example.env .env.dev`
5. `cp .example.env.test .env.test`
6. Create your DB (i.e. psql for Postgres: `psql -U <user> -h <host> -c "create database <db name>;"`) with same name as your .env file.
7. Run `ENVIRONMENT=[dev, test, prod] yarn migration:run`.
8. Start your server with `ENVIRONMENT=[dev, prod] yarn dev`.

## Some scripts

Add `ENVIRONMENT=[dev, prod]` before running scripts.
Why?: [Configuration file used by Typeorm](https://typeorm.io/#/using-ormconfig/which-configuration-file-is-used-by-typeorm)

Run `yarn build` to build js from typescript source.

Run `yarn start` to start the server from the compiled folder (/dist).

Run `yarn test` to run tests.

Run `yarn dev` to start and automatically detect any source-code changes, restarting the server as well.

Run `yarn schema:drop` to drop your schema of the DB.

Run `yarn schema:sync` to resync the schema of your DB.

Run `yarn seed:run` to run seed files.

Run `yarn db:reset` to drop schema and re run it, then seed the DB.

Run `yarn migration:generate` to create a new migration.

Run `yarn migration:run` to run pending migrations.

Run `yarn migration:revert` to rollback migrations.

Run `yarn migration:show` to see the list of all migrations (pending and also ran).


## Running with Docker

### Prerequisites
In order to run the app with Docker, you should install or update to the latest version, we recommend to install [Docker-Desktop](https://docs.docker.com/get-docker/) due to composer and some cool CLI-UI tools are included.

### Development with Docker

The following commands will build and run all you need to start working on the base, without any other installation requirements. Important: if you already have postgres running locally, you'll need to kill the service before run `docker-compose up`.

```
docker-compose --env-file .env.dev build
```

```
docker-compose --env-file .env.dev up
```

### Deployment with Docker (only for production)

The following commands will `build and run` a Docker image ready for production and size-optimized.

#### Build Docker image

```
docker build -f Dockerfile.prod -t node-ts-api-base .
```

#### Run docker image (you need to add .env file as param)

```
docker run --rm --env-file=.env.prod -p 3000:3000 --name node-api node-ts-api-base
```


## API Documentation

After running the server you will find OpenAPI Specification here: `http://<host>:<port>/docs`


## App scaffolding

This is the suggested scaffolding for this project. You can take a look at:

```bash
.
├── __tests__
│   └── ...
├── src
│   ├── config
│   │   └── ...
│   ├── controllers
│   │   └── ...
│   ├── database
│   │   └── ...
│   ├── entities
│   │   └── ...
│   ├── services
│   │   └── ...
│   ├── app.ts            (App root and is where the application will be configured.)
│   ├── server.ts         (HTTP server)
├── README.md
├── .nvmrc                (Locks down your Node version.)
├── jest.config.js        (Jest configuration file.)
├── yarn-lock.json
├── package.json          (Your application’s package manifest.)
├── tsconfig.json         (The TypeScript project configuration.)
├── prod-path.js          (Tool used to run in production, translates ts-path and alias)
```

## Dependencies

- [AdminBro](https://adminbro.com/) - Admin panel middleware.
- [routing-controllers](https://github.com/typestack/routing-controllers) - Create structured class-based controllers with decorators usage in Express.
- [routing-controllers-openapi](https://www.npmjs.com/package/routing-controllers-openapi) - Runtime OpenAPI v3 schema generation for routing-controllers.
- [swagger-ui-express](https://www.npmjs.com/package/swagger-ui-express) - Serves auto-generated swagger-ui API docs from express.
- [typeorm](https://typeorm.io/#/) - NodeJS ORM.
- [nodemon](https://nodemon.io/) - Utility that will monitor for any changes in your source and automatically restart your server.
- [multer](https://github.com/expressjs/multer) -  NodeJS middleware for handling multipart/form-data.
- [tsconfig-paths](https://github.com/dividab/tsconfig-paths#readme) - Utility to register relative paths set at tsconfig file
- [express-rate-limit](https://github.com/nfriedly/express-rate-limit) - Basic rate-limiting middleware used to limit repeated requests to public APIs
- [morgan](https://github.com/expressjs/morgan) - HTTP request logger middleware for node.js


## Code Quality

This repo is integrated with SonarQube for static code analysis and test coverage reporting. [This guide](https://www.notion.so/rootstrap/SonarQube-c87fcaef3fbe4d7995ad087486768a24#a59df288a98c4410807c02c2d381ec6a) covers all the steps, including how to run the test coverage on a local machine.
Use the provided `sonar-project.properties` as-is.
Once that is covered:
1. Run `yarn test:cover` to run tests with coverage reporting.
2. Run `sonar-scanner` to import the test results into the sonar dashboard.

## Docs

[Express documentation](https://expressjs.com/es/)
[Typescript documentation](https://www.typescriptlang.org/)

## Credits

**Express API Base** is maintained by [Rootstrap](http://www.rootstrap.com) with the help of our [contributors](https://github.com/rootstrap/express-api-base/graphs/contributors).

[<img src="https://s3-us-west-1.amazonaws.com/rootstrap.com/img/rs.png" width="100"/>](http://www.rootstrap.com)
