# Docker frontend

## Step 1: Build docker image

```bash
docker build -t dockerid/projectname -f Dockerfile.dev .
```

## Step 2: Run project using docker volumes

- It's essentially used for setting up a mapping from a folder inside the container to a folder outside the container (so that for any change we don't have to rebuild the docker image)

- For linux/unix

  ```bash
  docker run -p 3000:3000 -v /app/node_modules -v $(pwd):/app <image_id/image_name>
  ```

- For windows

  ```powershell
  docker run -p 3000:3000 -v /app/node_modules -v ${pwd}:/app <image_id/image_name>
  ```

## Step 2: Run project using docker-compose (optional)
Since the docker run command is big and a little complex, `docker-compose.yml` is created to start the container using short command. All the cases are specified in `yml` file.

```bash
docker-compose up --build
```
