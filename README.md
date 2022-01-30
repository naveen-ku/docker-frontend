# Docker frontend

## Start development server

### Step 1: Build docker image

```bash
docker build -t dockerid/projectname -f Dockerfile.dev .
```

### Step 2: Run project using docker volumes

- It's essentially used for setting up a mapping from a folder inside the container to a folder outside the container (so that for any change we don't have to rebuild the docker image)

- For linux/unix

  ```bash
  docker run -p 3000:3000 -v /app/node_modules -v $(pwd):/app <image_id/image_name>
  ```

- For windows

  ```powershell
  docker run -p 3000:3000 -v /app/node_modules -v ${pwd}:/app <image_id/image_name>
  ```

### Step 2: Run project using docker-compose (optional)
Since the docker run command is big and a little complex, `docker-compose.yml` is created to start the container using short command. All the cases are specified in `yml` file.

```bash
docker-compose up --build
```

## Start production server
```bash
docker build .
docker run -p 8080:80 <image_id>
```


## AWS Deployment Travis config for deployment

### Step 1: Create AWS account 
Setup `elasticbeanstalk` for this project. Create new application and environment from dashboard.

### Step 2: Add the following code on `.travis.yml`

```yml
deploy:
  provider: elasticbeanstalk
  region: "<region_name>"
  app: "<app_name_on_aws>"
  env: "<env_name_on_aws>"
  bucket_name: "<s3_bucket_name>"
  bucket_path: "<app_name_on_aws>"
  on:
    branch: master
  access_key_id: $aws_access_key_idgit 
  secret_access_key: 
    secure: "$aws_secret_key"

```

### Step 3: Create secret key on AWS and add them to travis ci dashboard env variable
- Go to IAM services on AWS
- Create new user 
- Attach existing policies to this user (policies are basically permissions)
- Give permission to provide full access to AWS elastic beanstalk
- Access key ID and secret access key are generated
- Go to travis ci dashboard and select the current project and go to settings
- Add access key ID and secret access key as environment variable

