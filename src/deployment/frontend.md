# Frontend
## Building from source
The frontend application is written with VueJS and Typescript and,
like most web applications, uses an npm based packaging scheme.

Assuming you've checked out the repo, the following commands will build the project:

```bash
yarn install # This installs the project dependencies
yarn build   # This will compile the webapp
```

After running these commands, the app is ready for deployment.
The compiled app is in `./dist/`, which can be deployed with any web server.
VueJS has some special needs for serving files, which are documented 
[here](https://router.vuejs.org/guide/essentials/history-mode.html#example-server-configurations).

## Using the container image
The frontend application is also made available as a container image over at
https://cloud.docker.com/u/upowdb/repository/docker/upowdb/frontend.

You can run it simply by running this command:

```bash
docker run --rm -d -p 80:80 docker.io/upowdb/frontend
```