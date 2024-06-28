# How to setup a new Laravel app with Laravel-Base

1. Fork this repo and `git pull` into the directory where you want to initialize the project (e.g. if `pwd = /home/user/src` we will be creating the new Laravel app at `home/user/src/laravel-app`).

2. Open the directory you just pulled in an editor of your choice.

3. Modify the the following parameters in `docker-compose.yml` according to your preference:

| Variable | Description |
| - | - |
| user | This will be the username for the new user created to run commands within the docker container |
| image | Name of the image that will be built | 
| (app) container_name | Name of the container for the main Laravel application once it spins up |
| (nginx) container_name | Name of the container running the nginx server which serves the Laravel application |
| networks | Defines the name of the network these containers are on, the name doesn't matter much as long as all containers are on the same network |

*Tip: use the find and replace method to replace all occurrences of `laravel-base` with the desired project name*

4. Spin up the containers using the following:

> docker-compose build app   //builds the image according to the Dockerfile

> docker-compose up -d   //spins up the containers 

> docker-compose ps   //if everything went well, this will show you a list of containers that are currently running which should include the ones you just spun up

5. Execute into the `app` container to initialize a new Laravel project:

> docker-compose exec app bash   //executes bash inside the `app` container

*Note: if you're using Git Bash, you likely have to prefix `winpty` in front of the command above*

All instruction below should be exectued WITHIN the app container 
------

6. Double check that you're in the directory `/var/www` and initialize a new Laravel project:

> compose create-project laravel/laravel \<name-of-project\> 

7. At this point, the newly initialized Laravel project should be contained within a folder at the same directory level as your `Dockerfile` and `docker-compose.yml`, move all contents of thie folder up a level to where `Dockerfile` is, **DO NOT FORGET THE FILES THAT STARTS WITH A `.`**. The old empty project folder may be deleted once everything has been moved.

8. After you run the following command, you should be able to see your application at `localhost:8000`

> composer install