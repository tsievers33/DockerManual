# Laravel development

## Prerequisites

- [Docker](https://docs.docker.com/)
- [Docker-compose](https://docs.docker.com/compose/)
- [An IDE of your choice](https://www.jetbrains.com/phpstorm/)

## Project setup
start off by pulling this project and giving the ```src``` directory all permissions.
```bash
sudo chmod -R a+rwx src
```

Now we are going to pull and deploy the stack (First install will take some time):
```bash
docker-compose up -d
```

(optional:) If you already have a stack for another project then it is recommended to create a fresh stack:
```bash
docker-compose build --no-cache # This will take significantly longer
```



Create a new Laravel project which will be placed in the ```src``` directory:
```bash
docker-compose run --rm composer create-project laravel/laravel .
```


Install dependecies:
```bash
docker-compose run --rm npm install  # Install dependecies
```

After the dependencies have been installed your project is available at:  [http://localhost:8181/](http://localhost:8181/).
### Compiling assets
If you are planning on using Vite you need to add the following to the 'scripts' in your ```package.json``` file:

```js
"scripts": {
  "dev": "vite --host 0.0.0.0",
  "build": "vite build"
},
```

After this is done asset compilations will be available with:
```bash
docker-compose run --rm --service-ports npm run dev # Start development server
```
Keep this terminal window open during development.

# Further usage:
Common commands that are used during the development of Laravel projects are available through the containers
that this stack creates. For example:

```bash
docker-compose run --rm composer require laravel/passport # Install Laravel Passport
```

```bash
docker-compose run --rm npm list  # List dependencies
```

```bash
docker-compose run --rm artisan migrate # Run migrations
```


