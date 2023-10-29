Project Documentation
This document outlines the necessary steps to run the project on your computer. Ensure that you have Git and Docker installed on your system before getting started.

Clone the Project
Open a terminal on your computer.

Navigate to the directory where you want to clone the project using the 'cd' command.

Use the following command to clone the project from the Git repository:

```bash
git clone <git@github.com:endricklosange/TpDocker.git>
```

Launch the Project
Navigate to the project directory you just cloned using the 'cd' command.

Use the following command to launch the Docker containers using the provided 'docker-compose.yaml' file:

```bash
docker-compose -f ./docker-compose.yaml up
```

This command starts the necessary Docker containers to run the application.

Once the containers are up and running, you can open a terminal inside the Symfony PHP container using the following command:

```bash
docker exec -it www_docker_php /bin/bash
```

This will allow you to access a terminal with Symfony CLI.

In the container's terminal, execute the Symfony command to apply database migrations:

```bash
symfony console doctrine:migrations:migrate
```

This will apply the database migrations.

Finally, you can access the application by opening a web browser and navigating to the following URL:

http://localhost/animal/