# Running wordpress + mysql in a docker container
Recently I was helping a charity to test wordpress plugin for them.  To test the plugin, I need to have wordpress running on my machine.  Docker is the easiest way to get the job done.  
The setup is running on  WSL (ubuntu 20) on a windows machine, so Docker desktop on windows + Docker backend on WSL.
The steps to setup:

1. create /home/wordpress to put files in.
2. create wordpress/.env
```
MYSQL_ROOT_PASSWORD=root_pwd
MYSQL_USER=db_user
MYSQL_PASSWORD=db_pwd
```
3. create the [docker-compose.yml](https://github.com/siufai6/wordpress_mysql_docker/blob/main/docker-compose.yml).   In the yml, we specify two services, wordpress and db.  In both services we are pointing to the .env files for  environment variables.  Note that in the db section, it allows mysql to create the db and the users such that wordpress can connect to later on.  The two services are also on the same network app_network.
4. As the wordpress image is a minimal one, we install vim editor on it so we can do basic editing of wordpress config file if necessary.
5. To do this and make the installation permanent, we  need to build a custom docker using the  [dockerfile](https://github.com/siufai6/wordpress_mysql_docker/blob/main/dockerfile)
6. Build and start the docker by docker-compose up --build -d
7. Then you should be able to access the wordpress on http://localhost:8000 

More often than not, you will need to do basic troubleshooting.  To check for logs of the services:
```
docker-compose logs -f db
docker-compose logs -f wordpress
```
