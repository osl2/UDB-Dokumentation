# Backend
## Building from source
The backend application is written Rust and,
like most rust applications, uses a cargo based packaging scheme.

### Dependencies
You'll development versions of the following libraries, which you can install using your distributions package manager:
 - sqlite
 - libpq
 - libgcc

Additionally, you'll need a rust installation. For that, see [rustup](https://rustup.rs)

### Compiling

Assuming you've checked out the repo, the following commands will build and test the project:

```bash
cargo check           # Checks syntax and basic linting
cargo clippy          # More advanced linting
cargo build --release # This will compile the backend
```

After running these commands, the app is ready for deployment.
The compiled app is in `./target/`.

If you want to build the postgres variant instead, you have to add `--no-default-features --features postgres` to the last of those commands.

## Using the container image
The backend application is also made available as a container image over at
https://cloud.docker.com/u/upowdb/repository/docker/upowdb/backend.

You can run it simply by running this command:

```bash
docker run --rm -d \
  -v /path/to/your/app.db:/path/to/your/app.db \
  -v /path/to/your/config.toml:/path/to/your/config.toml \
  -p 80:8080 docker.io/upowdb/backend
```

For the postgres variant, run this instead:

```bash
docker run --rm -d \
  -v /path/to/your/config.toml:/opt/upowdb/config.toml \
  -p 80:8080 docker.io/upowdb/backend:postgres
```