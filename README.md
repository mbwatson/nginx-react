# Nginx-Served React App


This is a `create-react-app`-generated React application deployed with Node's development server for development and served by [Nginx](https://hub.docker.com/_/nginx/) after building in [Node](https://hub.docker.com/_/node/) for production.

## What This Accomplishes

No frills--get your basic React application up and running quickly.

## How to Use This

Your application will live in a directory adjacent to the docker-related files, as shown in the tree shown below.

```
$ tree -L 2
.
├── app         # <-- The "app" directory is the root of your React application
│   ├── node_modules
│   ├── package.json
│   ├── package-lock.json
│   ├── public
│   └── src
├── docker-compose-prod.yml
├── docker-compose.yml
├── Dockerfile-dev
├── Dockerfile-prod
└── README.md
```

Ensure that the necessary requirements are outlined for Node in the `package.json` file.

There are two flavors of docker-compose files and of Dockerfiles--one of each for development and production builds. Each docker-compose command references the appropriate file.

By default, the application will run on port 3000. Thus a common configuration will forward the host's port 80 onto the container's 3000, making the application accessible at `http://localhost` on the host. Of course, other ports are fine. In the production build, we pass traffic right through port 80.

We mount the `app` directory so live editing can be used to adjust your application while the containers are running.

## Development

##### Build

```bash
$ docker-compose build
```

##### Run

```bash
$ docker-compose up
```

## Production

For deployment, we employ multistage builds. This will allows for building the web application in one container (Node, in this case) and then copying the build files over to another container (a server container, Nginx in this case) to be served.

##### Build

```bash
$ docker-compose -f docker-compose-prod.yml build
```

##### Run

Here, we forward the host port 80 to the container's port 80 since that is the default port for HTTP access expected by Nginx.

```bash
$ docker-compose -f docker-compose-prod.yml up
```

## Additional References

- Docker
  + Docker: [https://docs.docker.com](https://docs.docker.com)
  + Docker Compose: [https://docs.docker.com/compose/](https://docs.docker.com/compose/)
  + Docker Multi-Stage Builds [https://docs.docker.com/develop/develop-images/multistage-build/](https://docs.docker.com/develop/develop-images/multistage-build/)
- Nginx: [https://nginx.org/en/docs/](https://nginx.org/en/docs/)
- React JS: [https://reactjs.org/](https://reactjs.org/)