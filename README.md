# webapps via docker

1. clone [devops-box](https://github.com/salmanwaheed/devops-box) and run virtual machine
2. choose your app and clone it
  * [phpmyadmin-demo](https://github.com/salmanwaheed/phpmyadmin-demo)
  * [nodejs-demo](https://github.com/salmanwaheed/nodejs-demo)
  * [django-demo](https://github.com/salmanwaheed/django-demo)
  * [flask-demo](https://github.com/salmanwaheed/flask-demo)
  * [nginx-proxy](https://github.com/salmanwaheed/nginx-proxy)
  * [jsp-demo](https://github.com/salmanwaheed/jsp-demo)
  * [wordpress-demo](https://github.com/salmanwaheed/wordpress-demo)
  * [ror-demo](https://github.com/salmanwaheed/ror-demo)
  <!-- * [laravel-demo](https://github.com/salmanwaheed/laravel-demo) -->
  <!-- * [symfony-demo](https://github.com/salmanwaheed/symfony-demo) -->
  <!-- * [spring-demo](https://github.com/salmanwaheed/spring-demo) -->
  <!-- * [golang-demo](https://github.com/salmanwaheed/golang-demo) -->
3. start `docker-compose up -d`
4. build or re-build image + start `docker-compose up -d --build --force-recreate`
5. stop `docker-compose down`

### run any linux command without going inside the container 
```bash
docker run --rm -it -v $PWD:/src <image> \
  sh -c '<ANY-LINUX-COMMAND>'

# below examples are running directly into the container without going inside
sh -c 'ls -la' # show list of files and directories
sh -c 'npm init && npm install -S express' # nodejs
sh -c 'django-admin startproject my_project_name' # django
sh -c 'pip install pyyaml pymysql' # any command
```

### go inside the container
```bash
# for stopped or dont have container
docker run --rm -it -v $PWD:/src <image> sh

# for running container
docker exec --rm -it <container-id> sh
```

### run the server or directly use `docker-compose up -d`
```bash
docker run --rm -it \
    --name <container-name> \
    -p <external_port>:<internal_port> \
    -v $PWD:/src \
    -d <image> \
    sh -c '<ANY-LINUX-COMMAND>'

# below examples are running directly into the container without going inside
sh -c 'nodemon index.js' # run nodejs server
sh -c 'python app.py' # run flask server
sh -c 'python manage.py runserver 0.0.0.0:80' # run django server
```

### remove all images, containers, cache, volumes & etc
```bash
docker system prune --volumes -a
```
