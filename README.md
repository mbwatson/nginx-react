# Nginx-Served React App


This is a `create-react-app`-generated React application deployed with Node's development server for development and served by [Nginx](https://hub.docker.com/_/nginx/) after building in [Node](https://hub.docker.com/_/node/).

## What This Accomplishes

No frills--get your basic React application up and running quickly.

## How to Use This

Replace everything in the `/app` directory with your project, ensuring that the necessary requirements are outlined for Node in the `package.json` file.

Tagging the builds and naming the running containers can be nice, as can running the containers detached. Thus those options appear in the examples below, as do a few of these other common things:

- There are two types of Dockerfiles--one designed for a development build and one for a production build. Each build command references the appropriate file.
- By default, the application will run on port 3000. Thus a common configuration will forward the host's port 80 onto the container's 3000, making the application accessible at `http://localhost` on the host. Of course, other ports are fine. In the production build, we pass traffic right through port 80.

## Development

##### Build

```bash
$ docker build -t react-app/dev -f Dockerfile-dev .
```

##### Run

```bash
$ docker run -p 80:3000 --name webapp-dev -d react-app/dev
```

## Production

For deployment, we employ multistage builds. This will allows for building the web application in one container (Node, in this case) and then copying the build files over to another container (a server container, Nginx in this case) to be served.

##### Build

```bash
$ docker build -t react-app/prod -f Dockerfile-prod .
```

##### Run

Here, we forward the host port 80 to the container's port 80 since that is the default port for HTTP access expected by Nginx.

```bash
$ docker run --name react-app -p 80:80 -d react-app/prod 
```

## Additional References

- Docker
  + Docker: [https://docs.docker.com](https://docs.docker.com)
  + Docker Compose: [https://docs.docker.com/compose/](https://docs.docker.com/compose/)
  + Docker Multi-Stage Builds [https://docs.docker.com/develop/develop-images/multistage-build/](https://docs.docker.com/develop/develop-images/multistage-build/)
- Nginx: [https://nginx.org/en/docs/](https://nginx.org/en/docs/)
- React JS: [https://reactjs.org/](https://reactjs.org/)