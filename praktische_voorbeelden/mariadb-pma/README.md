# MariaDB with PMA

## Prerequisites

- [Docker](https://docs.docker.com/)
- [Docker-compose](https://docs.docker.com/compose/)
- [An IDE of your choice](https://www.jetbrains.com/datagrip/)

# What is PMA

phpMyAdmin is a free and open-source web-based application designed to manage MySQL and MariaDB databases through a 
graphical user interface (GUI). 
phpMyAdmin provides a convenient way for users to interact with MySQL and MariaDB databases without needing to use 
command-line tools or write SQL queries manually. It is widely used by developers, database administrators, and website 
owners for managing their databases efficiently.

# How to use this stack

After starting this stack with:
```bash
docker-compose up -d
```

Docker will pull and deploy an image of MariaDB and a linked instance of PHPMyAdmin.
The usage of PHPMyAdmin is not mandatory, but it is included for easy usage of this stack.

The MariaDB database has the following credentials:
``` 
Username:
root

Password:
example
```

These can be changed in the compose file if needed.

## Ports

The Mariadb instance will be at the standard [localhost:3306]() and PMA will be at [http://localhost:8080/](http://localhost:8080/)


